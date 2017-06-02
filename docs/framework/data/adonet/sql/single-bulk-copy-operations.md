---
title: "Esecuzione di singole operazioni di copia di massa | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Esecuzione di singole operazioni di copia di massa
L'approccio più semplice per eseguire un'operazione di copia di massa in SQL Server consiste nell'eseguire una singola operazione in un database.  Per impostazione predefinita, un'operazione di copia di massa viene eseguita come operazione isolata: l'operazione di copia avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback.  
  
> [!NOTE]
>  Per eseguire il rollback di una parte o dell'intera copia di massa quando si verifica un errore, è possibile usare una transazione gestita di <xref:System.Data.SqlClient.SqlBulkCopy> oppure eseguire la copia di massa in una transazione esistente.  **SqlBulkCopy** funzionerà anche con <xref:System.Transactions> se la connessione è inserita, in modo implicito o esplicito, nell'elenco di una transazione **System.Transactions**.  
>   
>  Per altre informazioni, vedere [Transazioni e operazioni di copia di massa](../../../../../docs/framework/data/adonet/sql/transaction-and-bulk-copy-operations.md).  
  
 In generale, i passaggi per eseguire un'operazione di copia di massa sono i seguenti:  
  
1.  Connettersi al server di origine per recuperare i dati da copiare.  I dati possono provenire anche da altre origini, se possono essere recuperati da un oggetto<xref:System.Data.IDataReader> o <xref:System.Data.DataTable>.  
  
2.  Connettersi al server di destinazione \(la connessione può essere eseguita automaticamente anche da **SqlBulkCopy**\).  
  
3.  Creare un oggetto <xref:System.Data.SqlClient.SqlBulkCopy>, impostando tutte le proprietà necessarie.  
  
4.  Impostare la proprietà **DestinationTableName** per indicare la tabella di destinazione per l'operazione di inserimento di massa.  
  
5.  Chiamare uno dei metodi **WriteToServer**.  
  
6.  Inoltre, è possibile aggiornare le proprietà e, se necessario, chiamare nuovamente **WriteToServer**.  
  
7.  Chiamare <xref:System.Data.SqlClient.SqlBulkCopy.Close%2A> o eseguire il wrapping delle operazioni di copia di massa all'interno di un'istruzione `Using`.  
  
> [!CAUTION]
>  È consigliabile assicurare che la corrispondenza tra i tipi di dati della colonna di origine e quelli di destinazione.  Se i tipi di dati non corrispondono, **SqlBulkCopy** tenterà di convertire ogni valore di origine nel tipo di dati di destinazione usando le regole della proprietà <xref:System.Data.SqlClient.SqlParameter.Value%2A> Le conversioni possono influenzare le prestazioni e possono provocare errori imprevisti.  Ad esempio, non è sempre possibile convertire un tipo di dati `Double` in `Decimal`.  
  
## Esempio  
 Nell'applicazione console riportata di seguito viene illustrato come caricare i dati usando la classe <xref:System.Data.SqlClient.SqlBulkCopy>.  In questo esempio, viene usato un oggetto <xref:System.Data.SqlClient.SqlDataReader> per copiare i dati dalla tabella **Production.Product** del database **AdventureWorks** di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] in una tabella simile dello stesso database.  
  
> [!IMPORTANT]
>  Questo esempio non verrà eseguito a meno che le tabelle di lavoro non siano state create come descritto in [Installazione dell'esempio relativo alla copia di massa](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md).  Il codice viene fornito solo per illustrare la sintassi relativa all'utilizzo di **SqlBulkCopy**.  Se la tabella di origine e quella di destinazione risiedono nella stessa istanza di SQL Server, per copiare i dati è più semplice e rapido usare un'istruzione `INSERT … SELECT` Transact\-SQL.  
  
 [!code-csharp[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/CS/source.cs#1)]
 [!code-vb[DataWorks BulkCopy.Single#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks BulkCopy.Single/VB/source.vb#1)]  
  
## Esecuzione di un'operazione di copia di massa con Transact\-SQL e la classe Command  
 Nell'esempio seguente viene illustrato come usare il metodo <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> per eseguire l'istruzione BULK INSERT.  
  
> [!NOTE]
>  Il percorso di file per l'origine dati è relativo al server.  Per la corretta esecuzione dell'operazione di copia di massa, è necessario che il processo server abbia accesso a tale percorso.  
  
```vb  
Using connection As SqlConnection = New SqlConnection(connectionString)  
Dim queryString As String = _  
    "BULK INSERT Northwind.dbo.[Order Details] FROM " & _  
    "'f:\mydata\data.tbl' WITH (FORMATFILE='f:\mydata\data.fmt' )"  
connection.Open()  
SqlCommand command = New SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery()  
End Using  
```  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## Vedere anche  
 [Operazioni di copia di massa in SQL Server](../../../../../docs/framework/data/adonet/sql/bulk-copy-operations-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)