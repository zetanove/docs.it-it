---
title: "AcceptChanges e RejectChanges | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2d1a6fe-31f9-4b83-9728-06c406a3394e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# AcceptChanges e RejectChanges
Dopo aver verificato la correttezza delle modifiche apportate alla <xref:System.Data.DataTable>, è possibile accettare tali modifiche usando il metodo <xref:System.Data.DataRow.AcceptChanges%2A> del <xref:System.Data.DataRow>, della <xref:System.Data.DataTable> o del <xref:System.Data.DataSet>. I valori della riga **Current** verranno impostati come valori **Original** e la proprietà **RowState** verrà impostata su **Unchanged**.  L'accettazione o il rifiuto delle modifiche comporta la cancellazione di eventuali informazioni **RowError** e l'impostazione della proprietà **HasErrors** su **false**.  È inoltre possibile che l'accettazione o il rifiuto delle modifiche influisca sui dati di aggiornamento nell'origine dati.  Per altre informazioni, vedere [Aggiornamenti di origini dati tramite DataAdapter](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md).  
  
 Se nella **DataTable** sono presenti vincoli di chiave esterna, le modifiche accettate o rifiutate tramite **AcceptChanges** e **RejectChanges** verranno propagate alle righe figlio del **DataRow** in base a **ForeignKeyConstraint.AcceptRejectRule**.  Per altre informazioni, vedere [Vincoli di DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md).  
  
 L'esempio seguente controlla se sono presenti righe con errori, risolve errori laddove è possibile e rifiuta le righe contenenti errori non risolvibili.  Notare che, per quanto riguarda gli errori risolti, il valore **RowError** viene reimpostato su una stringa vuota, provocando l'impostazione della proprietà **HasErrors** su **false**.  Quando tutte le righe contenenti errori sono state risolte o rifiutate, viene effettuata la chiamata ad **AcceptChanges** per accettare tutte le modifiche per l'intera **DataTable**.  
  
```vb  
If workTable.HasErrors Then  
  Dim errRow As DataRow  
  
  For Each errRow in workTable.GetErrors()  
  
    If errRow.RowError = "Total cannot exceed 1000." Then  
      errRow("Total") = 1000  
      errRow.RowError = ""    ' Clear the error.  
    Else  
      errRow.RejectChanges()  
    End If  
  Next  
End If  
  
workTable.AcceptChanges()  
  
```  
  
```csharp  
if (workTable.HasErrors)  
{  
  
  foreach (DataRow errRow in workTable.GetErrors())  
  {  
    if (errRow.RowError == "Total cannot exceed 1000.")  
    {  
      errRow["Total"] = 1000;  
      errRow.RowError = "";    // Clear the error.  
    }  
    else  
      errRow.RejectChanges();  
  }  
}  
  
workTable.AcceptChanges();  
```  
  
## Vedere anche  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [Modifica dei dati in una DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)