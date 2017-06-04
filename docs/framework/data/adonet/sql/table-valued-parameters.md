---
title: "Parametri valutati a livello di tabella | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Parametri valutati a livello di tabella
I parametri con valori di tabella consentono di eseguire facilmente il marshalling di più righe di dati di un'applicazione client a [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] senza richiedere più round trip o logica speciale sul lato server per l'elaborazione dei dati.  È possibile usare i parametri con valori di tabella per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri.  Le righe di dati in arrivo vengono archiviate in una variabile di tabella che può quindi essere usata tramite [!INCLUDE[tsql](../../../../../includes/tsql-md.md)].  
  
 I valori di colonna nei parametri con valori di tabella sono accessibili tramite istruzioni SELECT [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] standard.  I parametri con valori di tabella sono fortemente tipizzati e la loro struttura viene convalidata automaticamente.  La dimensione dei parametri valutati a livello di tabella è limitata solo dalla memoria del server.  
  
> [!NOTE]
>  Non è possibile restituire dati in un parametro valutato a livello di tabella.  I parametri valutati a livello di tabella sono di solo input. La parola chiave OUTPUT non è supportata.  
  
 Per altre informazioni sui parametri con valori di tabella, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Parametri con valori di tabella \(Motore di database\)](http://go.microsoft.com/fwlink/?LinkId=98363) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Viene descritto come creare e usare i parametri con valori di tabella.|  
|[Tipi di tabella definiti dall'utente](http://go.microsoft.com/fwlink/?LinkId=98364) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Vengono descritti i tipi di tabella definiti dall'utente usati per dichiarare i parametri con valori di tabella.|  
|Sezione relativa al [Motore di database di Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=120507) di [CodePlex](http://go.microsoft.com/fwlink/?LinkID=67739)|Sono inclusi esempi che illustrano come usare le funzionalità di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].|  
  
## Passaggio di più righe nelle versioni precedenti di SQL Server  
 Prima dell'introduzione dei parametri con valori di tabella in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2008, le opzioni per passare più righe di dati a una stored procedure o a un comando SQL con parametri erano limitate.  Per passare più righe al server, uno sviluppatore poteva scegliere tra le opzioni seguenti:  
  
-   Usare una serie di parametri singoli per rappresentare i valori in più colonne e righe di dati.  La quantità di dati che è possibile passare tramite questo metodo è limitata dal numero di parametri consentiti.  Le routine di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] possono includere al massimo 2100 parametri.  Per assemblare questi singoli valori in una variabile di tabella o in una tabella temporanea per l'elaborazione è necessaria la logica sul lato server.  
  
-   Aggregare più valori di dati in stringhe delimitate o in documenti XML, quindi passare tali valori di testo a una routine o a un'istruzione.  A tale scopo, è necessario che la routine o l'istruzione includa la logica necessaria per la convalida delle strutture di dati e la separazione dei valori.  
  
-   Creare una serie di istruzioni SQL singole per le modifiche ai dati che riguardano più righe, ad esempio quelle create chiamando il metodo `Update` di un oggetto <xref:System.Data.SqlClient.SqlDataAdapter>.  Le modifiche possono essere inviate al server individualmente o raggruppate in batch.  Anche in caso di invio in batch che contengono più istruzioni, ogni istruzione viene tuttavia eseguita separatamente nel server.  
  
-   Usare l'utilità `bcp` o l'oggetto <xref:System.Data.SqlClient.SqlBulkCopy> per caricare numerose righe di dati in una tabella.  Sebbene questa tecnica sia molto efficace, non supporta l'elaborazione sul lato server, a meno che i dati non vengano caricati in una tabella temporanea o in una variabile di tabella.  
  
## Creazione di tipi di parametri con valori di tabella  
 I parametri con valori di tabella sono basati su strutture di tabella fortemente tipizzate definite tramite istruzioni CREATE TYPE [!INCLUDE[tsql](../../../../../includes/tsql-md.md)].  Per poter usare i parametri con valori di tabella nelle applicazioni client, è prima necessario creare un tipo di tabella e definire la struttura in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Per altre informazioni sulla creazione di tipi di tabella, vedere [Tipi di tabella definiti dall'utente](http://go.microsoft.com/fwlink/?LinkID=98364) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
 L'istruzione seguente consente di creare un tipo di tabella denominato CategoryTableType, costituito dalle colonne CategoryID e CategoryName:  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 Dopo aver creato un tipo di tabella, è possibile dichiarare i parametri con valori di tabella basati su tale tipo.  Nel frammento [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] seguente viene illustrato come dichiarare un parametro con valori di tabella in una definizione di stored procedure.  Si noti che, per dichiarare un parametro con valori di tabella, è necessaria la parola chiave READONLY.  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## Modifica di dati con i parametri con valori di tabella \(Transact\-SQL\)  
 I parametri con valori di tabella possono essere usati nelle modifiche dei dati basate su set che riguardano più righe eseguendo un'unica istruzione.  È ad esempio possibile selezionare tutte le righe in un parametro con valori di tabella e inserirle in una tabella di database oppure creare un'istruzione di aggiornamento tramite l'unione in join di un parametro con valori di tabella con la tabella che si desidera aggiornare.  
  
 L'istruzione UPDATE [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] seguente illustra come usare un parametro con valori di tabella tramite la sua unione in join con la tabella Categories.  Quando si usa un parametro con valori di tabella con un JOIN in una clausola FROM, è anche necessario usare un alias per il parametro, come illustrato di seguito, dove per il parametro con valori di tabella viene usato l'alias "ec":  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 In questo esempio [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] viene illustrato come selezionare le righe da un parametro con valori di tabella per eseguire un'istruzione INSERT in una singola operazione basata su set.  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## Limitazioni relative ai parametri con valori di tabella  
 Per i parametri con valori di tabella sono previste diverse limitazioni:  
  
-   Non è possibile passare i parametri con valori di tabella a [funzioni CLR definite dall'utente](http://msdn.microsoft.com/library/ms131077.aspx).  
  
-   I parametri con valori di tabella possono essere indicizzati solo per supportare vincoli UNIQUE o PRIMARY KEY.  In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] non vengono gestite statistiche relative ai parametri con valori di tabella.  
  
-   I parametri con valori di tabella sono di sola lettura nel codice [!INCLUDE[tsql](../../../../../includes/tsql-md.md)].  Non è possibile aggiornare i valori delle colonne nelle righe di un parametro con valori di tabella e non è possibile inserire o eliminare righe.  Per modificare i dati passati a una stored procedure o a un'istruzione con parametri in un parametro con valori di tabella, è necessario inserire i dati in una tabella temporanea o in una variabile di tabella.  
  
-   Non è possibile usare istruzioni ALTER TABLE per modificare la struttura dei parametri con valori di tabella.  
  
## Configurazione di un esempio SqlParameter  
 <xref:System.Data.SqlClient> supporta il popolamento dei parametri con valori di tabella da oggetti <xref:System.Data.DataTable>, <xref:System.Data.Common.DbDataReader> o System.Collections.Generic.IEnumerable\<<xref:Microsoft.SqlServer.Server.SqlDataRecord>\> \(<xref:System.Collections.Generic.IEnumerable%601>?qualifyHint=False&autoUpgrade=True).  È necessario specificare un nome di tipo per il parametro con valori di tabella usando la proprietà <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> di un oggetto <xref:System.Data.SqlClient.SqlParameter>.  `TypeName` deve corrispondere al nome di un tipo compatibile creato in precedenza nel server.  Nel frammento di codice seguente viene illustrato come configurare <xref:System.Data.SqlClient.SqlParameter> per inserire dati.  
  
```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(  
    sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```  
  
```vb  
' Configure the command and parameter.  
Dim insertCommand As New SqlCommand(sqlInsert, connection)  
Dim tvpParam As SqlParameter = _  
   insertCommand.Parameters.AddWithValue( _  
  "@tvpNewCategories", addedCategories)  
tvpParam.SqlDbType = SqlDbType.Structured  
tvpParam.TypeName = "dbo.CategoryTableType"  
  
```  
  
 È anche possibile usare qualsiasi oggetto derivato da <xref:System.Data.Common.DbDataReader> per trasmettere flussi di righe di dati a un parametro con valori di tabella, come illustrato in questo frammento:  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand(  
  "usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam =   
   insertCommand.Parameters.AddWithValue(  
   "@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
```vb  
' Configure the SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  dataReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
```  
  
## Passaggio di un parametro con valori di tabella a una stored procedure  
 In questo esempio viene illustrato come passare i dati di un parametro con valori di tabella a una stored procedure.  Il codice consente di estrarre le righe aggiunte in un nuovo oggetto <xref:System.Data.DataTable> tramite il metodo <xref:System.Data.DataTable.GetChanges%2A>.  Viene quindi definito un oggetto <xref:System.Data.SqlClient.SqlCommand>, impostando la proprietà <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> su <xref:System.Data.CommandType>.  L'oggetto <xref:System.Data.SqlClient.SqlParameter> viene popolato usando il metodo <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> e la proprietà <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> viene impostata su `Structured`.  Viene quindi eseguito <xref:System.Data.SqlClient.SqlCommand> usando il metodo <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>.  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
// Create a DataTable with the modified rows.  
DataTable addedCategories =  
  CategoriesDataTable.GetChanges(DataRowState.Added);  
  
// Configure the SqlCommand and SqlParameter.  
SqlCommand insertCommand = new SqlCommand(  
    "usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
  
// Execute the command.  
insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection object.  
Using connection  
   '  Create a DataTable with the modified rows.  
   Dim addedCategories As DataTable = _  
     CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Configure the SqlCommand and SqlParameter.  
   Dim insertCommand As New SqlCommand( _  
     "usp_InsertCategories", connection)  
   insertCommand.CommandType = CommandType.StoredProcedure  
   Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
     "@tvpNewCategories", addedCategories)  
   tvpParam.SqlDbType = SqlDbType.Structured  
  
   '  Execute the command.  
   insertCommand.ExecuteNonQuery()  
End Using  
```  
  
### Passaggio di un parametro con valori di tabella a un'istruzione SQL con parametri  
 Nell'esempio seguente viene illustrato come inserire i dati nella tabella dbo.Categories tramite un'istruzione INSERT con una sottoquery SELECT che dispone di un parametro con valori di tabella come origine dati.  Quando si passa un parametro con valori di tabella a un'istruzione SQL con parametri, è necessario specificare un nome di tipo per il parametro con valori di tabella usando la nuova proprietà <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> di un oggetto <xref:System.Data.SqlClient.SqlParameter>.  `TypeName` deve corrispondere al nome di un tipo compatibile creato in precedenza nel server.  Nel codice di questo esempio viene usata la proprietà `TypeName` per fare riferimento alla struttura di tipi definita in dbo.CategoryTableType.  
  
> [!NOTE]
>  Se si fornisce un valore per una colonna Identity in un parametro con valori di tabella, è necessario eseguire l'istruzione SET IDENTITY\_INSERT per la sessione.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
// Create a DataTable with the modified rows.  
DataTable addedCategories = CategoriesDataTable.GetChanges(  
    DataRowState.Added);  
  
// Define the INSERT-SELECT statement.  
string sqlInsert =   
    "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
    + " SELECT nc.CategoryID, nc.CategoryName"  
    + " FROM @tvpNewCategories AS nc;"  
  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(  
    sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
  
// Execute the command.  
insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
Using connection  
  ' Create a DataTable with the modified rows.  
  Dim addedCategories As DataTable = _  
    CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Define the INSERT-SELECT statement.  
  Dim sqlInsert As String = _  
  "INSERT INTO dbo.Categories (CategoryID, CategoryName)" _  
  & " SELECT nc.CategoryID, nc.CategoryName" _  
  & " FROM @tvpNewCategories AS nc;"  
  
  ' Configure the command and parameter.  
  Dim insertCommand As New SqlCommand(sqlInsert, connection)  
  Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
    "@tvpNewCategories", addedCategories)  
  tvpParam.SqlDbType = SqlDbType.Structured  
  tvpParam.TypeName = "dbo.CategoryTableType"  
  
  ' Execute the query  
  insertCommand.ExecuteNonQuery()  
End Using  
```  
  
## Trasmissione di flussi di righe con un oggetto DataReader  
 È anche possibile usare qualsiasi oggetto derivato da <xref:System.Data.Common.DbDataReader> per trasmettere flussi di righe di dati a un parametro con valori di tabella.  Nel frammento di codice seguente viene illustrato il recupero di dati da un database Oracle tramite un oggetto <xref:System.Data.OracleClient.OracleCommand> e un oggetto <xref:System.Data.OracleClient.OracleDataReader>.  Nel codice viene quindi configurato un oggetto <xref:System.Data.SqlClient.SqlCommand> per richiamare una stored procedure con un singolo parametro di input.  La proprietà <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> di <xref:System.Data.SqlClient.SqlParameter> è impostata su `Structured`.  <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> passa il set di risultati di `OracleDataReader` alla stored procedure come parametro con valori di tabella.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =   
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
' Retrieve data from Oracle.  
Dim selectCommand As New OracleCommand( _  
  "Select CategoryID, CategoryName FROM Categories;", _  
  oracleConnection)  
Dim oracleReader As OracleDataReader = _  
  selectCommand.ExecuteReader(CommandBehavior.CloseConnection)  
  
' Configure SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  oracleReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
' Execute the command.  
insertCommand.ExecuteNonQuery()  
```  
  
## Vedere anche  
 [Configurazione dei parametri e tipi di dati dei parametri](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [Comandi e parametri](../../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Parametri di DataAdapter](../../../../../docs/framework/data/adonet/dataadapter-parameters.md)   
 [Operazioni sui dati SQL Server in ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)