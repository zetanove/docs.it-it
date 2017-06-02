---
title: "Procedura: associare il controllo DataGrid Windows Form a un&#39;origine dati | Microsoft Docs"
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
  - "controlli con associazione"
  - "controlli con associazione, controllo DataGrid"
  - "associazione dati, controllo DataGrid"
  - "controlli con associazione a dati, DataGrid"
  - "DataGrid (controllo) [Windows Form], associazione dati"
  - "dataset [Windows Form], associazione al controllo DataGrid"
  - "controlli Windows Form, associazione dati"
ms.assetid: 128cdb07-dfd3-4d60-9d6a-902847667c36
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: associare il controllo DataGrid Windows Form a un&#39;origine dati
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGrid> Windows Form è specificamente progettato per la visualizzazione di informazioni di un'origine dati.  Il controllo viene associato in fase di esecuzione chiamando il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>.  Sebbene sia possibile visualizzare dati da numerose origini dati, quelle più comuni sono i dataset e le visualizzazioni dati.  
  
### Per eseguire l'associazione dati del controllo DataGrid a livello di codice  
  
1.  Aggiungere codice per il riempimento del dataset.  
  
     Se l'origine dati è un dataset o una visualizzazione dati basata su una tabella di dataset, aggiungere codice al form per riempire il dataset.  
  
     L'esatto codice utilizzato dipende da dove il dataset ottiene i dati.  Se il dataset viene popolato direttamente da un database, verrà chiamato il metodo `Fill`  di un adattatore dati, come nell'esempio riportato di seguito, nel quale viene popolato un dataset denominato `DsCategories1`:  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
     Se la compilazione del dataset avviene da un servizio Web XML, verrà normalmente creata un'istanza del servizio nel codice e verrà chiamato uno dei relativi metodi per restituire un dataset.  Quindi, il dataset del servizio Web XML verrà unito al dataset locale.  Nell'esempio riportato di seguito viene illustrato come creare un'istanza di un servizio Web XML denominato `CategoriesService`, come chiamare il metodo `GetCategories` corrispondente e come unire il dataset risultante a un dataset locale, denominato `DsCategories1`:  
  
    ```vb  
    Dim ws As New MyProject.localhost.CategoriesService()  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials  
    DsCategories1.Merge(ws.GetCategories())  
  
    ```  
  
    ```csharp  
    MyProject.localhost.CategoriesService ws = new MyProject.localhost.CategoriesService();  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials;  
    DsCategories1.Merge(ws.GetCategories());  
  
    ```  
  
    ```cpp  
    MyProject::localhost::CategoriesService^ ws =   
       new MyProject::localhost::CategoriesService();  
    ws->Credentials = System::Net::CredentialCache::DefaultCredentials;  
    dsCategories1->Merge(ws->GetCategories());  
    ```  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> del controllo <xref:System.Windows.Forms.DataGrid>, passando l'origine dati e un membro dati.  Nel caso non fosse necessario passare un membro dati in modo esplicito, passare una stringa vuota.  
  
    > [!NOTE]
    >  Se si sta eseguendo l'associazione della griglia per la prima volta, è possibile impostare le proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> e <xref:System.Windows.Forms.DataGrid.DataMember%2A> del controllo.  non sarà però più possibile reimpostarle, una volta eseguita l'operazione.  Si consiglia quindi di utilizzare sempre il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>.  
  
     Nell'esempio seguente viene illustrato come effettuare l'associazione a livello di codice alla tabella Customers in un dataset denominato `DsCustomers1`:  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers")  
  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers");  
  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "Customers");  
    ```  
  
     Se la tabella Customers è l'unica tabella del dataset, sarà possibile, in alternativa, associare la griglia nel modo che segue:  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "")  
  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "");  
  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "");  
    ```  
  
3.  Se lo si desidera, aggiungere alla griglia gli stili di tabella e di colonna appropriati.  Se non viene definito alcuno stile di tabella, la tabella verrà ugualmente visualizzata, ma con una formattazione minima e con tutte le colonne visibili.  
  
## Vedere anche  
 [Cenni preliminari sul controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)