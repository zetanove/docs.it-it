---
title: "Procedura: definire un&#39;icona per un pulsante di una barra degli strumenti mediante la finestra di progettazione | Microsoft Docs"
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
  - "pulsanti [Windows Form], immagini"
  - "esempi [Windows Form], barre degli strumenti"
  - "icone [Windows Form], pulsanti della barra degli strumenti"
  - "immagini [Windows Form], pulsanti della barra degli strumenti"
  - "ToolBar (controllo) [Windows Form], aggiunta di icone a pulsanti"
  - "barre degli strumenti [Windows Form], aggiunta di icone a pulsanti"
ms.assetid: d848f38e-67f2-49d4-8e88-01c845c06c02
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: definire un&#39;icona per un pulsante di una barra degli strumenti mediante la finestra di progettazione
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo <xref:System.Windows.Forms.ToolBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 I pulsanti <xref:System.Windows.Forms.ToolBar> consentono di visualizzare icone al loro interno per semplificarne l'identificazione da parte degli utenti.  Questo risultato viene conseguito aggiungendo immagini al componente <xref:System.Windows.Forms.ImageList> e associando tale componente al controllo <xref:System.Windows.Forms.ToolBar>.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.ToolBar> e un componente <xref:System.Windows.Forms.ImageList>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare un'icona per un pulsante di una barra degli strumenti in fase di progettazione  
  
1.  Aggiungere le immagini al componente <xref:System.Windows.Forms.ImageList>.  Per ulteriori informazioni, vedere [Procedura: aggiungere o rimuovere immagini ImageList con la finestra di progettazione](../../../../docs/framework/winforms/controls/how-to-add-or-remove-imagelist-images-with-the-designer.md).  
  
2.  Selezionare il controllo <xref:System.Windows.Forms.ToolBar> nel form.  
  
3.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.ToolBar.ImageList%2A> del controllo <xref:System.Windows.Forms.ToolBar> sul componente <xref:System.Windows.Forms.ImageList>.  
  
4.  Fare clic sulla proprietà <xref:System.Windows.Forms.ToolBar.Buttons%2A> del controllo <xref:System.Windows.Forms.ToolBar> per selezionarla, quindi fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) per aprire l'**Editor della raccolta ToolBarButton**.  
  
5.  Utilizzare il pulsante **Aggiungi** per aggiungere pulsanti al controllo <xref:System.Windows.Forms.ToolBar>.  
  
6.  Nella finestra **Proprietà** visualizzata nel riquadro sul lato destro dell'**Editor della raccolta ToolBarButton**, impostare la proprietà <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> di ciascun pulsante della barra degli strumenti su uno dei valori presenti nell'elenco basato sulle immagini aggiunte al componente <xref:System.Windows.Forms.ImageList>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolBar>   
 [Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [Controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)