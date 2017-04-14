---
title: "Procedura: aggiungere elementi ToolStrip dinamicamente | Microsoft Docs"
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
  - "ContextMenuStrip (controllo) [Windows Form]"
  - "barre degli strumenti [Windows Form], aggiunta dinamica di elementi"
  - "ToolStrip (controllo) [Windows Form]"
ms.assetid: 0e8dea56-5f46-408b-914d-7e360341a234
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: aggiungere elementi ToolStrip dinamicamente
È possibile popolare in modo dinamico la raccolta di voci di menu di un controllo <xref:System.Windows.Forms.ToolStrip> quando si apre il menu.  
  
## Esempio  
 L'esempio di codice seguente illustra come aggiungere voci in modo dinamico a un controllo <xref:System.Windows.Forms.ContextMenuStrip>.  L'esempio mostra anche come riutilizzare lo stesso oggetto <xref:System.Windows.Forms.ContextMenuStrip> per tre diversi controlli nel form.  
  
 Nell'esempio, un gestore eventi <xref:System.Windows.Forms.ToolStripDropDown.Opening> popola la raccolta di voci di menu.  Il gestore eventi <xref:System.Windows.Forms.ToolStripDropDown.Opening> esamina le proprietà <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A?displayProperty=fullName> e <xref:System.Windows.Forms.ToolStripItem.OwnerItem%2A?displayProperty=fullName> e aggiunge un oggetto <xref:System.Windows.Forms.ToolStripItem> che descrive il controllo del codice sorgente.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#40)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#40)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Riferimenti agli assembly System.Drawing e System.Windows.Forms.  
  
 Per informazioni sulla compilazione di questo esempio dalla riga di comando per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], vedere [Compilazione dalla riga di comando](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilazione dalla riga di comando con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  È anche possibile compilare questo esempio in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] incollando il codice in un nuovo progetto.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 <xref:System.Windows.Forms.ToolStripDropDownButton>   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)