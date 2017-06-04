---
title: "Procedura: utilizzare descrizioni comandi nei controlli ToolStrip | Microsoft Docs"
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
  - "barre degli strumenti [Windows Form], aggiunta di descrizioni comandi"
  - "ToolStrip (controllo) [Windows Form], aggiunta di descrizioni comandi"
  - "descrizioni comandi [Windows Form], aggiunta"
ms.assetid: c5d86024-a7c5-44ee-8b3f-2daf53d80d3e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: utilizzare descrizioni comandi nei controlli ToolStrip
È possibile visualizzare una classe <xref:System.Windows.Forms.ToolTip> per il controllo <xref:System.Windows.Forms.ToolStrip> desiderato impostando la proprietà <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> del controllo su `true`.  
  
### Per visualizzare una descrizione comando  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> del controllo su `true`.  
  
     Il valore predefinito di <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A?displayProperty=fullName> è `true` e il valore predefinito di <xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A?displayProperty=fullName> e <xref:System.Windows.Forms.StatusStrip.ShowItemToolTips%2A?displayProperty=fullName> è `false`.  
  
### Per utilizzare la proprietà ToolTipText per il testo della descrizione comando di un ToolStripButton  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A> del pulsante su `true`.  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripButton.AutoToolTip%2A?displayProperty=fullName> del pulsante su `false`.  
  
     Per impostazione predefinita la proprietà `AutoToolTip` è `true` per <xref:System.Windows.Forms.ToolStripButton>, <xref:System.Windows.Forms.ToolStripDropDownButton> e <xref:System.Windows.Forms.ToolStripSplitButton>.  
  
     Una classe <xref:System.Windows.Forms.ToolStripButton> utilizza la proprietà `Text` per il testo della classe <xref:System.Windows.Forms.ToolTip> per impostazione predefinita.  Utilizzare questa procedura per visualizzare testo personalizzato in una classe <xref:System.Windows.Forms.ToolTip> di una classe <xref:System.Windows.Forms.ToolStripButton>.  
  
> [!NOTE]
>  Se si imposta <xref:System.Windows.Forms.ToolStripItemDisplayStyle> su <xref:System.Windows.Forms.ToolStripItemDisplayStyle> o su <xref:System.Windows.Forms.ToolStripItemDisplayStyle>, sul pulsante non verrà visualizzato alcun testo ma la descrizione comando verrà visualizzata ugualmente.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip.ShowItemToolTips%2A>   
 <xref:System.Windows.Forms.ToolStripButton>   
 <xref:System.Windows.Forms.ToolStripDropDownButton>   
 <xref:System.Windows.Forms.ToolStripSplitButton>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)