---
title: "Modifica di DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 697a3991-b660-4a5a-8a54-1a2304ff158e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Modifica di DataView
È possibile usare il <xref:System.Data.DataView> per aggiungere, eliminare o modificare righe di dati nella tabella sottostante.  La possibilità di usare il **DataView** per modificare i dati nella tabella sottostante è controllata dall'impostazione di una delle tre proprietà Boolean del **DataView**.  Tali proprietà sono <xref:System.Data.DataView.AllowNew%2A>, <xref:System.Data.DataView.AllowEdit%2A> e <xref:System.Data.DataView.AllowDelete%2A>.  L'impostazione predefinita è **true**.  
  
 Se la proprietà **AllowNew** è **true**, è possibile usare il metodo <xref:System.Data.DataView.AddNew%2A> del **DataView** per creare un nuovo <xref:System.Data.DataRowView>.  Notare che la nuova riga viene effettivamente aggiunta alla <xref:System.Data.DataTable> sottostante solo dopo la chiamata del metodo <xref:System.Data.DataRowView.EndEdit%2A> di **DataRowView**.  Se viene chiamato il metodo <xref:System.Data.DataRowView.CancelEdit%2A> del **DataRowView**, la nuova riga verrà eliminata.  Notare inoltre che è possibile modificare solo un **DataRowView** alla volta.  Se si chiama il metodo **AddNew** o **BeginEdit** del **DataRowView** mentre è presente una riga in sospeso, **EndEdit** viene chiamato implicitamente per la riga in sospeso.  Quando viene chiamato **EndEdit**, le modifiche vengono applicate alla **DataTable** sottostante ed è possibile confermarle o rifiutarle in un secondo momento mediante i metodi **AcceptChanges** o **RejectChanges** dell'oggetto **DataTable**, **DataSet** o **DataRow**.  Se la proprietà **AllowNew** è **false**, in caso di chiamata del metodo **AddNew** del **DataRowView** viene generata un'eccezione.  
  
 Se la proprietà **AllowEdit** è **true**, è possibile modificare il contenuto del **DataRow** mediante il **DataRowView**.  È possibile confermare le modifiche alla riga sottostante mediante **DataRowView.EndEdit** o rifiutare tali modifiche mediante **DataRowView.CancelEdit**.  Notare che è possibile modificare solo una riga alla volta.  Se si chiama il metodo **AddNew** o **BeginEdit** del **DataRowView** mentre è presente una riga in sospeso, **EndEdit** viene chiamato implicitamente per la riga in sospeso.  Quando viene chiamato **EndEdit**, le modifiche proposte vengono inserite nella versione di riga **Current** del **DataRow** sottostante ed è possibile confermarle o rifiutarle in un secondo momento mediante il metodo **AcceptChanges** o **RejectChanges** dell'oggetto **DataTable**, **DataSet** o **DataRow**.  Se la proprietà **AllowEdit** è **false**, in caso di tentativo di modifica di un valore nel **DataView** viene generata un'eccezione.  
  
 Quando un **DataRowView** esistente viene modificato, gli eventi della **DataTable** sottostante vengono ancora generati con le modifiche proposte.  Notare che se si chiama **EndEdit** o **CancelEdit** nel **DataRow** sottostante, le modifiche in sospeso verranno applicate o annullate indipendentemente dalla chiamata o meno di **EndEdit** o **CancelEdit** per il **DataRowView**.  
  
 Se la proprietà **AllowDelete** è **true**, è possibile eliminare righe dal **DataView** mediante il metodo **Delete** dell'oggetto **DataView** o **DataRowView** e le righe verranno eliminate dalla **DataTable** sottostante.  È possibile confermare o rifiutare le eliminazioni in un secondo momento rispettivamente mediante il metodo **AcceptChanges** o **RejectChanges**.  Se la proprietà **AllowDelete** è **false**, in caso di chiamata del metodo **Delete** del **DataView** o del **DataRowView** viene generata un'eccezione.  
  
 Nell'esempio di codice seguente viene disabilitata la possibilità di eliminare righe mediante l'oggetto **DataView** e vengono aggiunte nuove righe alla tabella sottostante mediante l'oggetto **DataView**.  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custView As DataView = custTable.DefaultView  
custView.Sort = "CompanyName"  
  
custView.AllowDelete = False  
  
Dim newDRV As DataRowView = custView.AddNew()  
newDRV("CustomerID") = "ABCDE"  
newDRV("CompanyName") = "ABC Products"  
newDRV.EndEdit()  
  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
DataView custView = custTable.DefaultView;  
custView.Sort = "CompanyName";  
  
custView.AllowDelete = false;  
  
DataRowView newDRV = custView.AddNew();  
newDRV["CustomerID"] = "ABCDE";  
newDRV["CompanyName"] = "ABC Products";  
newDRV.EndEdit();  
```  
  
## Vedere anche  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 <xref:System.Data.DataRowView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)