---
title: "Modifica di dati con valori di grandi dimensioni (max) in ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Modifica di dati con valori di grandi dimensioni (max) in ADO.NET
I tipi di dati LOB \(oggetti di grandi dimensioni\) sono quelli che superano la dimensione massima di 8 kilobyte \(KB\) per le righe.  In SQL Server viene fornito un identificatore `max` per i tipi di dati `varchar`, `nvarchar` e `varbinary` per consentire l'archiviazione di valori di dimensioni pari a 2^32 byte.  Nelle colonne di tabelle e nelle variabili Transact\-SQL possono essere specificati tipi di dati `varchar(max)`, `nvarchar(max)` o `varbinary(max)`.  In ADO.NET i tipi di dati `max` possono essere recuperati da un `DataReader` e possono inoltre essere specificati come parametri di input e di output senza richiedere una gestione speciale.  Per tipi di dati `varchar` di grandi dimensioni, è possibile recuperare e aggiornare i dati in modo incrementale.  
  
 I tipi di dati `max` possono essere usati per eseguire confronti, come le variabili Transact\-SQL, e per eseguire concatenazioni.  È inoltre usarli nelle clausole DISTINCT, ORDER BY e GROUP BY di un'istruzione SELECT, nonché nelle aggregazioni, nelle unioni e nelle sottoquery.  
  
 La tabella seguente fornisce i collegamenti alla documentazione online di SQL Server.  
  
 **Documentazione online di SQL Server**  
  
1.  [Uso di tipi di dati per valori di grandi dimensioni](http://go.microsoft.com/fwlink/?LinkId=120498)  
  
## Restrizioni per i tipi di valori di grandi dimensioni  
 Le seguenti restrizioni si applicano ai tipi di dati `max` e non ai tipi di dati di dimensioni minori:  
  
-   Un tipo `sql_variant` non può contenere un tipo di dati `varchar` di grandi dimensioni.  
  
-   Le colonne `varchar` di grandi dimensioni non possono essere specificate come colonne di chiave primaria in un indice.  Sono consentite in una colonna inclusa in un indice non cluster.  
  
-   Le colonne `varchar` di grandi dimensioni non possono essere usate come colonne chiave di partizionamento.  
  
## Uso di tipi di valori di grandi dimensioni in Transact\-SQL  
 La funzione `OPENROWSET` di Transact\-SQL è un metodo unico per eseguire la connessione e l'accesso ai dati remoti.  Include tutte le informazioni di connessione necessarie per l'accesso remoto ai dati da un'origine dati OLE DB.  È possibile fare riferimento a `OPENROWSET` nella clausola FROM di una query come se fosse un nome di tabella.  È inoltre possibile farvi riferimento come tabella di destinazione di un'istruzione INSERT, UPDATE o DELETE, soggetta alle funzionalità del provider OLE DB.  
  
 La funzione `OPENROWSET` include il provider di set di righe `BULK`, che consente di leggere i dati direttamente da un file senza caricare i dati in una tabella di destinazione.  Questo consente l'uso di `OPENROWSET` in una semplice istruzione INSERT SELECT.  
  
 Gli argomenti dell'opzione `OPENROWSET``BULK` forniscono un controllo notevole sul punto in cui iniziare e terminare la lettura dei dati, sulla gestione degli errori e sull'interpretazione dei dati.  È ad esempio possibile specificare che il file di dati venga letto come una singola riga o come un set di righe di una singola colonna di tipo `varbinary`, `varchar` o `nvarchar`.  Per la sintassi e le opzioni complete, vedere la documentazione online di SQL Server.  
  
 Nell'esempio seguente viene inserita una foto nella tabella ProductPhoto del database di esempio AdventureWorks.  Se si usa il provider `BULK``OPENROWSET`, è necessario fornire l'elenco di colonne denominato anche se non si inseriscono valori in ogni colonna.  In questo caso, la chiave primaria è definita come colonna Identity e può essere omessa dall'elenco di colonne.  Notare che è necessario fornire anche un nome di correlazione alla fine dell'istruzione `OPENROWSET`, che in questo caso è ThumbnailPhoto.  Tale nome è correlato alla colonna della tabella `ProductPhoto` in cui viene caricato il file.  
  
```  
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## Aggiornamento di dati tramite UPDATE .WRITE  
 L'istruzione Transact\-SQL UPDATE include una nuova sintassi WRITE per modificare il contenuto delle colonne `varchar(max)`, `nvarchar(max)` o `varbinary(max)`.  In tal modo è possibile eseguire aggiornamenti parziali dei dati.  La sintassi UPDATE .WRITE viene illustrata di seguito in formato abbreviato:  
  
 UPDATE  
  
 { *\<object\>* }  
  
 SET  
  
 { *column\_name* \= { .WRITE \( *espressione* , @Offset , @Length \) }  
  
 Il metodo WRITE specifica che una sezione del valore di *column\_name* verrà modificato.  L'espressione corrisponde al valore che verrà copiato in *column\_name*, l'argomento `@Offset` al punto di inizio in cui verrà scritta l'espressione e l'argomento `@Length` alla lunghezza della sezione nella colonna.  
  
|Se|Then|  
|--------|----------|  
|L'espressione è impostata su NULL.|Il valore di `@Length` viene ignorato e il valore di *column\_name* viene troncato in base al valore specificato di `@Offset`.|  
|Il valore di `@Offset` è NULL.|L'operazione di aggiornamento aggiunge l'espressione alla fine del valore di *column\_name* e il valore di `@Length` viene ignorato.|  
|Il valore di `@Offset` è maggiore della lunghezza del valore di column\_name.|SQL Server restituisce un errore.|  
|Il valore di `@Length` è NULL.|L'operazione di aggiornamento rimuove tutti i dati a partire da `@Offset` alla fine del valore di `column_name`.|  
  
> [!NOTE]
>  Il valore di `@Offset` o di `@Length` non può essere un numero negativo.  
  
## Esempio  
 In questo esempio di Transact\-SQL viene aggiornato un valore parziale di DocumentSummary, una colonna `nvarchar(max)` della tabella Document nel database AdventureWorks.  La parola "components" viene sostituita con la parola "features" specificando la parola di sostituzione, la posizione iniziale \(offset\) della parola da sostituire nei dati esistenti e il numero di caratteri da sostituire \(lunghezza\).  Per confrontare i risultati, nell'esempio sono incluse le istruzioni SELECT precedenti e successive all'istruzione UPDATE.  
  
```  
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## Uso di tipi di valori di grandi dimensioni in ADO.NET  
 È possibile usare tipi di valore di grandi dimensioni in ADO.NET specificandoli come oggetti <xref:System.Data.SqlClient.SqlParameter> `` in un oggetto <xref:System.Data.SqlClient.SqlDataReader> per restituire un set di risultati oppure usando un oggetto <xref:System.Data.SqlClient.SqlDataAdapter> per compilare un oggetto `DataSet` o `DataTable`.  Non vi è differenza tra il modo di usare un tipo di valore di grandi dimensioni e il relativo tipo di dati del valore di dimensioni minori.  
  
### Uso di GetSqlBytes per il recupero di dati  
 È possibile usare il metodo `GetSqlBytes` del tipo <xref:System.Data.SqlClient.SqlDataReader> per recuperare il contenuto di una colonna `varbinary(max)`.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlCommand> denominato `cmd` che consente di selezionare dati `varbinary(max)` da una tabella e un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare i dati come tipo <xref:System.Data.SqlTypes.SqlBytes>.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim bytes As SqlBytes = reader.GetSqlBytes(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### Uso di GetSqlChars per il recupero di dati  
 È possibile usare il metodo `GetSqlChars` del tipo <xref:System.Data.SqlClient.SqlDataReader> per recuperare il contenuto di una colonna `varchar(max)` o `nvarchar(max)`.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlCommand> denominato `cmd` che consente di selezionare dati `nvarchar(max)` da una tabella e un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare i dati.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim buffer As SqlChars = reader.GetSqlChars(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### Uso di GetSqlBinary per il recupero di dati  
 È possibile usare il metodo `GetSqlBinary` di un tipo <xref:System.Data.SqlClient.SqlDataReader> per recuperare il contenuto di una colonna `varbinary(max)`.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlCommand> denominato `cmd` che consente di selezionare dati `varbinary(max)` da una tabella e un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare i dati come flusso <xref:System.Data.SqlTypes.SqlBinary>.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim binaryStream As SqlBinary = reader.GetSqlBinary(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### Uso di GetBytes per il recupero di dati  
 Il metodo `GetBytes` di un tipo <xref:System.Data.SqlClient.SqlDataReader> consente di leggere un flusso di byte dall'offset della colonna specificata nella matrice di byte a partire dall'offset della matrice specificata.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare byte in una matrice di byte.  Notare che, a differenza di `GetSqlBytes`, con `GetBytes` è necessario specificare una dimensione per il buffer della matrice.  
  
```vb  
While reader.Read()  
    Dim buffer(4000) As Byte  
    Dim byteCount As Integer = _  
    CInt(reader.GetBytes(1, 0, buffer, 0, 4000))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### Uso di GetValue per il recupero di dati  
 Il metodo `GetValue` di un tipo <xref:System.Data.SqlClient.SqlDataReader> consente di leggere il valore dall'offset della colonna specificata in una matrice.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare dati binari dall'offset della prima colonna e dati di tipo stringa dall'offset della seconda colonna.  
  
```vb  
While reader.Read()  
    ' Read the data from varbinary(max) column  
    Dim binaryData() As Byte = CByte(reader.GetValue(0))  
  
    ' Read the data from varchar(max) or nvarchar(max) column  
    Dim stringData() As String = Cstr((reader.GetValue(1))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## Conversione da tipi di valore di grandi dimensioni a tipi CLR  
 È possibile convertire il contenuto di una colonna `varchar(max)` o `nvarchar(max)` usando uno dei metodi disponibili per la conversione di stringhe, ad esempio `ToString`.  Il seguente frammento di codice presuppone un oggetto <xref:System.Data.SqlClient.SqlDataReader> denominato `reader` che consente di recuperare i dati.  
  
```vb  
While reader.Read()  
    Dim str as String = reader(0).ToString()  
    Console.WriteLine(str)  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### Esempio  
 Il codice seguente consente di recuperare il nome e l'oggetto `LargePhoto` dalla tabella `ProductPhoto` del database `AdventureWorks` e di salvarlo in un file.  È necessario compilare l'assembly con un riferimento allo spazio dei nomi <xref:System.Drawing>.  Il metodo <xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> del tipo <xref:System.Data.SqlClient.SqlDataReader> restituisce un oggetto <xref:System.Data.SqlTypes.SqlBytes> che espone una proprietà `Stream`.  Questa viene usata nel codice per creare un nuovo oggetto `Bitmap`, che verrà quindi salvato nel formato`ImageFormat`GIF.  
  
 [!code-csharp[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/VB/source.vb#1)]  
  
## Utilizzo dei parametri di tipi di valore di grandi dimensioni  
 I tipi di valore di grandi dimensioni possono essere usati negli oggetti <xref:System.Data.SqlClient.SqlParameter> nello stesso modo in cui si usano tipi di valore di dimensioni minori in oggetti <xref:System.Data.SqlClient.SqlParameter>.  È possibile recuperare tipi di valore di grandi dimensioni come valori <xref:System.Data.SqlClient.SqlParameter>, come illustrato nell'esempio seguente.  Il codice presuppone l'esistenza della seguente stored procedure GetDocumentSummary nel database di esempio AdventureWorks.  La stored procedure accetta un parametro di input denominato @DocumentID e restituisce il contenuto della colonna DocumentSummary nel parametro di output @DocumentSummary.  
  
```  
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### Esempio  
 Il codice di ADO.NET crea oggetti <xref:System.Data.SqlClient.SqlConnection> e <xref:System.Data.SqlClient.SqlCommand> per eseguire la stored procedure GetDocumentSummary e recuperare le informazioni di riepilogo del documento archiviate come tipo di valore di grandi dimensioni.  Il codice passa un valore per il parametro di input @DocumentID e i risultati restituiti nel parametro di output @DocumentSummary vengono visualizzati nella finestra della console.  
  
 [!code-csharp[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/VB/source.vb#1)]  
  
## Vedere anche  
 [Dati binari e con valori di grandi dimensioni SQL Server](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [Mapping dei tipi di dati SQL Server](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [Operazioni sui dati SQL Server in ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)