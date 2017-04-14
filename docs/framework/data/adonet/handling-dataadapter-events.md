---
title: "Gestione degli eventi di DataAdapter | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Gestione degli eventi di DataAdapter
<xref:System.Data.Common.DataAdapter> di ADO.NET espone tre eventi che è possibile usare per rispondere alle modifiche apportate ai dati nell'origine dati.  Nella tabella seguente vengono descritti gli eventi di `DataAdapter`.  
  
|Evento|Descrizione|  
|------------|-----------------|  
|`RowUpdating`|Sta per iniziare un'operazione UPDATE, INSERT o DELETE su una riga tramite la chiamata a uno dei metodi `Update`.|  
|`RowUpdated`|È stata completata un'operazione UPDATE, INSERT o DELETE su una riga tramite la chiamata a uno dei metodi `Update`.|  
|`FillError`|Si è verificato un errore durante un'operazione `Fill`.|  
  
## RowUpdating e RowUpdated  
 `RowUpdating` viene generato prima che un aggiornamento a una riga di <xref:System.Data.DataSet> sia stato elaborato nell'origine dati.  `RowUpdated` viene generato dopo che un aggiornamento a una riga di `DataSet` è stato elaborato nell'origine dati.  Di conseguenza, è possibile usare `RowUpdating` per modificare il comportamento dell'aggiornamento prima che venga eseguito, in modo da fornire una gestione aggiuntiva quando verrà eseguito l'aggiornamento, conservare un riferimento a una riga aggiornata, annullare l'aggiornamento corrente e pianificarlo per un processo in batch che verrà eseguito successivamente e così via.  `RowUpdated` risulta utile per rispondere a errori ed eccezioni che si verificano durante l'aggiornamento.  È possibile aggiungere le informazioni sugli errori al `DataSet` così come riprovare la logica e così via.  
  
 Gli argomenti <xref:System.Data.Common.RowUpdatingEventArgs> e <xref:System.Data.Common.RowUpdatedEventArgs> passati agli eventi `RowUpdating` e `RowUpdated` includono una proprietà `Command` che fa riferimento all'oggetto `Command` usato per eseguire l'aggiornamento, una proprietà `Row` che fa riferimento all'oggetto `DataRow` contenente le informazioni aggiornate, una proprietà `StatementType` relativa al tipo di aggiornamento eseguito, l'oggetto `TableMapping`, se applicabile, e lo `Status` dell'operazione.  
  
 È possibile usare la proprietà `Status` per determinare se si è verificato un errore durante l'operazione ed eventualmente per controllare le operazioni relative alle righe correnti e risultanti.  Quando si verifica l'evento, la proprietà `Status` sarà uguale a `Continue` o `ErrorsOccurred`.  Nella tabella seguente sono indicati i valori su cui è possibile impostare la proprietà `Status` per controllare le operazioni successive durante l'aggiornamento.  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|`Continue`|Continua l'operazione di aggiornamento.|  
|`ErrorsOccurred`|Interrompe l'operazione di aggiornamento e genera un'eccezione.|  
|`SkipCurrentRow`|Ignora la riga corrente e continua l'operazione di aggiornamento.|  
|`SkipAllRemainingRows`|Interrompe l'operazione di aggiornamento, ma non genera un'eccezione.|  
  
 Se si imposta la proprietà `Status` su `ErrorsOccurred`, verrà generata un'eccezione.  È possibile controllare l'eccezione generata impostando la proprietà `Errors` sull'eccezione desiderata.  Se si usa uno degli altri valori di `Status` non verrà generata alcuna eccezione.  
  
 È inoltre possibile usare la proprietà `ContinueUpdateOnError` per gestire gli errori relativi alle righe aggiornate.  Se `DataAdapter.ContinueUpdateOnError` è `true`, quando un aggiornamento di una riga determina la generazione di un'eccezione, il testo dell'eccezione viene inserito nelle informazioni `RowError` della stessa riga e l'elaborazione continua senza generare un'eccezione.  In questo modo è possibile rispondere agli errori quando l'evento `Update` è completato, a differenza di quanto avviene con l'evento `RowUpdated` che consente di rispondere agli errori nel momento in cui si verificano.  
  
 Nell'esempio di codice seguente viene illustrato come aggiungere e rimuovere i gestori eventi.  Il gestore dell'evento `RowUpdating` scrive un log di tutti i record eliminati con un timestamp.  Il gestore dell'evento `RowUpdated` aggiunge le informazioni sugli errori alla proprietà `RowError` della riga nel `DataSet`, evita la generazione dell'eccezione e continua l'elaborazione, riproducendo quindi il comportamento di `ContinueUpdateOnError` \= `true`.  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
' Add handlers.  
AddHandler custAdapter.RowUpdating, New SqlRowUpdatingEventHandler( _  
  AddressOf OnRowUpdating)  
AddHandler custAdapter.RowUpdated, New SqlRowUpdatedEventHandler(  
  AddressOf OnRowUpdated)  
  
' Set DataAdapter command properties, fill DataSet, and modify DataSet.  
  
custAdapter.Update(custDS, "Customers")  
  
' Remove handlers.  
RemoveHandler custAdapter.RowUpdating, _  
  New SqlRowUpdatingEventHandler(AddressOf OnRowUpdating)  
RemoveHandler custAdapter.RowUpdated, _  
  New SqlRowUpdatedEventHandler(AddressOf OnRowUpdated)  
  
Private Shared Sub OnRowUpdating(sender As Object, _  
  args As SqlRowUpdatingEventArgs)  
  If args.StatementType = StatementType.Delete Then  
    Dim tw As System.IO.TextWriter = _  
  System.IO.File.AppendText("Deletes.log")  
    tw.WriteLine( _  
      "{0}: Customer {1} Deleted.", DateTime.Now, args.Row(_  
      "CustomerID", DataRowVersion.Original))  
    tw.Close()  
  End If  
End Sub  
  
Private Shared Sub OnRowUpdated( _  
  sender As Object, args As SqlRowUpdatedEventArgs)  
  If args.Status = UpdateStatus.ErrorsOccurred  
    args.Status = UpdateStatus.SkipCurrentRow  
    args.Row.RowError = args.Errors.Message  
  End If  
End Sub  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
// Add handlers.  
custAdapter.RowUpdating += new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
// Set DataAdapter command properties, fill DataSet, modify DataSet.  
  
custAdapter.Update(custDS, "Customers");  
  
// Remove handlers.  
custAdapter.RowUpdating -= new SqlRowUpdatingEventHandler(OnRowUpdating);  
custAdapter.RowUpdated -= new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
protected static void OnRowUpdating(  
  object sender, SqlRowUpdatingEventArgs args)  
{  
  if (args.StatementType == StatementType.Delete)  
  {  
    System.IO.TextWriter tw = System.IO.File.AppendText("Deletes.log");  
    tw.WriteLine(  
      "{0}: Customer {1} Deleted.", DateTime.Now,   
       args.Row["CustomerID", DataRowVersion.Original]);  
    tw.Close();  
  }  
}  
  
protected static void OnRowUpdated(  
  object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.Status == UpdateStatus.ErrorsOccurred)  
  {  
    args.Row.RowError = args.Errors.Message;  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## FillError  
 `DataAdapter` genera l'evento `FillError` quando si verifica un errore durante un'operazione `Fill`.  Questo tipo di errore si verifica solitamente quando i dati nella riga che viene aggiunta non possono essere convertiti in un tipo .NET Framework senza una perdita di precisione.  
  
 Se si verifica un errore durante un'operazione `Fill`, la riga corrente non verrà aggiunta a `DataTable`.  L'evento `FillError` consente di risolvere l'errore e aggiungere la riga o di ignorare la riga esclusa e continuare l'operazione `Fill`.  
  
 `FillErrorEventArgs` passato all'evento `FillError` può contenere diverse proprietà che consentono di rispondere agli errori e di risolverli.  Nella tabella seguente sono illustrate le proprietà dell'oggetto `FillErrorEventArgs`.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|`Errors`|`Exception` generata.|  
|`DataTable`|Oggetto `DataTable` in fase di riempimento quando si è verificato l'errore.|  
|`Values`|Matrice di oggetti contenente i valori della riga in fase di inserimento quando si è verificato l'errore.  I riferimenti ordinali della matrice di `Values` corrispondono ai riferimenti ordinali delle colonne della riga che viene aggiunta.  `Values[0]`, ad esempio, è il valore che era stato aggiunto come prima colonna della riga.|  
|`Continue`|Consente di scegliere se generare o meno una Exception.  Se si imposta la proprietà `Continue` su `false`, l'operazione `Fill` corrente verrà interrotta e verrà generata un'eccezione.  Se si imposta `Continue` su `true`, l'operazione `Fill` continuerà nonostante l'errore.|  
  
 Nell'esempio di codice seguente viene aggiunto un gestore per l'evento `FillError` di `DataAdapter`.  Nel codice dell'evento `FillError` viene determinato se esiste il rischio potenziale di una perdita di precisione e viene fornita la possibilità di rispondere all'eccezione.  
  
```vb  
AddHandler adapter.FillError, New FillErrorEventHandler( _  
  AddressOf FillError)  
  
Dim dataSet As DataSet = New DataSet  
adapter.Fill(dataSet, "ThisTable")  
  
Private Shared Sub FillError(sender As Object, _  
  args As FillErrorEventArgs)  
  If args.Errors.GetType() Is Type.GetType("System.OverflowException") Then  
    ' Code to handle precision loss.  
    ' Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(New Object() _  
      {args.Values(0), args.Values(1), DBNull.Value})  
    ' Set the RowError containing the value for the third column.  
    args.RowError = _  
      "OverflowException encountered. Value from data source: " & _  
      args.Values(2)  
    args.Continue = True  
  End If  
End Sub  
```  
  
```csharp  
adapter.FillError += new FillErrorEventHandler(FillError);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "ThisTable");  
  
protected static void FillError(object sender, FillErrorEventArgs args)  
{  
  if (args.Errors.GetType() == typeof(System.OverflowException))  
  {  
    // Code to handle precision loss.  
    //Add a row to table using the values from the first two columns.  
    DataRow myRow = args.DataTable.Rows.Add(new object[]  
       {args.Values[0], args.Values[1], DBNull.Value});  
    //Set the RowError containing the value for the third column.  
    args.RowError =   
       "OverflowException Encountered. Value from data source: " +  
       args.Values[2];  
    args.Continue = true;  
  }  
}  
```  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Gestione di eventi dataset](../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataset-events.md)   
 [Gestione degli eventi di DataTable](../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)   
 [Eventi](../../../../docs/standard/events/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)