---
title: "Procedura: gestire l&#39;evento di apertura ContextMenuStrip | Microsoft Docs"
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
  - "menu di scelta rapida, gestione eventi"
  - "ContextMenuStrip (controllo) [Windows Form]"
  - "gestione eventi, menu di scelta rapida"
  - "menu di scelta rapida, gestione eventi"
  - "ToolStrip (controllo) [Windows Form]"
ms.assetid: b661b3dd-7815-4cc2-a1aa-a9a391ab3427
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: gestire l&#39;evento di apertura ContextMenuStrip
Il comportamento del controllo <xref:System.Windows.Forms.ContextMenuStrip> può essere personalizzato mediante la gestione dell'evento <xref:System.Windows.Forms.ToolStripDropDown.Opening>.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come gestire l'evento <xref:System.Windows.Forms.ToolStripDropDown.Opening>.  Il gestore eventi aggiunge elementi a un controllo <xref:System.Windows.Forms.ContextMenuStrip> in modo dinamico.  Per l'esempio di codice completo, vedere [Procedura: aggiungere elementi ToolStrip dinamicamente](../../../../docs/framework/winforms/controls/how-to-add-toolstrip-items-dynamically.md).  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#42)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#42)]  
  
 Impostare la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A?displayProperty=fullName> su `true` per impedire l'apertura del menu.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A>   
 <xref:System.Windows.Forms.ToolStripDropDown>   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)