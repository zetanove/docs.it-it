---
title: "Aggiornamento dei dati in un&#39;origine dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 55c545e5-dcd5-4323-a5b9-3825c2157462
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Aggiornamento dei dati in un&#39;origine dati
Le istruzioni SQL che modificano i dati, ad esempio INSERT, UPDATE o DELETE, non restituiscono righe.  Analogamente, molte stored procedure eseguono un'operazione ma non restituiscono righe.  Per eseguire comandi che non restituiscono righe, creare un oggetto **Command** con il comando SQL appropriato, un oggetto **Connection** con tutti i **Parameters** necessari  Eseguire il comando con il metodo **ExecuteNonQuery** dell'oggetto **Command**.  
  
 Il metodo **ExecuteNonQuery** restituisce un valore intero che rappresenta il numero di righe interessate dall'istruzione o dalla stored procedure eseguita.  Se si eseguono più istruzioni, il valore restituito sarà la somma dei record interessati da ognuna delle istruzioni eseguite.  
  
## Esempio  
 Nell'esempio di codice seguente viene eseguita un'istruzione INSERT per inserire un record in un database usando **ExecuteNonQuery**.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
connection.Open()  
  
Dim queryString As String = "INSERT INTO Customers " & _  
  "(CustomerID, CompanyName) Values('NWIND', 'Northwind Traders')"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
Dim recordsAffected As Int32 = command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
connection.Open();  
  
string queryString = "INSERT INTO Customers " +  
  "(CustomerID, CompanyName) Values('NWIND', 'Northwind Traders')";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
Int32 recordsAffected = command.ExecuteNonQuery();  
```  
  
 Nell'esempio di codice seguente viene eseguita la stored procedure creata dal codice di esempio in [Esecuzione di operazioni nel catalogo](../../../../docs/framework/data/adonet/performing-catalog-operations.md).  La stored procedure non restituisce righe, quindi viene usato il metodo **ExecuteNonQuery**, ma riceve un parametro di input e restituisce un parametro di output e un valore restituito.  
  
 Per l'oggetto <xref:System.Data.OleDb.OleDbCommand>, il parametro **ReturnValue** deve essere aggiunto prima alla raccolta **Parameters**.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim command As SqlCommand = _  
   New SqlCommand("InsertCategory" , connection)  
command.CommandType = CommandType.StoredProcedure  
  
Dim parameter As SqlParameter = _  
 command.Parameters.Add("@RowCount", SqlDbType.Int)  
parameter.Direction = ParameterDirection.ReturnValue  
  
parameter = command.Parameters.Add( _  
  "@CategoryName", SqlDbType.NChar, 15)  
  
parameter = command.Parameters.Add("@Identity", SqlDbType.Int)  
parameter.Direction = ParameterDirection.Output  
  
command.Parameters("@CategoryName").Value = "New Category"  
command.ExecuteNonQuery()  
  
Dim categoryID As Int32 = CInt(command.Parameters("@Identity").Value)  
Dim rowCount As Int32 = CInt(command.Parameters("@RowCount").Value)   
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlCommand command = new SqlCommand("InsertCategory" , connection);  
command.CommandType = CommandType.StoredProcedure;  
  
SqlParameter parameter = command.Parameters.Add(  
  "@RowCount", SqlDbType.Int);  
parameter.Direction = ParameterDirection.ReturnValue;  
  
parameter = command.Parameters.Add(  
  "@CategoryName", SqlDbType.NChar, 15);  
  
parameter = command.Parameters.Add("@Identity", SqlDbType.Int);  
parameter.Direction = ParameterDirection.Output;  
  
command.Parameters["@CategoryName"].Value = "New Category";  
command.ExecuteNonQuery();  
  
Int32 categoryID = (Int32) command.Parameters["@Identity"].Value;  
Int32 rowCount = (Int32) command.Parameters["@RowCount"].Value;  
```  
  
## Vedere anche  
 [Utilizzo di oggetti Command per la modifica dei dati](../../../../docs/framework/data/adonet/using-commands-to-modify-data.md)   
 [Aggiornamenti di origini dati tramite DataAdapter](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)