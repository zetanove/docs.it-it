---
title: "Procedura: aggiungere pulsanti a un controllo ToolBar mediante la finestra di progettazione | Microsoft Docs"
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
  - "esempi [Windows Form], barre degli strumenti"
  - "ToolBar (controllo) [Windows Form], aggiunta di pulsanti"
  - "ToolBar (controllo) [Windows Form], aggiunta di menu a discesa"
  - "ToolBar (controllo) [Windows Form], aggiunta di separatori"
  - "barre degli strumenti [Windows Form], aggiunta di pulsanti"
ms.assetid: d9ce3040-3e21-4e2d-80ae-b430982b2db8
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: aggiungere pulsanti a un controllo ToolBar mediante la finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo <xref:System.Windows.Forms.ToolBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Una parte integrante del controllo <xref:System.Windows.Forms.ToolBar> è costituita dai pulsanti che vi vengono aggiunti.  Questi pulsanti possono essere utilizzati per semplificare l'accesso ai comandi di menu oppure possono essere posizionati in un'altra area dell'interfaccia utente dell'applicazione per esporre agli utenti i comandi che non sono disponibili nella struttura di menu.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.ToolBar>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere pulsanti in fase di progettazione  
  
1.  Fare clic sul controllo <xref:System.Windows.Forms.ToolBar>.  
  
2.  Nella finestra **Proprietà** fare clic sulla proprietà <xref:System.Windows.Forms.ToolBar.Buttons%2A> per selezionarla, quindi fare clic sul pulsante con i **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per aprire l'**Editor della raccolta ToolBarButton**.  
  
3.  Utilizzare i pulsanti **Aggiungi** e **Rimuovi** per aggiungere e rimuovere pulsanti dal controllo <xref:System.Windows.Forms.ToolBar>.  
  
4.  Configurare le proprietà dei singoli pulsanti nella finestra **Proprietà** visualizzata nel riquadro sul lato destro dell'editor.  Nella tabella riportata di seguito sono indicate alcune importanti proprietà di cui tenere conto.  
  
    |Proprietà|Descrizione|  
    |---------------|-----------------|  
    |<xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A>|Imposta il menu da visualizzare nel pulsante a discesa della barra degli strumenti.  La proprietà <xref:System.Windows.Forms.ToolBarButton.Style%2A> del pulsante della barra degli strumenti deve essere impostata su <xref:System.Windows.Forms.ToolBarButtonStyle>.  Questa proprietà accetta un'istanza della classe <xref:System.Windows.Forms.ContextMenu> come riferimento.|  
    |<xref:System.Windows.Forms.ToolBarButton.PartialPush%2A>|Imposta se un pulsante della barra degli strumenti per l'attivazione\/disattivazione dello stile è parzialmente premuto.  La proprietà <xref:System.Windows.Forms.ToolBarButton.Style%2A> del pulsante della barra degli strumenti deve essere impostata su <xref:System.Windows.Forms.ToolBarButtonStyle>.|  
    |<xref:System.Windows.Forms.ToolBarButton.Pushed%2A>|Imposta se un pulsante di barra degli strumenti per l'attivazione\/disattivazione dello stile è attualmente premuto.  La proprietà <xref:System.Windows.Forms.ToolBarButton.Style%2A> del pulsante della barra degli strumenti deve essere impostata su <xref:System.Windows.Forms.ToolBarButtonStyle> o <xref:System.Windows.Forms.ToolBarButtonStyle>.|  
    |<xref:System.Windows.Forms.ToolBarButton.Style%2A>|Imposta lo stile del pulsante della barra degli strumenti.  Deve essere uno dei valori dell'enumerazione <xref:System.Windows.Forms.ToolBarButtonStyle>.|  
    |<xref:System.Windows.Forms.ToolBarButton.Text%2A>|Stringa di testo visualizzata dal pulsante.|  
    |<xref:System.Windows.Forms.ToolBarButton.ToolTipText%2A>|Testo visualizzato come una descrizione comando per il pulsante.|  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo e creare i pannelli specificati.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolBar>   
 [Procedura: definire un'icona per un pulsante ToolBar](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [Cenni preliminari sul controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-overview-windows-forms.md)   
 [Controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)