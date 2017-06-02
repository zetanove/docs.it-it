---
title: "Informazioni sugli errori delle righe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b1f9070-d032-48c7-b030-bd8fbb2ca59a
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Informazioni sugli errori delle righe
Per evitare di dover rispondere agli errori delle righe mentre si modificano i valori di una <xref:System.Data.DataTable>, è possibile aggiungere alla riga le informazioni sugli errori per un uso successivo.  A questo scopo, l'oggetto <xref:System.Data.DataRow> fornisce una proprietà <xref:System.Data.DataRow.RowError%2A> su ciascuna riga.  L'aggiunta di dati alla proprietà **RowError** di un **DataRow** consente di impostare la proprietà <xref:System.Data.DataRow.HasErrors%2A> di **DataRow** su **true**.  Se il **DataRow** fa parte di una **DataTable** e il valore per **DataRow.HasErrors** è **true**, anche il valore per la proprietà **DataTable.HasErrors** sarà **true**.  Queste impostazioni si applicano anche al **DataSet** a cui appartiene la **DataTable**.  Quando si effettuano verifiche relative agli errori, è possibile controllare la proprietà **HasErrors** per stabilire se alle righe sono state aggiunte informazioni relative agli errori.  Se il valore per **HasErrors** è **true**, è possibile usare il metodo <xref:System.Data.DataTable.GetErrors%2A> della **DataTable** per restituire ed esaminare solo le righe contenenti errori, come mostrato nell'esempio seguente.  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
workTable.Columns.Add("CustID", Type.GetType("System.Int32"))  
workTable.Columns.Add("Total", Type.GetType("System.Double"))  
  
AddHandler workTable.RowChanged, New DataRowChangeEventHandler(AddressOf OnRowChanged)  
  
Dim i  As Int32  
  
For i  = 0 To 10  
  workTable.Rows.Add(New Object() {i , i *100})  
Next  
  
If workTable.HasErrors Then  
  Console.WriteLine("Errors in Table " & workTable.TableName)  
  
  Dim myRow As DataRow  
  
  For Each myRow In workTable.GetErrors()  
    Console.WriteLine("CustID = " & myRow("CustID").ToString())  
    Console.WriteLine(" Error = " & myRow.RowError & vbCrLf)  
  Next  
End If  
  
Private Shared Sub OnRowChanged( _  
    sender As Object, args As DataRowChangeEventArgs)  
  ' Check for zero values.  
  If CDbl(args.Row("Total")) = 0 Then args.Row.RowError = _  
      "Total cannot be 0."  
End Sub  
  
```  
  
```csharp  
DataTable  workTable = new DataTable("Customers");  
workTable.Columns.Add("CustID", typeof(Int32));  
workTable.Columns.Add("Total", typeof(Double));  
  
workTable.RowChanged += new DataRowChangeEventHandler(OnRowChanged);  
  
for (int i = 0; i < 10; i++)  
  workTable.Rows.Add(new Object[] {i, i*100});  
  
if (workTable.HasErrors)  
{  
  Console.WriteLine("Errors in Table " + workTable.TableName);  
  
  foreach (DataRow myRow in workTable.GetErrors())  
  {  
    Console.WriteLine("CustID = " + myRow["CustID"]);  
    Console.WriteLine(" Error = " + myRow.RowError + "\n");  
  }  
}  
  
protected static void OnRowChanged(  
    Object sender, DataRowChangeEventArgs args)  
{  
  // Check for zero values.  
  if (args.Row["Total"].Equals(0D))  
    args.Row.RowError = "Total cannot be 0.";  
}  
```  
  
## Vedere anche  
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataTable>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)