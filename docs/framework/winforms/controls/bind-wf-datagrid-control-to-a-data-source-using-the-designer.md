---
title: "Procedura: associare il controllo DataGrid Windows Form a un&#39;origine dati mediante la finestra di progettazione | Microsoft Docs"
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
ms.assetid: 4e96e3d0-b1cc-4de1-8774-bc9970ec4554
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: associare il controllo DataGrid Windows Form a un&#39;origine dati mediante la finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Il controllo <xref:System.Windows.Forms.DataGrid> Windows Form è specificamente progettato per la visualizzazione di informazioni di un'origine dati.  Per associare il controllo in fase di progettazione, impostare le proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> e <xref:System.Windows.Forms.DataGrid.DataMember%2A> oppure, in fase di esecuzione, chiamare il metodo <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>.  Sebbene sia possibile visualizzare dati da numerose origini dati, quelle più comuni sono i dataset e le visualizzazioni dati.  
  
 Se l'origine dati è disponibile in fase di progettazione, ad esempio se il form contiene un'istanza di un dataset o di una visualizzazione dati, sarà possibile associare la griglia all'origine dati in fase di progettazione.  Sarà quindi possibile visualizzare in anteprima la disposizione dei dati all'interno della griglia  
  
 e associare la griglia a livello di codice, in fase di esecuzione.  Ciò risulta utile quando si desidera impostare un'origine dati in base alle informazioni ottenute in fase di esecuzione.  L'applicazione, ad esempio, potrebbe consentire all'utente di specificare il nome di una tabella da visualizzare.  Questa funzionalità è inoltre necessaria quando l'origine dati non esiste in fase di progettazione,  come nel caso di matrici, raccolte, dataset non tipizzati e visualizzatori di dati.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGrid>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  Per impostazione predefinita, in [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] il controllo <xref:System.Windows.Forms.DataGrid> non si trova nella **Casella degli strumenti**.  Per informazioni su come aggiungerlo, vedere [How to: Add Items to the Toolbox](http://msdn.microsoft.com/it-it/458e119e-17fe-450b-b889-e31c128bd7e0).  Inoltre, in [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] è possibile utilizzare la finestra **Origini dati** per l'associazione di dati in fase di progettazione.  Per ulteriori informazioni, vedere [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per associare il controllo DataGrid a una singola tabella nella finestra di progettazione  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> del controllo su un oggetto contenente gli elementi di dati ai quali si desidera effettuare l'associazione.  
  
2.  Se l'origine dati è un dataset, impostare la proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A> sul nome della tabella alla quale si desidera effettuare l'associazione.  
  
3.  Se l'origine dati è un dataset o una visualizzazione dati basata su una tabella di dataset, aggiungere codice al form per riempire il dataset.  
  
     L'esatto codice utilizzato dipende da dove il dataset ottiene i dati.  Se il dataset viene popolato direttamente da un database, verrà chiamato il metodo `Fill` di un adattatore dati, come nell'esempio di codice riportato di seguito, nel quale viene popolato un dataset denominato `DsCategories1`:  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
4.  Se lo si desidera, aggiungere alla griglia gli stili di tabella e di colonna appropriati.  
  
     Se non viene definito alcuno stile di tabella, la tabella verrà ugualmente visualizzata, ma con una formattazione minima e con tutte le colonne visibili.  
  
### Per associare il controllo DataGrid a più tabelle in un dataset nella finestra di progettazione  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A> del controllo su un oggetto contenente gli elementi di dati ai quali si desidera effettuare l'associazione.  
  
2.  Se il dataset contiene tabelle correlate, ovvero se contiene un oggetto relazione, impostare la proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A> sul nome della tabella padre.  
  
3.  Aggiungere codice per il riempimento del dataset.  
  
## Vedere anche  
 [Cenni preliminari sul controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [Procedura: aggiungere tabelle e colonne al controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Accesso ai dati in Visual Studio](../Topic/Accessing%20data%20in%20Visual%20Studio.md)