---
title: "Procedura: creare elenchi Master-Details mediante il controllo DataGrid Windows Form nella finestra di progettazione | Microsoft Docs"
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
ms.assetid: 19438ba2-f687-4417-a2fb-ab1cd69d4ded
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare elenchi Master-Details mediante il controllo DataGrid Windows Form nella finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.DataGridView> sostituisca il controllo <xref:System.Windows.Forms.DataGrid> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.DataGrid> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  Per ulteriori informazioni vedere [Differenze tra i controlli DataGridView e DataGrid di Windows Form](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md).  
  
 Se <xref:System.Data.DataSet> contiene una serie di tabelle correlate, è possibile utilizzare due controlli <xref:System.Windows.Forms.DataGrid> per visualizzare i dati in un formato Master\-Details.  Il primo <xref:System.Windows.Forms.DataGrid> viene designato come griglia principale e il secondo come griglia dei dettagli.  Quando si seleziona una voce nell'elenco principale, nell'elenco dei dettagli vengono visualizzate tutte le relative voci figlio.  Se ad esempio <xref:System.Data.DataSet> contiene una tabella Customers e una tabella correlata Orders, è possibile specificare la tabella Customers come griglia principale e la tabella Orders come griglia dei dettagli.  Quando si seleziona un cliente nella griglia principale, tutti gli ordini associati a quel cliente inclusi nella tabella Orders verranno visualizzati nella griglia dei dettagli.  
  
 Per la procedura descritta di seguito è richiesto un progetto **Applicazione Windows**.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per creare un elenco Master\-Details nella finestra di progettazione  
  
1.  Aggiungere due controlli <xref:System.Windows.Forms.DataGrid> nel form.  Per ulteriori informazioni, vedere [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  Per impostazione predefinita, in [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] il controllo <xref:System.Windows.Forms.DataGrid> non si trova nella **Casella degli strumenti**.  Per ulteriori informazioni, vedere [How to: Add Items to the Toolbox](http://msdn.microsoft.com/it-it/458e119e-17fe-450b-b889-e31c128bd7e0).  
  
    > [!NOTE]
    >  I passaggi descritti di seguito non sono applicabili a [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)], dove viene utilizzata la finestra **Origini dati** per l'associazione dati in fase di progettazione.  Per ulteriori informazioni, vedere [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md) e [Procedura: visualizzare dati correlati in un'applicazione Windows Form](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md).  
  
2.  Trascinare due o più tabelle da **Esplora server** nel form.  
  
3.  Scegliere **Genera DataSet** dal menu **Dati**.  
  
4.  Impostare le relazioni tra le tabelle mediante Progettazione XML.  Per informazioni dettagliate, vedere "Procedura: creare relazioni uno\-a\-molti nei DataSet e negli schemi XML" su MSDN.  
  
5.  Salvare le relazioni scegliendo **Salva tutto** dal menu **File**.  
  
6.  Configurare il controllo <xref:System.Windows.Forms.DataGrid> che si desidera designare come griglia principale nel modo seguente:  
  
    1.  Selezionare l'oggetto <xref:System.Data.DataSet> dall'elenco a discesa della proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A>.  
  
    2.  Selezionare la tabella principale \(ad esempio, "Customers"\) dall'elenco a discesa della proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A>.  
  
7.  Configurare il controllo <xref:System.Windows.Forms.DataGrid> che si desidera designare come griglia dei dettagli nel modo seguente:  
  
    1.  Selezionare l'oggetto <xref:System.Data.DataSet> dall'elenco a discesa della proprietà <xref:System.Windows.Forms.DataGrid.DataSource%2A>.  
  
    2.  Selezionare la relazione \(ad esempio, "Customers.CustOrd"\) tra la tabella principale e la tabella dei dettagli dall'elenco a discesa della proprietà <xref:System.Windows.Forms.DataGrid.DataMember%2A>.  Per visualizzare la relazione, espandere il nodo facendo clic sul segno più \(**\+**\) accanto alla tabella master nella casella di riepilogo a discesa.  
  
## Vedere anche  
 [Controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Cenni preliminari sul controllo DataGrid](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [Procedura: associare il controllo DataGrid Windows Form a un'origine dati](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)   
 [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)