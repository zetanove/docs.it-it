---
title: "Parametri di DataAdapter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Parametri di DataAdapter
<xref:System.Data.Common.DbDataAdapter> dispone di quattro proprietà che consentono di recuperare e aggiornare i dati dell'origine dati. La proprietà <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> restituisce i dati dall'origine dati, mentre le proprietà <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> e <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> vengono usate per gestire le modifiche nell'origine dati.  La proprietà `SelectCommand` deve essere impostata prima di chiamare il metodo `Fill` di `DataAdapter`.  È necessario impostare la proprietà `InsertCommand`, `UpdateCommand` o `DeleteCommand` prima di chiamare il metodo `Update` di `DataAdapter` a seconda delle modifiche apportate ai dati in <xref:System.Data.DataTable>,  Se ad esempio sono state aggiunte righe, è necessario impostare la proprietà `InsertCommand` prima di chiamare `Update`.  Quando `Update` elabora una riga inserita, aggiornata o eliminata, `DataAdapter` usa la rispettiva proprietà `Command` per l'operazione.  Le informazioni correnti sulla riga modificata vengono passate all'oggetto `Command` mediante la raccolta `Parameters`.  
  
 Quando si aggiorna una riga nell'origine dati, viene chiamata l'istruzione UPDATE che usa un identificatore univoco per identificare la riga nella tabella da aggiornare.  In genere, il valore dell'identificatore univoco corrisponde a quello del campo di una chiave primaria.  Nell'istruzione UPDATE vengono usati i parametri che contengono sia l'identificatore univoco che le colonne e i valori da aggiornare, come illustrato nell'istruzione Transact\-SQL seguente.  
  
```  
UPDATE Customers SET CompanyName = @CompanyName   
  WHERE CustomerID = @CustomerID  
```  
  
> [!NOTE]
>  La sintassi per i segnaposto dei parametri varia in base all'origine dati.  In questo esempio vengono mostrati i segnaposto per un'origine dati SQL Server.  Per i parametri <xref:System.Data.OleDb> e <xref:System.Data.Odbc> vengono usati come segnaposto i punti interrogativi \(?\).  
  
 In questo esempio di [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], il campo `CompanyName` viene aggiornato con il valore del parametro `@CompanyName` nella riga in cui `CustomerID` è uguale al valore del parametro `@CustomerID```.  Le informazioni della riga modificata vengono recuperate dai parametri mediante la proprietà <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A> dell'oggetto <xref:System.Data.SqlClient.SqlParameter>.  Di seguito sono riportati i parametri della precedente istruzione UPDATE di esempio.  Nel codice si presuppone che la variabile `adapter` rappresenti un oggetto <xref:System.Data.SqlClient.SqlDataAdapter> valido.  
  
```  
adapter.Parameters.Add( _  
  "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
Dim parameter As SqlParameter = _  
  adapter.UpdateCommand.Parameters.Add("@CustomerID", _  
  SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
```  
  
 Il metodo `Add` della raccolta `Parameters` accetta il nome del parametro, il tipo di dati, le dimensioni \(se applicabili al tipo\) e il nome dell'oggetto <xref:System.Data.Common.DbParameter.SourceColumn%2A> da `DataTable`.  Notare che la proprietà <xref:System.Data.Common.DbParameter.SourceVersion%2A> del parametro `@CustomerID` è impostata su `Original`.  Questo valore assicura che l'aggiornamento della riga esistente nell'origine dati venga eseguito se il valore della colonna o delle colonne identificative è stato cambiato nell'oggetto <xref:System.Data.DataRow> modificato.  In questo caso il valore `Original` della riga corrisponde al valore corrente nell'origine dati e il valore `Current` della riga contiene il valore aggiornato.  `SourceVersion` non è impostato per il parametro `@CompanyName`, pertanto verrà usato il valore di riga `Current` predefinito.  
  
> [!NOTE]
>  Per le operazioni `Fill` del `DataAdapter` e i metodi `Get` del `DataReader`, il tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] viene inferito dal tipo restituito dal provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  I tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] inferiti e metodi delle funzioni di accesso per i tipi di dati Microsoft SQL Server, OLE DB e ODBC sono descritti in [Mapping dei tipi di dati in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md).  
  
## Parameter.SourceColumn e Parameter.SourceVersion  
 È possibile passare `SourceColumn` e `SourceVersion` come argomenti del costruttore `Parameter` o impostarli come proprietà di un oggetto `Parameter` esistente.  `SourceColumn` è il nome dell'oggetto <xref:System.Data.DataColumn> derivato da <xref:System.Data.DataRow> in cui viene recuperato il valore di `Parameter`.  `SourceVersion` specifica la versione di `DataRow` usata da `DataAdapter` per recuperare il valore.  
  
 Nella tabella seguente sono elencati i valori di enumerazione <xref:System.Data.DataRowVersion> disponibili per l'uso con `SourceVersion`.  
  
|Enumerazione DataRowVersion|Descrizione|  
|---------------------------------|-----------------|  
|`Current`|Il parametro usa il valore corrente della colonna.  Questa è l'impostazione predefinita.|  
|`Default`|Il parametro usa il valore `DefaultValue` della colonna.|  
|`Original`|Il parametro usa il valore originale della colonna.|  
|`Proposed`|Il parametro usa un valore proposto.|  
  
 Nell'esempio di codice `SqlClient` della sezione successiva viene definito un parametro per un oggetto <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> in cui la colonna `CustomerID` viene usata come `SourceColumn` per due parametri: `@CustomerID` \(`SET CustomerID = @CustomerID`\) e `@OldCustomerID` \(`WHERE CustomerID = @OldCustomerID`\).  Il parametro `@CustomerID` viene usato per aggiornare la colonna **CustomerID** in base al valore corrente di `DataRow`.  Di conseguenza, viene usato `SourceColumn` `CustomerID` in cui il valore di `SourceVersion` è uguale a `Current`.  Il parametro *@OldCustomerID* viene usato per identificare la riga corrente nell'origine dati.  Poiché il valore della colonna corrispondente viene individuato nella versione `Original` della riga, verrà usato lo stesso oggetto `SourceColumn` \(`CustomerID`\) con `SourceVersion` `Original`.  
  
## Uso di parametri SqlClient  
 Nell'esempio seguente viene illustrato come creare un oggetto <xref:System.Data.SqlClient.SqlDataAdapter> e impostare <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> su <xref:System.Data.MissingSchemaAction> per recuperare informazioni aggiuntive sullo schema dal database.  Vengono impostate le proprietà <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> e <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> e i relativi oggetti <xref:System.Data.SqlClient.SqlParameter> corrispondenti vengono aggiunti alla raccolta <xref:System.Data.SqlClient.SqlCommand.Parameters%2A>.  Il metodo restituisce un oggetto `SqlDataAdapter`.  
  
 [!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/CS/source.cs#1)]
 [!code-vb[Classic WebData SqlDataAdapter.SqlDataAdapter Example#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/Classic WebData SqlDataAdapter.SqlDataAdapter Example/VB/source.vb#1)]  
  
## Segnaposti di parametri OleDb  
 Per gli oggetti <xref:System.Data.OleDb.OleDbDataAdapter> e <xref:System.Data.Odbc.OdbcDataAdapter>, è necessario usare il punto interrogativo \(?\) come segnaposto per identificare i parametri.  
  
```vb  
Dim selectSQL As String = _  
  "SELECT CustomerID, CompanyName FROM Customers " & _  
  "WHERE CountryRegion = ? AND City = ?"  
Dim insertSQL AS String = _  
  "INSERT INTO Customers (CustomerID, CompanyName) VALUES (?, ?)"  
Dim updateSQL AS String = _  
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " & _  
  WHERE CustomerID = ?"  
Dim deleteSQL As String = "DELETE FROM Customers WHERE CustomerID = ?"  
```  
  
```csharp  
string selectSQL =   
  "SELECT CustomerID, CompanyName FROM Customers " +  
  "WHERE CountryRegion = ? AND City = ?";  
string insertSQL =   
  "INSERT INTO Customers (CustomerID, CompanyName) " +  
  "VALUES (?, ?)";  
string updateSQL =   
  "UPDATE Customers SET CustomerID = ?, CompanyName = ? " +  
  "WHERE CustomerID = ? ";  
string deleteSQL = "DELETE FROM Customers WHERE CustomerID = ?";  
```  
  
 Le istruzioni delle query con parametri definiscono i parametri di input e di output che è necessario creare.  Per creare un parametro, usare il metodo `Parameters.Add` o il costruttore `Parameter` per specificare il nome della colonna, il tipo di dati e le dimensioni.  Per tipi di dati intrinseci, ad esempio `Integer`, non è necessario includere le dimensioni oppure è possibile specificare quelle predefinite.  
  
 Nell'esempio di codice seguente vengono creati i parametri per un'istruzione SQL e viene quindi compilato un `DataSet`.  
  
## Esempio di OleDb  
  
```vb  
' Assumes that connection is a valid OleDbConnection object.  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter   
  
Dim selectCMD AS OleDbCommand = New OleDbCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add parameters and set values.  
selectCMD.Parameters.Add( _  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add( _  
  "@City", OleDbType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OleDbConnection object.  
OleDbDataAdapter adapter = new OleDbDataAdapter();  
  
OleDbCommand selectCMD = new OleDbCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
// Add parameters and set values.  
selectCMD.Parameters.Add(  
  "@CountryRegion", OleDbType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add(  
  "@City", OleDbType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
## Parametri Odbc  
  
```vb  
' Assumes that connection is a valid OdbcConnection object.  
Dim adapter As OdbcDataAdapter = New OdbcDataAdapter  
  
Dim selectCMD AS OdbcCommand = New OdbcCommand(selectSQL, connection)  
adapter.SelectCommand = selectCMD  
  
' Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK"  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London"  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
  
```  
  
```csharp  
// Assumes that connection is a valid OdbcConnection object.  
OdbcDataAdapter adapter = new OdbcDataAdapter();  
  
OdbcCommand selectCMD = new OdbcCommand(selectSQL, connection);  
adapter.SelectCommand = selectCMD;  
  
//Add Parameters and set values.  
selectCMD.Parameters.Add("@CountryRegion", OdbcType.VarChar, 15).Value = "UK";  
selectCMD.Parameters.Add("@City", OdbcType.VarChar, 15).Value = "London";  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  Se non viene specificato un nome, al parametro viene assegnato il nome predefinito incrementale Parameter*N* *,* che inizia con "Parameter1".  Si consiglia di evitare la convenzione di denominazione Parameter*N* quando si specifica il nome del parametro, in quanto il nome indicato può entrare in conflitto con un nome predefinito esistente in `ParameterCollection`.  Se il nome fornito è già presente, viene generata un'eccezione.  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Aggiornamenti di origini dati tramite DataAdapter](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Modifica di dati con le stored procedure](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [Mapping dei tipi di dati in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)