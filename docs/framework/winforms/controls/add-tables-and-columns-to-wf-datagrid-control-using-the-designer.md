---
title: "Procedura: aggiungere tabelle e colonne nel controllo DataGrid Windows Form mediante la finestra di progettazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "colonne [Windows Form], aggiunta al controllo DataGrid"
  - "DataGrid (controllo) [Windows Form], aggiunta di tabelle e colonne"
  - "tabelle [Windows Form], aggiunta al controllo DataGrid"
ms.assetid: 4a6d1b34-b696-476b-bf8a-57c6230aa9e1
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: aggiungere tabelle e colonne nel controllo DataGrid Windows Form mediante la finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 È possibile visualizzare i dati del controllo <xref:System.Windows.Forms.DataGrid> Windows Form in tabelle e colonne creando oggetti <xref:System.Windows.Forms.DataGridTableStyle> e aggiungendoli all'oggetto <xref:System.Windows.Forms.GridTableStylesCollection>, a cui si accede mediante la proprietà <xref:System.Windows.Forms.DataGrid.TableStyles%2A> del controllo <xref:System.Windows.Forms.DataGrid>.  Ogni stile di tabella consente di visualizzare il contenuto di qualsiasi tabella di dati specificata nella proprietà <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> della classe <xref:System.Windows.Forms.DataGridTableStyle>.  Per impostazione predefinita, uno stile di tabella per il quale non sono stati specificati stili di colonna consente di visualizzare tutte le colonne presenti nella tabella di dati corrispondente.  È possibile limitare le colonne della tabella che dovranno essere visualizzate aggiungendo oggetti <xref:System.Windows.Forms.DataGridColumnStyle> all'insieme <xref:System.Windows.Forms.GridColumnStylesCollection>, a cui si accede mediante la proprietà <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> di ciascuna classe <xref:System.Windows.Forms.DataGridTableStyle>.  
  
 Nelle seguenti procedure è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGrid>.  Per informazioni su come impostare tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  Per impostazione predefinita, in [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] il controllo <xref:System.Windows.Forms.DataGrid> non si trova nella **Casella degli strumenti**.  Per informazioni su come aggiungerlo, vedere [How to: Add Items to the Toolbox](http://msdn.microsoft.com/it-it/458e119e-17fe-450b-b889-e31c128bd7e0).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere una tabella al controllo DataGrid nella finestra di progettazione  
  
1.  Per visualizzare i dati nella tabella è innanzitutto necessario associare il controllo <xref:System.Windows.Forms.DataGrid> a un dataset.  Per ulteriori informazioni, vedere [Procedura: associare il controllo DataGrid Windows Form a un'origine dati mediante la finestra di progettazione](../../../../docs/framework/winforms/controls/bind-wf-datagrid-control-to-a-data-source-using-the-designer.md).  
  
2.  Selezionare la proprietà <xref:System.Windows.Forms.DataGrid.TableStyles%2A> del controllo <xref:System.Windows.Forms.DataGrid> nella finestra Proprietà, quindi fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà per visualizzare l'**Editor della raccolta DataGridTableStyle**.  
  
3.  Nell'editor della raccolta fare clic su **Aggiungi** per inserire uno stile di tabella.  
  
4.  Scegliere **OK** per chiudere l'editor della raccolta, quindi aprirlo nuovamente facendo clic sul pulsante con i puntini di sospensione accanto alla proprietà <xref:System.Windows.Forms.DataGrid.TableStyles%2A>.  
  
     Alla riapertura dell'editor della raccolta, tutte le tabelle di dati associate al controllo verranno visualizzate nell'elenco a discesa corrispondente alla proprietà <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> dello stile di tabella.  
  
5.  Nella casella **Membri** dell'editor di raccolte fare clic sullo stile di tabella.  
  
6.  Nella casella **Proprietà** dell'editor della raccolta selezionare il valore di <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> per la tabella che si desidera visualizzare.  
  
### Per aggiungere una colonna al controllo DataGrid nella finestra di progettazione  
  
1.  Nella casella **Membri** dell'**Editor della raccolta DataGridTableStyle** selezionare lo stile di tabella appropriato.  Nella casella **Proprietà** dell'editor della raccolta selezionare la raccolta <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>, quindi fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà per visualizzare l'**Editor della raccolta DataGridColumnStyle**.  
  
2.  Nell'editor della raccolta fare clic su **Aggiungi** per inserire uno stile di colonna oppure fare clic sulla freccia verso il basso accanto ad **Aggiungi** per specificare un tipo di colonna.  
  
     Nella casella di riepilogo a discesa è possibile selezionare il tipo <xref:System.Windows.Forms.DataGridTextBoxColumn> o <xref:System.Windows.Forms.DataGridBoolColumn>.  
  
3.  Fare clic su OK per chiudere l'**Editor della raccolta DataGridColumnStyle**, quindi aprirlo nuovamente facendo clic sul pulsante con i puntini di sospensione accanto alla proprietà <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>.  
  
     Alla riapertura dell'editor della raccolta, tutte le colonne di dati della tabella di dati associata verranno visualizzate nell'elenco a discesa corrispondente alla proprietà <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> dello stile di colonna.  
  
4.  Nella casella **Membri** dell'editor di raccolte fare clic sullo stile di colonna.  
  
5.  Nella casella **Proprietà** dell'editor della raccolta selezionare il valore di <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> per la colonna che si desidera visualizzare.  
  
## Vedere anche  
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Procedura: eliminare o nascondere colonne nel controllo DataGrid Windows Form](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)