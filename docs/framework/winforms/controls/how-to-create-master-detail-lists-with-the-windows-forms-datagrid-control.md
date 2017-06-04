---
title: "Procedura: creare elenchi Master-Details con il controllo DataGrid Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DataGrid (controllo) [Windows Form], Master-Details (elenchi)"
  - "Master-Details (elenchi)"
  - "tabelle correlate, visualizzazione nel controllo DataGrid"
ms.assetid: 20388c6a-94f9-4d96-be18-8c200491247f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: creare elenchi Master-Details con il controllo DataGrid Windows Form
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Se <xref:System.Data.DataSet> contiene una serie di tabelle correlate, è possibile utilizzare due controlli <xref:System.Windows.Forms.DataGrid> per visualizzare i dati in un formato Master\-Details.  Il primo <xref:System.Windows.Forms.DataGrid> viene designato come griglia principale e il secondo come griglia dei dettagli.  Quando si seleziona una voce nell'elenco principale, nell'elenco dei dettagli vengono visualizzate tutte le relative voci figlio.  Se ad esempio <xref:System.Data.DataSet> contiene una tabella Customers e una tabella correlata Orders, è possibile specificare la tabella Customers come griglia principale e la tabella Orders come griglia dei dettagli.  Quando si seleziona un cliente nella griglia principale, tutti gli ordini associati a quel cliente inclusi nella tabella Orders verranno visualizzati nella griglia dei dettagli.  
  
### Per impostare una relazione Master\-Details a livello di codice  
  
1.  Creare due nuovi controlli <xref:System.Windows.Forms.DataGrid> e impostarne le proprietà.  
  
2.  Aggiungere delle tabelle al dataset.  
  
3.  Dichiarare una variabile di tipo <xref:System.Data.DataRelation> per rappresentare la relazione che si desidera creare.  
  
4.  Creare un'istanza della relazione \(DataRelation\) specificando un nome per la relazione nonché la tabella, la colonna e l'elemento che collegheranno le due tabelle.  
  
5.  Aggiungere la relazione alla raccolta <xref:System.Data.DataSet.Relations%2A> dell'oggetto <xref:System.Data.DataSet>.  
  
6.  Utilizzare il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> del controllo <xref:System.Windows.Forms.DataGrid> per associare entrambe le griglie all'oggetto <xref:System.Data.DataSet>.  
  
     Nell'esempio riportato di seguito viene illustrato come impostare una relazione Master\-Details tra la tabella Customers e la tabella Orders in un oggetto <xref:System.Data.DataSet> \(`ds`\) precedentemente generato.  
  
    ```vb  
    Dim myDataRelation As DataRelation  
    myDataRelation = New DataRelation _  
       ("CustOrd", ds.Tables("Customers").Columns("CustomerID"), _  
       ds.Tables("Orders").Columns("CustomerID"))  
    ' Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation)  
    GridOrders.SetDataBinding(ds, "Customers")  
    GridDetails.SetDataBinding(ds, "Customers.CustOrd")  
  
    ```  
  
    ```csharp  
    DataRelation myDataRelation;  
    myDataRelation = new DataRelation("CustOrd", ds.Tables["Customers"].Columns["CustomerID"], ds.Tables["Orders"].Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation);  
    GridOrders.SetDataBinding(ds,"Customers");  
    GridDetails.SetDataBinding(ds,"Customers.CustOrd");  
  
    ```  
  
    ```cpp  
    DataRelation^ myDataRelation;  
    myDataRelation = gcnew DataRelation("CustOrd",  
       ds->Tables["Customers"]->Columns["CustomerID"],  
       ds->Tables["Orders"]->Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds->Relations->Add(myDataRelation);  
    GridOrders->SetDataBinding(ds, "Customers");  
    GridDetails->SetDataBinding(ds, "Customers.CustOrd");  
    ```  
  
## Vedere anche  
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Cenni preliminari sul controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [Procedura: associare il controllo DataGrid Windows Form a un'origine dati](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)