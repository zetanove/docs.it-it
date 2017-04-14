---
title: "Procedura: spostare ToolStrip da ToolStripContainer a un form | Microsoft Docs"
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
  - "ToolStrip (controllo) [Windows Form], relazione padre-figlio con i form"
  - "Windows Form, relazione padre-figlio tra ToolStrip (controlli)"
ms.assetid: a1c94a7f-6fc5-4e4c-84cf-ff11dc573d33
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: spostare ToolStrip da ToolStripContainer a un form
Utilizzare la seguente procedura per spostare un <xref:System.Windows.Forms.ToolStrip> da <xref:System.Windows.Forms.ToolStripContainer> in un form.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per spostare ToolStrip da ToolStripContainer a un form  
  
1.  Selezionare <xref:System.Windows.Forms.ToolStrip>.  
  
2.  Tagliare <xref:System.Windows.Forms.ToolStrip> premendo CTRL \+ X o facendo clic con il tasto destro del mouse su <xref:System.Windows.Forms.ToolStrip> e scegliendo **Taglia** dal menu di scelta rapida.  
  
3.  Selezionare il form.  
  
4.  Incollare <xref:System.Windows.Forms.ToolStrip> premendo CTRL \+ V oppure scegliendo **Incolla** dal menu **Modifica**.  
  
5.  Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.Dock%2A> del controllo <xref:System.Windows.Forms.ToolStrip> su **Superiore**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripContainer>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)