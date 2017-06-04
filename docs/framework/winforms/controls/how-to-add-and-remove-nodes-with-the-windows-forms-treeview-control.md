---
title: "Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form | Microsoft Docs"
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
  - "esempi [Windows Form], TreeView (controllo)"
  - "nodi della struttura ad albero nel controllo TreeView"
  - "TreeView (controllo) [Windows Form], aggiunta di nodi"
  - "TreeView (controllo) [Windows Form], rimozione di nodi"
ms.assetid: de1b82db-4905-449a-9f59-af271a6b6673
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form
Il controllo <xref:System.Windows.Forms.TreeView> di Windows Forms archivia i nodi di livello superiore nella raccolta <xref:System.Windows.Forms.TreeView.Nodes%2A>.  Ogni controllo <xref:System.Windows.Forms.TreeNode> dispone inoltre della raccolta <xref:System.Windows.Forms.TreeNode.Nodes%2A> per archiviare i nodi figlio.  Le proprietà di entrambi le raccolte sono di tipo <xref:System.Windows.Forms.TreeNodeCollection> che fornisce membri della raccolta standard consentendo di aggiungere, rimuovere e ridisporre i nodi a un solo livello della gerarchia di nodi.  
  
### Per aggiungere nodi a livello di codice  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.TreeNodeCollection.Add%2A> della proprietà <xref:System.Windows.Forms.TreeView.Nodes%2A> della visualizzazione struttura ad albero.  
  
    ```vb  
    ' Adds new node as a child node of the currently selected node.  
    Dim newNode As TreeNode = New TreeNode("Text for new node")  
    TreeView1.SelectedNode.Nodes.Add(newNode)  
  
    ```  
  
    ```csharp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode newNode = new TreeNode("Text for new node");  
    treeView1.SelectedNode.Nodes.Add(newNode);  
  
    ```  
  
    ```cpp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode ^ newNode = new TreeNode("Text for new node");  
    treeView1->SelectedNode->Nodes->Add(newNode);  
    ```  
  
### Per rimuovere nodi a livello di codice  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.TreeNodeCollection.Remove%2A> della proprietà <xref:System.Windows.Forms.TreeView.Nodes%2A> della visualizzazione struttura ad albero per rimuovere un singolo nodo oppure il metodo <xref:System.Windows.Forms.TreeNodeCollection.Clear%2A> per cancellarli tutti.  
  
    ```vb  
    ' Removes currently selected node, or root if nothing is selected.  
    TreeView1.Nodes.Remove(TreeView1.SelectedNode)  
    ' Clears all nodes.  
    TreeView1.Nodes.Clear()  
  
    ```  
  
    ```csharp  
    // Removes currently selected node, or root if nothing   
    // is selected.  
    treeView1.Nodes.Remove(treeView1.SelectedNode);  
    // Clears all nodes.  
    TreeView1.Nodes.Clear();  
  
    ```  
  
    ```cpp  
    // Removes currently selected node, or root if nothing  
    // is selected.  
    treeView1->Nodes->Remove(treeView1->SelectedNode);  
    // Clears all nodes.  
    treeView1->Nodes->Clear();  
    ```  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [Procedura: impostare icone per il controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md)   
 [Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [Procedura: individuare il nodo di TreeView scelto](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)