---
title: "How to: Disable Adding and Deleting DataRepeater Items (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, disabling delete"
  - "DataRepeater, disabling add"
ms.assetid: 298d8f60-ddfe-4361-ab66-cf76d0df5220
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# How to: Disable Adding and Deleting DataRepeater Items (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per impostazione predefinita, gli utenti possono aggiungere ed eliminare elementi in un controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  Per aggiungere un nuovo elemento, premere CTRL\+N quando <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItemEventArgs.DataRepeaterItem%2A> ha lo stato attivo o fare clic sul pulsante **AddNewItem** sul controllo <xref:System.Windows.Forms.BindingNavigator>.  Per eliminare un elemento, premere CANC quando <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItemEventArgs.DataRepeaterItem%2A> ha lo stato attivo o fare clic sul pulsante **DeleteItem** sul controllo <xref:System.Windows.Forms.BindingNavigator>.  
  
 È possibile disabilitare l'aggiunta e\/o la rimozione di elementi in fase di progettazione o in fase di esecuzione.  
  
### Per disabilitare l'aggiunta e l'eliminazione in fase di progettazione  
  
1.  In Progettazione Windows Form selezionare il controllo <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
    > [!NOTE]
    >  Selezionare l'area inferiore del controllo.  Selezionando l'area del modello di elemento, verrà visualizzato un diverso insieme di proprietà.  
  
2.  Nella finestra Proprietà, impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.AllowUserToAddItems%2A> su **False**.  
  
3.  Impostare la proprietà <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.AllowUserToDeleteItems%2A> su **False**.  
  
4.  In Progettazione Windows Form, selezionare il controllo <xref:System.Windows.Forms.BindingNavigator>, quindi fare clic sul pulsante **AddNewItem** \(contrassegnato da un segno più\).  
  
5.  Nella finestra Proprietà, impostare la proprietà <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> su **False**.  
  
6.  In Progettazione Windows Form, selezionare il controllo <xref:System.Windows.Forms.BindingNavigator>, quindi fare clic sul pulsante **DeleteItem** \(contrassegnato da una X rossa\).  
  
7.  Nella finestra Proprietà, impostare la proprietà <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> su **False**.  
  
8.  Nella Barra dei componenti, selezionare l'oggetto <xref:System.Windows.Forms.BindingSource> con associazione a <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>.  
  
9. Nella finestra Proprietà, impostare la proprietà <xref:System.Windows.Forms.BindingSource.AllowNew%2A> su **False**.  
  
10. In Progettazione Windows Form, fare doppio clic sul pulsante **DeleteItem** per aprire l'editor di codice.  
  
11. Nell'elenco a discesa Eventi, selezionare l'evento `BindingNavigatorDeleteItem_EnabledChanged`.  
  
12. Aggiungere il codice seguente al gestore eventi `BindingNavigatorDeleteItem_EnabledChanged`:  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DisableAddDeleteCS/DisableAddDelete.cs#1)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/vbpowerpacksdatarepeaterdisableadddelete/form1.vb#1)]  
  
    > [!NOTE]
    >  Questo passaggio è necessario in quanto <xref:System.Windows.Forms.BindingSource> attiva il pulsante **DeleteItem** ogni volta che vengono apportate modifiche al record corrente.  
  
### Per disabilitare l'aggiunta e l'eliminazione in fase di esecuzione  
  
1.  In Progettazione Windows Form, fare doppio clic sul form per aprire l'editor di codice.  
  
2.  Aggiungere all'evento `Form_Load` il codice seguente:  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DisableAddDeleteCS/DisableAddDelete.cs#2)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/vbpowerpacksdatarepeaterdisableadddelete/form1.vb#2)]  
  
3.  Aggiungere il codice seguente al gestore eventi `BindingNavigatorDeleteItem_EnabledChanged`:  
  
     [!code-cs[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/csharp/DisableAddDeleteCS/DisableAddDelete.cs#1)]
     [!code-vb[VbPowerPacksDataRepeaterDisableAddDelete#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/visualbasic/vbpowerpacksdatarepeaterdisableadddelete/form1.vb#1)]  
  
    > [!NOTE]
    >  Questo passaggio è necessario in quanto <xref:System.Windows.Forms.BindingSource> attiva il pulsante **DeleteItem** ogni volta che vengono apportate modifiche al record corrente.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [Introduction to the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [Troubleshooting the DataRepeater Control](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)