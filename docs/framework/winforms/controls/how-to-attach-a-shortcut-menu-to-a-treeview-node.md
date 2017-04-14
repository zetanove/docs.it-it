---
title: "Procedura: associare un menu di scelta rapida a un nodo di TreeView | Microsoft Docs"
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
  - "menu di scelta rapida, aggiunta al controllo TreeView"
  - "nodi della struttura ad albero nel controllo TreeView, menu di scelta rapida"
  - "TreeView (controllo) [Windows Form], aggiunta a menu di scelta rapida"
ms.assetid: a23c6752-fd8f-44ad-b781-bab37962fc7c
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: associare un menu di scelta rapida a un nodo di TreeView
Il controllo <xref:System.Windows.Forms.TreeView> Windows Form consente di visualizzare una gerarchia di nodi, nello stesso modo in cui file e cartelle vengono visualizzati nel riquadro sinistro di Esplora risorse.  Se si imposta la proprietà <xref:System.Windows.Forms.Control.ContextMenuStrip%2A>, è possibile fornire all'utente operazioni sensibili al contesto per la selezione con il pulsante destro del mouse del controllo <xref:System.Windows.Forms.TreeView>.  Se si associa un componente <xref:System.Windows.Forms.ContextMenuStrip> a singoli elementi <xref:System.Windows.Forms.TreeNode>, è possibile aggiungere un livello personalizzato di funzionalità del menu di scelta rapida ai controlli <xref:System.Windows.Forms.TreeView>.  
  
### Per associare un menu di scelta rapida a un TreeNode a livello di codice  
  
1.  Creare un'istanza di un controllo <xref:System.Windows.Forms.TreeView> con le impostazioni appropriate delle proprietà, creare un <xref:System.Windows.Forms.TreeNode> di primo livello e aggiungere sottonodi.  
  
2.  Creare un'istanza di un componente <xref:System.Windows.Forms.ContextMenuStrip>, quindi aggiungere una classe <xref:System.Windows.Forms.ToolStripMenuItem> per ogni operazione che si desidera rendere disponibile in fase di esecuzione.  
  
3.  Impostare la proprietà <xref:System.Windows.Forms.TreeNode.ContextMenuStrip%2A> del <xref:System.Windows.Forms.TreeNode> appropriato sul menu di scelta rapida creato.  
  
4.  Quando la proprietà è impostata, il menu di scelta rapida viene visualizzato se si fa clic con il pulsante destro del mouse sul nodo.  
  
 Nell'esempio di codice riportato di seguito vengono creati gli oggetti <xref:System.Windows.Forms.TreeView> e <xref:System.Windows.Forms.ContextMenuStrip> di base associati all'oggetto <xref:System.Windows.Forms.TreeNode> di primo livello del controllo <xref:System.Windows.Forms.TreeView>.  Personalizzare le opzioni di menu in base a quelle necessarie per il controllo <xref:System.Windows.Forms.TreeView> sviluppato.  Potrebbe inoltre essere necessario scrivere il codice per gestire gli eventi <xref:System.Windows.Forms.ToolStripItem.Click> per tali voci di menu.  
  
 [!code-cpp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/cpp/Form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.TreeNodeContextMenuStrip#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/system.windows.forms.TreeNodeContextMenuStrip/VB/Form1.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContextMenuStrip>   
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)