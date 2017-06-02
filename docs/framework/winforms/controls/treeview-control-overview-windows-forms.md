---
title: "Cenni preliminari sul controllo TreeView (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "TreeView"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "TreeView (controllo) [Windows Form], informazioni sul controllo TreeView"
ms.assetid: 0ece823a-9508-478a-bbdb-7d7c3bae51d5
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sul controllo TreeView (Windows Form)
Il controllo <xref:System.Windows.Forms.TreeView> di Windows Form consente di visualizzare una gerarchia di nodi, nello stesso modo in cui file e cartelle vengono visualizzati nel riquadro sinistro della funzionalità Esplora risorse in un sistema operativo Windows.  Ciascun nodo della struttura può contenere altri nodi, denominati *nodi figlio*.  I nodi padre, o i nodi che contengono i nodi figlio, possono essere visualizzati in forma espansa o compressa.  Nella visualizzazione struttura ad albero, accanto ai nodi possono essere presenti anche caselle di controllo se la proprietà <xref:System.Windows.Forms.TreeView.CheckBoxes%2A> della visualizzazione struttura ad albero viene impostata su `true`.  È quindi possibile selezionare o cancellare i nodi a livello di codice impostando la proprietà <xref:System.Windows.Forms.TreeNode.Checked%2A> del nodo su `true` o `false`.  
  
## Proprietà chiave  
 Le proprietà chiave del controllo <xref:System.Windows.Forms.TreeView> sono <xref:System.Windows.Forms.TreeView.Nodes%2A> e <xref:System.Windows.Forms.TreeView.SelectedNode%2A>.  La proprietà <xref:System.Windows.Forms.TreeView.Nodes%2A> contiene l'elenco dei nodi di primo livello nella visualizzazione struttura ad albero.  La proprietà <xref:System.Windows.Forms.TreeView.SelectedNode%2A> consente di impostare il nodo attualmente selezionato.  Accanto ai nodi è possibile visualizzare icone.  Il controllo usa le immagini della classe <xref:System.Windows.Forms.ImageList> indicate nella proprietà <xref:System.Windows.Forms.TreeView.ImageList%2A> della visualizzazione struttura ad albero.  La proprietà <xref:System.Windows.Forms.TreeView.ImageIndex%2A> consente di impostare l'immagine predefinita per i nodi nella visualizzazione struttura ad albero.  Per altre informazioni sulla visualizzazione delle immagini, vedere [Procedura: impostare icone per il controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md).  Se si usa [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)], è disponibile un'ampia libreria di immagini standard da usare con il controllo <xref:System.Windows.Forms.TreeView>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TreeView>   
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Procedura: impostare icone per il controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md)   
 [Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)   
 [Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [Procedura: individuare il nodo di TreeView scelto](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)