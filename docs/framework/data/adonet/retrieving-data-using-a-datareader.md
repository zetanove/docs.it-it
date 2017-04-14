---
title: "Recupero di dati mediante un DataReader | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Recupero di dati mediante un DataReader
Per recuperare dati mediante un **DataReader**, è necessario creare un'istanza dell'oggetto **Command**, quindi creare un **DataReader** chiamando **Command.ExecuteReader** per recuperare righe da un'origine dati.  Nell'esempio seguente è illustrato l'uso di un **DataReader** in cui `reader` rappresenta un DataReader valido e `command` rappresenta un oggetto Command valido.  
  
```  
reader = command.ExecuteReader();  
```  
  
 Il metodo **Read** dell'oggetto **DataReader** viene usato per ottenere una riga dai risultati della query.  È possibile accedere a ogni colonna della riga restituita passando il nome o il riferimento ordinale della colonna al **DataReader**.  Per migliorare le prestazioni, tuttavia, **DataReader** fornisce una serie di metodi che consentono di accedere ai valori delle colonne nei tipi di dati nativi, quali **GetDateTime**, **GetDouble**, **GetGuid**, **GetInt32** e così via.  Per un elenco dei metodi delle funzioni di accesso tipizzate per **DataReader** specifici del provider di dati, vedere <xref:System.Data.OleDb.OleDbDataReader> e <xref:System.Data.SqlClient.SqlDataReader>.  L'utilizzo di metodi di funzioni di accesso tipizzate, quando si conosce il tipo di dati sottostante, riduce il numero di conversioni dei tipi necessari al momento del recupero del valore della colonna.  
  
> [!NOTE]
>  Nella versione di .NET Framework per Windows Server 2003 è inclusa una proprietà aggiuntiva per **DataReader**, **HasRows**, con cui è possibile determinare se **DataReader** ha restituito risultati prima di leggerli.  
  
 Nell'esempio di codice seguente viene scorso un oggetto **DataReader** e vengono restituite due colonne da ogni riga.  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
 **DataReader** fornisce un flusso di dati non archiviati nel buffer che consente alla logica procedurale di elaborare sequenzialmente i risultati provenienti da un'origine dati.  L'utilizzo di **DataReader** è consigliabile quando si recuperano grandi quantità di dati in quanto i dati non sono memorizzati nella cache.  
  
## Chiusura dell'oggetto DataReader  
 È necessario chiamare sempre il metodo **Close** una volta terminato l'uso dell'oggetto **DataReader**.  
  
 I parametri di output o i valori restituiti presenti nell'oggetto **Command** non saranno disponibili fino a quando l'oggetto **DataReader** non viene chiuso.  
  
 Notare che quando è aperto un oggetto **DataReader**, l'oggetto **Connection** viene usato esclusivamente da quell'oggetto **DataReader**.  Non sarà possibile eseguire alcun comando per l'oggetto **Connection**, né creare un altro **DataReader** fino a quando il **DataReader** originale non viene chiuso.  
  
> [!NOTE]
>  Non chiamare **Close** o **Dispose** su un oggetto **Connection**, un oggetto **DataReader** o su qualsiasi altro oggetto gestito nel metodo **Finalize** della classe.  Nei finalizzatori rilasciare solo le risorse non gestite che la classe controlla direttamente.  Se nella classe non sono presenti risorse non gestite, non includere un metodo **Finalize** nella definizione della classe.  Per altre informazioni, vedere [Garbage Collection](../../../../docs/standard/garbage-collection/index.md).  
  
## Recupero di più set di risultati tramite NextResult  
 Se vengono restituiti più set di risultati, l'oggetto **DataReader** fornisce il metodo **NextResult** per scorrere in modo sequenziale i set di risultati.  Nell'esempio seguente viene illustrata l'elaborazione dei risultati di due dichiarazioni SELECT da parte del tipo <xref:System.Data.SqlClient.SqlDataReader> usando il metodo <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A>.  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## Recupero di informazioni sullo schema dall'oggetto DataReader  
 Mentre un oggetto **DataReader** è aperto, è possibile recuperare le informazioni sullo schema relative al set di risultati corrente usando il metodo **GetSchemaTable**.  Il metodo **GetSchemaTable** restituisce un oggetto <xref:System.Data.DataTable> compilato con righe e colonne contenenti le informazioni sullo schema del set di risultati corrente.  L'oggetto **DataTable** contiene una riga per ogni colonna del set di risultati.  Ogni colonna della riga nella tabella dello schema è associata a una proprietà della colonna restituita nel set di risultati, in cui **ColumnName** è il nome della proprietà e il valore della colonna è il valore della proprietà.  Nell'esempio di codice seguente vengono rilasciate le informazioni sullo schema per l'oggetto **DataReader**.  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## Utilizzo dei capitoli OLE DB  
 I rowset gerarchici, o capitoli \(tipo OLE DB **DBTYPE\_HCHAPTER**, tipo ADO **adChapter**\), possono essere recuperati usando <xref:System.Data.OleDb.OleDbDataReader>.  Quando una query che include un capitolo viene restituita come un **DataReader**, il capitolo viene restituito come colonna del **DataReader** e viene esposto come un oggetto **DataReader**.  
  
 È possibile inoltre usare il **DataSet** di ADO.NET per rappresentare rowset gerarchici usando relazioni padre\-figlio tra le tabelle.  Per altre informazioni, vedere [DataSet, DataTable e DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md).  
  
 Nell'esempio di codice seguente viene usato il provider MSDataShape per generare una colonna del capitolo contenente gli ordini per ogni cliente presente in un elenco di clienti.  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")  
  
Dim custCMD As OleDbCommand = New OleDbCommand( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
connection.Open()  
  
Dim custReader As OleDbDataReader = custCMD.ExecuteReader()  
Dim orderReader As OleDbDataReader  
  
Do While custReader.Read()  
  Console.WriteLine("Orders for " & custReader.GetString(1))   
  ' custReader.GetString(1) = CompanyName  
  
  orderReader = custReader.GetValue(2)  
  ' custReader.GetValue(2) = Orders chapter as DataReader  
  
  Do While orderReader.Read()  
    Console.WriteLine(vbTab & orderReader.GetInt32(1))  
    ' orderReader.GetInt32(1) = OrderID  
  Loop  
  orderReader.Close()  
Loop  
' Make sure to always close readers and connections.  
custReader.Close()  
End Using  
```  
  
```csharp  
Using (OleDbConnection connection = new OleDbConnection(  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"));  
{  
OleDbCommand custCMD = new OleDbCommand(  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
connection.Open();  
  
OleDbDataReader custReader = custCMD.ExecuteReader();  
OleDbDataReader orderReader;  
  
while (custReader.Read())  
{  
  Console.WriteLine("Orders for " + custReader.GetString(1));   
  // custReader.GetString(1) = CompanyName  
  
  orderReader = (OleDbDataReader)custReader.GetValue(2);        
  // custReader.GetValue(2) = Orders chapter as DataReader  
  
  while (orderReader.Read())  
    Console.WriteLine("\t" + orderReader.GetInt32(1));          
    // orderReader.GetInt32(1) = OrderID  
  orderReader.Close();  
}  
// Make sure to always close readers and connections.  
custReader.Close();  
}  
```  
  
## Restituzione di risultati con i REF CURSOR Oracle  
 Con il provider di dati .NET Framework per Oracle è possibile usare i REF CURSOR Oracle per la restituzione del risultato di una query.  I REF CURSOR Oracle vengono restituiti come <xref:System.Data.OracleClient.OracleDataReader>.  
  
 È possibile recuperare un oggetto **OracleDataReader** che rappresenta un REF CURSOR Oracle usando il metodo <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> ed è possibile specificare un <xref:System.Data.OracleClient.OracleCommand> che restituisca uno o più REF CURSOR Oracle come **SelectCommand** per un <xref:System.Data.OracleClient.OracleDataAdapter> usato per compilare un <xref:System.Data.DataSet>.  
  
 Per accedere a un REF CURSOR restituito da un'origine dati Oracle, creare un **OracleCommand** per la query e aggiungere un parametro di output che fa riferimento al REF CURSOR alla raccolta **Parameters** di **OracleCommand**.  È necessario che il nome del parametro corrisponda al nome del parametro REF CURSOR della query.  Impostare il tipo di parametro su **OracleType.Cursor**.  Il metodo **ExecuteReader** di **OracleCommand** restituirà un **OracleDataReader** per il REF CURSOR.  
  
 Se **OracleCommand** restituisce più REF CURSOR, aggiungere più parametri di output.  Per accedere ai diversi REF CURSOR, chiamare il metodo **OracleCommand.ExecuteReader**.  La chiamata a **ExecuteReader** restituirà un **OracleDataReader** che fa riferimento al primo REF CURSOR.  Sarà quindi possibile chiamare il metodo **OracleDataReader.NextResult** per accedere ai REF CURSOR successivi.  Sebbene la corrispondenza tra i parametri della raccolta **OracleCommand.Parameters** e i parametri di output di REF CURSOR avvenga per nome, **OracleDataReader** accederà ai parametri nell'ordine in cui questi sono stati aggiunti alla raccolta **Parameters**.  
  
 Si considerino ad esempio il package e il corpo package Oracle seguenti.  
  
```  
CREATE OR REPLACE PACKAGE CURSPKG AS   
  TYPE T_CURSOR IS REF CURSOR;   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR);   
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR)   
  IS   
  BEGIN   
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;   
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;   
  END OPEN_TWO_CURSORS;   
END CURSPKG;   
```  
  
 Con il codice seguente viene creato un oggetto **OracleCommand** che restituisce i REF CURSOR dal package Oracle precedente tramite l'aggiunta di due parametri di tipo **OracleType.Cursor** alla raccolta **Parameters**.  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 Il codice seguente restituisce il risultato del comando precedente tramite i metodi **Read** e **NextResult** di **OracleDataReader**.  I parametri REF CURSOR vengono restituiti in ordine.  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 Nell'esempio seguente viene usato il comando precedente per compilare un **DataSet** con i risultati del package Oracle.  
  
> [!NOTE]
>  Per evitare il verificarsi di **OverflowException**, è consigliabile gestire le conversioni dei valori di tipo NUMBER Oracle in un tipo .NET Framework valido prima di archiviare i valori in un **DataRow**.  Per determinare se si è verificata una **OverflowException**, è possibile usare l'evento **FillError**.  Per altre informazioni sull'evento **FillError**, vedere [Gestione degli eventi di DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md).  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```  
  
## Vedere anche  
 [Working with DataReaders](http://msdn.microsoft.com/it-it/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Recupero di informazioni sullo schema di database](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)