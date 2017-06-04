---
title: "Procedura: impostare lo sfondo di un controllo Panel Windows Form mediante la finestra di progettazione | Microsoft Docs"
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
  - "colori di sfondo, controlli Panel Windows Form"
  - "immagini di sfondo, controlli Panel Windows Form"
  - "colori, controlli Panel Windows Form"
  - "Panel (controllo) [Windows Form], sfondo"
ms.assetid: db83cf54-3c69-4b08-ac6c-25b9b5abb1b0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: impostare lo sfondo di un controllo Panel Windows Form mediante la finestra di progettazione
Un controllo <xref:System.Windows.Forms.Panel> Windows Form consente di visualizzare sia un colore di sfondo che un'immagine di sfondo.  La proprietà <xref:System.Windows.Forms.Control.BackColor%2A> imposta il colore di sfondo per i controlli contenuti nel pannello, ad esempio etichette e pulsanti di opzione.  Se la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> non è impostata, tutto il pannello verrà riempito dalla selezione <xref:System.Windows.Forms.Control.BackColor%2A>.  Se la proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A> è impostata, l'immagine verrà visualizzata dietro i controlli contenuti nel pannello.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.Panel>.  Per informazioni su come impostare tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per impostare lo sfondo in Progettazione Windows Form  
  
1.  Fare clic sul controllo <xref:System.Windows.Forms.Panel>.  
  
2.  Nella finestra **Proprietà** fare clic sul pulsante freccia accanto alla proprietà <xref:System.Windows.Forms.Control.BackColor%2A> per visualizzare una finestra con tre schede.  
  
3.  Fare clic sulla scheda **Personalizzato** per visualizzare una tavolozza di colori.  
  
4.  Fare clic sulla scheda **Web** o sulla scheda **Sistema** per visualizzare un elenco di nomi predefiniti per i colori, quindi scegliere un colore.  
  
5.  Nella finestra **Proprietà** fare clic sul pulsante freccia accanto alla proprietà <xref:System.Windows.Forms.Control.BackgroundImage%2A>.  
  
6.  Nella finestra di dialogo **Apri** selezionare il file che si desidera visualizzare.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.BackColor%2A>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>   
 [Controllo Panel](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Cenni preliminari sul controllo Panel](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [Procedura: raggruppare i controlli con il controllo Panel di Windows Form nella finestra di progettazione](../../../../docs/framework/winforms/controls/group-controls-with-wf-panel-control-using-the-designer.md)