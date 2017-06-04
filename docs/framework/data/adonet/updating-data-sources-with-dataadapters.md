---
title: "Aggiornamenti di origini dati tramite DataAdapter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Aggiornamenti di origini dati tramite DataAdapter
Il metodo `Update` di <xref:System.Data.Common.DataAdapter> viene chiamato per applicare le modifiche apportate a un oggetto <xref:System.Data.DataSet> nell'origine dati.  Il metodo `Update`, analogamente al metodo `Fill`, accetta come argomenti un'istanza di un oggetto `DataSet` e un oggetto <xref:System.Data.DataTable> o nome di `DataTable` facoltativi.  L'istanza di `DataSet` rappresenta l'oggetto `DataSet` contenente le modifiche che sono state apportate e l'oggetto `DataTable` identifica la tabella da cui recuperare le modifiche.  Se non viene specificato nessun oggetto `DataTable`, verrà usato il primo oggetto `DataTable` di `DataSet`.  
  
 Quando si chiama il metodo `Update`, `DataAdapter` analizza le modifiche apportate ed esegue il comando appropriato \(INSERT, UPDATE o DELETE\).  Quando rileva una modifica a un oggetto <xref:System.Data.DataRow>, `DataAdapter` elabora la modifica usando <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> o <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A>.  In questo modo è possibile ottimizzare le prestazioni dell'applicazione ADO.NET specificando la sintassi del comando in fase di progettazione e, dove possibile, mediante stored procedure.  È necessario impostare in modo esplicito i comandi prima di chiamare `Update`.  Se `Update` viene chiamato e non esiste il comando appropriato per un determinato aggiornamento, ad esempio nessun `DeleteCommand` per le righe cancellate, viene generata un'eccezione.  
  
> [!NOTE]
>  Se si usano stored procedure SQL Server per modificare o eliminare dati tramite `DataAdapter`, assicurarsi di non usare SET NOCOUNT ON nella definizione della stored procedure.  Con tale comando il totale restituito delle righe interessate è pari a zero e tale situazione viene interpretata da `DataAdapter` come un conflitto di concorrenza.  In questo caso verrà generata un'eccezione <xref:System.Data.DBConcurrencyException>.  
  
 È possibile usare i parametri Command per specificare i valori di input e di output di un'istruzione SQL o una stored procedure per ogni riga modificata in un `DataSet`.  Per altre informazioni, vedere [Parametri di DataAdapter](../../../../docs/framework/data/adonet/dataadapter-parameters.md).  
  
> [!NOTE]
>  È importante capire la differenza tra eliminazione di una riga in un oggetto <xref:System.Data.DataTable> e rimozione della riga.  Quando si chiama il metodo `Remove` o `RemoveAt`, la riga viene rimossa immediatamente.  Eventuali righe corrispondenti nell'origine dati di back\-end non saranno interessate se si passa `DataTable` o `DataSet` a un oggetto `DataAdapter` e si chiama `Update`.  Quando si usa il metodo `Delete`, la riga rimane in `DataTable` e viene contrassegnato per l'eliminazione.  Se quindi si passa `DataTable` o `DataSet` a un oggetto `DataAdapter` e si chiama `Update`, la riga corrispondente nell'origine dati di back\-end verrà eliminata.  
  
 Se `DataTable` esegue il mapping o viene generato da una singola tabella di database, è possibile usare l'oggetto <xref:System.Data.Common.DbCommandBuilder> per generare automaticamente gli oggetti `DeleteCommand`, `InsertCommand` e `UpdateCommand` di `DataAdapter`.  Per altre informazioni, vedere [Generazione di comandi con CommandBuilder](../../../../docs/framework/data/adonet/generating-commands-with-commandbuilders.md).  
  
## Uso di UpdatedRowSource per eseguire il mapping di valori su un oggetto DataSet  
 Per controllare come viene eseguito il mapping dei valori restituiti dall'origine dati su un oggetto `DataTable` in seguito a una chiamata al metodo Update di un oggetto `DataAdapter`, è possibile usare la proprietà <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> dell'oggetto <xref:System.Data.Common.DbCommand>.  Impostando la proprietà `UpdatedRowSource` su uno dei valori di enumerazione <xref:System.Data.UpdateRowSource>, è possibile controllare se i parametri restituiti dai comandi di `DataAdapter` vengono ignorati o applicati alla riga modificata in `DataSet`.  È possibile inoltre specificare se la prima riga restituita \(se esiste\) viene applicata alla riga modificata in `DataTable`.  
  
 La tabella seguente descrive i diversi valori dell'enumerazione `UpdateRowSource` e viene illustrato il modo in cui influenzano il comportamento di un comando usato con un `DataAdapter`.  
  
|Enumerazione UpdatedRowSource|Descrizione|  
|-----------------------------------|-----------------|  
|<xref:System.Data.UpdateRowSource>|È possibile eseguire il mapping dei parametri di output e della prima riga di un set di risultati restituiti sulla riga modificata nel `DataSet`.|  
|<xref:System.Data.UpdateRowSource>|È possibile eseguire il mapping sulla riga modificata nel `DataSet` solo dei dati nella prima riga di un set di risultati restituiti.|  
|<xref:System.Data.UpdateRowSource>|Tutti i parametri di output, o righe, di un set di risultati restituiti vengono ignorati.|  
|<xref:System.Data.UpdateRowSource>|È possibile eseguire il mapping sulla riga modificata nel `DataSet` solo dei parametri di output.|  
  
 Il metodo `Update` applica le modifiche nell'origine dati, ma è possibile che altri client abbiano modificato i dati nell'origine dati dall'ultima volta che è stato compilato il `DataSet`.  Per aggiornare `DataSet` con i dati correnti, usare i metodi `DataAdapter` e `Fill`.  Le nuove righe verranno aggiunte alla tabella e le informazioni aggiornate verranno inserite nelle righe esistenti.  Quando si esegue il metodo `Fill`, verrà determinato se aggiungere una nuova riga o aggiornare una riga esistente esaminando i valori delle chiavi primarie delle righe del `DataSet` e delle righe restituite da `SelectCommand`.  Se il metodo `Fill` rileva un valore di chiave primaria di una riga del `DataSet` che corrisponde al valore di chiave primaria di una riga presente nei risultati restituiti da `SelectCommand`, la riga esistente verrà aggiornata con le informazioni presenti nella riga restituita da `SelectCommand` e la proprietà <xref:System.Data.DataRow.RowState%2A> della riga esistente verrà impostata su `Unchanged`.  Se una riga restituita da `SelectCommand` presenta un valore di chiave primaria che non corrisponde ad alcuno dei valori di chiave primaria delle righe del `DataSet`, il metodo `Fill` aggiungerà una nuova riga con il valore relativo a `RowState` impostato su `Unchanged`.  
  
> [!NOTE]
>  Se `SelectCommand` restituisce i risultati di un OUTER JOIN, il `DataAdapter` non imposterà un valore `PrimaryKey` per l'oggetto `DataTable` risultante.  Per assicurarsi che le righe duplicate vengano risolte correttamente, sarà necessario definire `PrimaryKey` in modo autonomo.  Per altre informazioni, vedere [Definizione di chiavi primarie](../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md).  
  
 Per gestire le eccezioni che possono verificarsi quando si chiama il metodo `Update`, è possibile usare l'evento `RowUpdated` per rispondere agli errori di aggiornamento delle righe nel momento in cui si verificano \(vedere [Gestione degli eventi di DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)\), oppure impostare `DataAdapter.ContinueUpdateOnError` su `true` prima di chiamare il metodo `Update` e rispondere alle informazioni sugli errori archiviate nella proprietà `RowError` di una determinata riga al termine dell'aggiornamento \(vedere [Informazioni sugli errori delle righe](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-error-information.md)\).  
  
 **Nota** Se si chiama `AcceptChanges` sull'oggetto `DataSet`, `DataTable` o `DataRow`, tutti i valori `Original` relativi a un oggetto `DataRow` verranno sovrascritti con i valori `Current` relativi a `DataRow`.  Se i valori di campo che identificano la riga come univoca sono stati modificati, dopo la chiamata a `AcceptChanges` i valori `Original` non corrisponderanno più ai valori dell'origine dati.  `AcceptChanges` viene chiamato automaticamente per ogni riga durante una chiamata al metodo Update di un oggetto `DataAdapter`.  Per mantenere i valori originali durante una chiamata al metodo Update, impostare prima la proprietà `AcceptChangesDuringUpdate` di `DataAdapter` su false oppure creare un gestore eventi per l'evento `RowUpdated` e impostare <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> su <xref:System.Data.UpdateStatus>.  Per altre informazioni, vedere [Unione del contenuto di un DataSet](../../../../docs/framework/data/adonet/dataset-datatable-dataview/merging-dataset-contents.md) e [Gestione degli eventi di DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md).  
  
## Esempio  
 Negli esempi seguenti viene illustrato come aggiornare le righe modificate impostando in modo esplicito `UpdateCommand` di `DataAdapter` e chiamando il relativo metodo `Update` .  Notare che il parametro specificato nella clausola WHERE dell'istruzione UPDATE viene impostato in modo da usare il valore `Original` di `SourceColumn`.  Questo è importante in quanto è possibile che il valore `Current` sia stato modificato e che non corrisponda più al valore nell'origine dati.  Il valore `Original` è il valore che è stato usato per compilare `DataTable` dall'origine dati.  
  
 [!code-csharp[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/VB/source.vb#1)]  
  
## Colonne AutoIncrement  
 Se nelle tabelle dell'origine dati sono presenti colonne con incremento automatico, è possibile riempire le colonne nel `DataSet` restituendo il valore dell'incremento automatico come un parametro di output di una stored procedure ed eseguendone il mapping su una colonna della tabella, restituendo il valore dell'incremento automatico nella prima riga di un set di risultati restituito da una stored procedure o un'istruzione SQL oppure usando l'evento `RowUpdated` di `DataAdapter` per eseguire un'ulteriore istruzione SELECT.  Per altre informazioni e un esempio, vedere [Recupero dei valori di identità o del contatore](../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md).  
  
## Ordine di Insert, Update e Delete  
 In molti casi l'ordine in cui le modifiche apportate mediante `DataSet` vengono inviate all'origine dati è importante.  Se ad esempio il valore di una chiave primaria relativo a una riga esistente viene aggiornato ed è stata aggiunta una nuova riga con il nuovo valore della chiave primaria come chiave esterna, è importante elaborare l'aggiornamento prima di effettuare l'inserimento.  
  
 È possibile usare il metodo `Select` di `DataTable` per restituire una matrice `DataRow` che faccia riferimento solo a righe con un particolare `RowState`.  È quindi possibile passare la matrice `DataRow` restituita al metodo `Update` di `DataAdapter` per elaborare le righe modificate.  Se si specifica un subset di righe da aggiornare, è possibile controllare l'ordine in cui vengono elaborati gli inserimenti, gli aggiornamenti e le eliminazioni.  
  
## Esempio  
 Il codice seguente, ad esempio, assicura che vengano elaborate prima le righe cancellate della tabella, quindi le righe aggiornate e infine le righe inserite.  
  
```vb  
Dim table As DataTable = dataSet.Tables("Customers")  
  
' First process deletes.  
dataSet.Update(table.Select(Nothing, Nothing, _  
  DataViewRowState.Deleted))  
  
' Next process updates.  
adapter.Update(table.Select(Nothing, Nothing, _  
  DataViewRowState.ModifiedCurrent))  
  
' Finally, process inserts.  
dataAdapater.Update(table.Select(Nothing, Nothing, _  
  DataViewRowState.Added))  
```  
  
```csharp  
DataTable table = dataSet.Tables["Customers"];  
  
// First process deletes.  
adapter.Update(table.Select(null, null, DataViewRowState.Deleted));  
  
// Next process updates.  
adapter.Update(table.Select(null, null,   
  DataViewRowState.ModifiedCurrent));  
  
// Finally, process inserts.  
adapter.Update(table.Select(null, null, DataViewRowState.Added));  
```  
  
## Uso di un oggetto DataAdapter per recuperare e aggiornare dati  
 È possibile usare un oggetto DataAdapter per recuperare e aggiornare i dati.  
  
-   Nell'esempio viene usato DataAdapter.AcceptChangesDuringFill per clonare i dati nel database.  Se la proprietà è impostata su false, AcceptChanges non viene chiamato quando viene compilata la tabella e le righe appena aggiunte sono considerate righe inserite.  Di conseguenza, nell'esempio queste righe vengono usate per inserire nuove righe nel database.  
  
-   Negli esempi viene usato DataAdapter.TableMappings per definire il mapping tra la tabella di origine e DataTable.  
  
-   Nell'esempio viene usato DataAdapter.FillLoadOption per determinare come l'adattatore riempie l'elemento DataTable dall'elemento DbDataReader.  Quando si crea un oggetto DataTable, è possibile scrivere i dati solo da un database alla versione corrente o alla versione originale impostando la proprietà come LoadOption.Upsert o LoadOption.PreserveChanges.  
  
-   Viene inoltre aggiornata la tabella usando DbDataAdapter.UpdateBatchSize per eseguire operazioni batch.  
  
 Prima di compilare ed eseguire l'esempio, è necessario creare il database di esempio:  
  
```  
USE [master]  
GO  
  
CREATE DATABASE [MySchool]   
  
GO  
  
USE [MySchool]  
GO  
  
SET ANSI_NULLS ON  
GO  
SET QUOTED_IDENTIFIER ON  
GO  
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,  
[Year] [smallint] NOT NULL,  
[Title] [nvarchar](100) NOT NULL,  
[Credits] [int] NOT NULL,  
[DepartmentID] [int] NOT NULL,  
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED   
(  
[CourseID] ASC,  
[Year] ASC  
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]  
  
GO  
  
SET ANSI_NULLS ON  
GO  
SET QUOTED_IDENTIFIER ON  
GO  
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,  
[Name] [nvarchar](50) NOT NULL,  
[Budget] [money] NOT NULL,  
[StartDate] [datetime] NOT NULL,  
[Administrator] [int] NULL,  
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED   
(  
[DepartmentID] ASC  
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]  
  
GO  
  
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)  
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)  
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)  
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)  
  
SET IDENTITY_INSERT [dbo].[Department] ON   
  
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)  
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)  
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)  
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)  
SET IDENTITY_INSERT [dbo].[Department] OFF  
  
ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])  
REFERENCES [dbo].[Department] ([DepartmentID])  
GO  
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]  
GO  
```  
  
 Il progetti C\# e Visual Basic con questo esempio di codice sono disponibili in [Esempi di codice per sviluppatori](http://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=How%20to%20use%20DataAdapter%20to%20retrieve%20and%20update%20data&f%5B1%5D).  
  
```  
using System;  
using System.Data;  
using System.Data.Common;  
using System.Data.SqlClient;  
using System.Linq;  
using CSDataAdapterOperations.Properties;  
  
namespace CSDataAdapterOperations.Properties {  
   internal sealed partial class Settings : global::System.Configuration.ApplicationSettingsBase {  
  
      private static Settings defaultInstance = ((Settings)(global::System.Configuration.ApplicationSettingsBase.Synchronized(new Settings())));  
  
      public static Settings Default {  
         get {  
            return defaultInstance;  
         }  
      }  
  
      [global::System.Configuration.ApplicationScopedSettingAttribute()]  
      [global::System.Configuration.DefaultSettingValueAttribute("Data Source=(local);Initial Catalog=MySchool;Integrated Security=True")]  
      public string MySchoolConnectionString {  
         get {  
            return ((string)(this["MySchoolConnectionString"]));  
         }  
      }  
   }  
}  
  
class Program {  
   static void Main(string[] args) {  
      Settings settings = new Settings();  
  
      // Copy the data from the database.  Get the table Department and Course from the database.  
      String selectString = @"SELECT [DepartmentID],[Name],[Budget],[StartDate],[Administrator]  
                                     FROM [MySchool].[dbo].[Department];  
  
                                   SELECT [CourseID],@Year as [Year],Max([Title]) as [Title],  
                                   Max([Credits]) as [Credits],Max([DepartmentID]) as [DepartmentID]  
                                   FROM [MySchool].[dbo].[Course]  
                                   Group by [CourseID]";  
  
      DataSet mySchool = new DataSet();  
  
      SqlCommand selectCommand = new SqlCommand(selectString);  
      SqlParameter parameter = selectCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2);  
      parameter.Value = new Random(DateTime.Now.Millisecond).Next(9999);  
  
      // Use DataTableMapping to map the source tables and the destination tables.  
      DataTableMapping[] tableMappings = {new DataTableMapping("Table", "Department"), new DataTableMapping("Table1", "Course")};  
      CopyData(mySchool, settings.MySchoolConnectionString, selectCommand, tableMappings);  
  
      Console.WriteLine("The following tables are from the database.");  
      foreach (DataTable table in mySchool.Tables) {  
         Console.WriteLine(table.TableName);  
         ShowDataTable(table);  
      }  
  
      // Roll back the changes  
      DataTable department = mySchool.Tables["Department"];  
      DataTable course = mySchool.Tables["Course"];  
  
      department.Rows[0]["Name"] = "New" + department.Rows[0][1];  
      course.Rows[0]["Title"] = "New" + course.Rows[0]["Title"];  
      course.Rows[0]["Credits"] = 10;  
  
      Console.WriteLine("After we changed the tables:");  
      foreach (DataTable table in mySchool.Tables) {  
         Console.WriteLine(table.TableName);  
         ShowDataTable(table);  
      }  
  
      department.RejectChanges();  
      Console.WriteLine("After use the RejectChanges method in Department table to roll back the changes:");  
      ShowDataTable(department);  
  
      DataColumn[] primaryColumns = { course.Columns["CourseID"] };  
      DataColumn[] resetColumns = { course.Columns["Title"] };  
      ResetCourse(course, settings.MySchoolConnectionString, primaryColumns, resetColumns);  
      Console.WriteLine("After use the ResetCourse method in Course table to roll back the changes:");  
      ShowDataTable(course);  
  
      // Batch update the table.  
      String insertString = @"Insert into [MySchool].[dbo].[Course]([CourseID],[Year],[Title],   
                                   [Credits],[DepartmentID])   
             values (@CourseID,@Year,@Title,@Credits,@DepartmentID)";  
      SqlCommand insertCommand = new SqlCommand(insertString);  
      insertCommand.Parameters.Add("@CourseID", SqlDbType.NVarChar, 10, "CourseID");  
      insertCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2, "Year");  
      insertCommand.Parameters.Add("@Title", SqlDbType.NVarChar, 100, "Title");  
      insertCommand.Parameters.Add("@Credits", SqlDbType.Int, 4, "Credits");  
      insertCommand.Parameters.Add("@DepartmentID", SqlDbType.Int, 4, "DepartmentID");  
  
      const Int32 batchSize = 10;  
      BatchInsertUpdate(course, settings.MySchoolConnectionString, insertCommand, batchSize);  
   }  
  
   private static void CopyData(DataSet dataSet, String connectionString, SqlCommand selectCommand, DataTableMapping[] tableMappings) {  
      using (SqlConnection connection = new SqlConnection(connectionString)) {  
         selectCommand.Connection = connection;  
  
         connection.Open();  
  
         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {adapter.TableMappings.AddRange(tableMappings);  
            // If set the AcceptChangesDuringFill as the false, AcceptChanges will not be called on a   
            // DataRow after it is added to the DataTable during any of the Fill operations.  
            adapter.AcceptChangesDuringFill = false;  
  
            adapter.Fill(dataSet);  
         }  
      }  
   }  
  
   // Roll back only one column or several columns data of the Course table by call ResetDataTable method.  
   private static void ResetCourse(DataTable table, String connectionString,  
       DataColumn[] primaryColumns, DataColumn[] resetColumns) {  
      table.PrimaryKey = primaryColumns;  
  
      // Build the query string  
      String primaryCols = String.Join(",", primaryColumns.Select(col => col.ColumnName));  
      String resetCols = String.Join(",", resetColumns.Select(col => "Max(" + col.ColumnName + ") as " + col.ColumnName));  
  
      String selectString = String.Format("Select {0},{1} from Course Group by {0}", primaryCols, resetCols);  
  
      SqlCommand selectCommand = new SqlCommand(selectString);  
  
      ResetDataTable(table, connectionString, selectCommand);  
   }  
  
   // RejectChanges will roll back all changes made to the table since it was loaded, or the last time AcceptChanges   
   // was called. When you copy from the database, you can lose all the data after calling RejectChanges  
   // The ResetDataTable method rolls back one or more columns of data.  
   private static void ResetDataTable(DataTable table, String connectionString,  
       SqlCommand selectCommand) {  
      using (SqlConnection connection = new SqlConnection(connectionString)) {  
         selectCommand.Connection = connection;  
  
         connection.Open();  
  
         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {  
            // The incoming values for this row will be written to the current version of each   
            // column. The original version of each column's data will not be changed.  
            adapter.FillLoadOption = LoadOption.Upsert;  
  
            adapter.Fill(table);  
         }  
      }  
   }  
  
   private static void BatchInsertUpdate(DataTable table, String connectionString,  
       SqlCommand insertCommand, Int32 batchSize) {  
      using (SqlConnection connection = new SqlConnection(connectionString)) {  
         insertCommand.Connection = connection;  
         // When setting UpdateBatchSize to a value other than 1, all the commands   
         // associated with the SqlDataAdapter have to have their UpdatedRowSource   
         // property set to None or OutputParameters. An exception is thrown otherwise.  
         insertCommand.UpdatedRowSource = UpdateRowSource.None;  
  
         connection.Open();  
  
         using (SqlDataAdapter adapter = new SqlDataAdapter()) {  
            adapter.InsertCommand = insertCommand;  
            // Gets or sets the number of rows that are processed in each round-trip to the server.  
            // Setting it to 1 disables batch updates, as rows are sent one at a time.  
            adapter.UpdateBatchSize = batchSize;  
  
            adapter.Update(table);  
  
            Console.WriteLine("Successfully to update the table.");  
         }  
      }  
   }  
  
   private static void ShowDataTable(DataTable table) {  
      foreach (DataColumn col in table.Columns) {  
         Console.Write("{0,-14}", col.ColumnName);  
      }  
      Console.WriteLine("{0,-14}", "RowState");  
  
      foreach (DataRow row in table.Rows) {  
         foreach (DataColumn col in table.Columns) {  
            if (col.DataType.Equals(typeof(DateTime)))  
               Console.Write("{0,-14:d}", row[col]);  
            else if (col.DataType.Equals(typeof(Decimal)))  
               Console.Write("{0,-14:C}", row[col]);  
            else  
               Console.Write("{0,-14}", row[col]);  
         }  
         Console.WriteLine("{0,-14}", row.RowState);  
      }  
   }  
}  
```  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Stati delle righe e versioni delle righe](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)   
 [AcceptChanges e RejectChanges](../../../../docs/framework/data/adonet/dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)   
 [Unione del contenuto di un DataSet](../../../../docs/framework/data/adonet/dataset-datatable-dataview/merging-dataset-contents.md)   
 [Recupero dei valori di identità o del contatore](../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)