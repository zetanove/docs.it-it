---
title: "Modifiche di DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f08008a9-042e-4de9-94f3-4f0e502b1eb5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Modifiche di DataTable
Quando si apportano modifiche ai valori di colonna in <xref:System.Data.DataRow>, le modifiche vengono inserite direttamente nello stato attuale della riga.  Il valore per <xref:System.Data.DataRowState> viene quindi impostato su **Modified** e le modifiche vengono accettate o rifiutate tramite i metodi <xref:System.Data.DataRow.AcceptChanges%2A> o <xref:System.Data.DataRow.RejectChanges%2A> di **DataRow**.  In **DataRow** sono inoltre disponibili tre metodi che consentono di sospendere lo stato di una riga durante la modifica.  Questi metodi sono <xref:System.Data.DataRow.BeginEdit%2A>, <xref:System.Data.DataRow.EndEdit%2A> e <xref:System.Data.DataRow.CancelEdit%2A>.  
  
 Quando si modificano i valori delle colonne direttamente in un **DataRow**, il **DataRow** gestirà tali valori usando le versioni di riga **Current**, **Default**, and **Original**.  Oltre a tali versioni di riga, nei metodi **BeginEdit**, **EndEdit** e **CancelEdit** viene usata una quarta versione: **Proposed**.  Per altre informazioni sulle versioni delle righe, vedere [Stati delle righe e versioni delle righe](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  
  
 La versione di riga **Proposed** risulta disponibile durante un'operazione di modifica iniziata chiamando **BeginEdit** e terminata tramite **EndEdit** o **CancelEdit** oppure tramite una chiamata ad **AcceptChanges** o **RejectChanges**.  
  
 Durante l'operazione di modifica è possibile applicare la logica di convalida a singole colonne valutando **ProposedValue** nell'evento **ColumnChanged** della **DataTable**.  L'evento **ColumnChanged** contiene **DataColumnChangeEventArgs**, che consente di conservare un riferimento alla colonna in fase di modifica e a **ProposedValue**.  Una volta terminata la valutazione del valore proposto, è possibile modificarlo o annullare la modifica.  Al termine della modifica, la riga perde lo stato **Proposed**.  
  
 È possibile confermare le modifiche chiamando **EndEdit** o annullarle chiamando **CancelEdit**.  Notare che mentre **EndEdit** consente di confermare le modifiche, **DataSet** non consente l'accettazione delle modifiche fino a quando non viene chiamato **AcceptChanges**.  Notare inoltre che se si chiama **AcceptChanges** prima del completamento della modifica tramite **EndEdit** o **CancelEdit**, l'operazione di modifica viene terminata e i valori di riga **Proposed** vengono accettati sia nella versione di riga **Current** che nella versione di riga **Original**.  Analogamente, la chiamata di **RejectChanges** consente di terminare la modifica ed eliminare le versioni di riga **Current** e **Proposed**.  Chiamando **EndEdit** o **CancelEdit** dopo aver chiamato **AcceptChanges** o **RejectChanges** non si otterrà alcun effetto, poiché l'operazione di modifica è già stata terminata.  
  
 Nell'esempio seguente viene mostrato come usare **BeginEdit** con **EndEdit** e **CancelEdit**.  L'esempio consente inoltre di controllare il valore **ProposedValue** nell'evento **ColumnChanged** e di stabilire se annullare la modifica.  
  
```vb  
Dim workTable As DataTable = New DataTable  
workTable.Columns.Add("LastName", Type.GetType("System.String"))  
  
AddHandler workTable.ColumnChanged, _  
  New DataColumnChangeEventHandler(AddressOf OnColumnChanged)  
  
Dim workRow As DataRow = workTable.NewRow()  
workRow(0) = "Smith"  
workTable.Rows.Add(workRow)  
  
workRow.BeginEdit()  
' Causes the ColumnChanged event to write a message and cancel the edit.  
workRow(0) = ""       
workRow.EndEdit()  
  
' Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow(0), workRow.RowState)  
  
Private Shared Sub OnColumnChanged( _  
  sender As Object, args As DataColumnChangeEventArgs)  
  If args.Column.ColumnName = "LastName" Then  
    If args.ProposedValue.ToString() = "" Then  
      Console.WriteLine("Last Name cannot be blank.  Edit canceled.")  
      args.Row.CancelEdit()  
    End If  
  End If  
End Sub  
  
```  
  
```csharp  
DataTable workTable  = new DataTable();  
workTable.Columns.Add("LastName", typeof(String));  
  
workTable.ColumnChanged +=   
  new DataColumnChangeEventHandler(OnColumnChanged);  
  
DataRow workRow = workTable.NewRow();  
workRow[0] = "Smith";  
workTable.Rows.Add(workRow);  
  
workRow.BeginEdit();  
// Causes the ColumnChanged event to write a message and cancel the edit.  
workRow[0] = "";       
workRow.EndEdit();  
  
// Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow[0], workRow.RowState);    
  
protected static void OnColumnChanged(  
  Object sender, DataColumnChangeEventArgs args)  
{  
  if (args.Column.ColumnName == "LastName")  
    if (args.ProposedValue.ToString() == "")  
    {  
      Console.WriteLine("Last Name cannot be blank. Edit canceled.");  
      args.Row.CancelEdit();  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataRowVersion>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Gestione degli eventi di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)