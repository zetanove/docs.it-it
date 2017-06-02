---
title: "Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form | Microsoft Docs"
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
  - "nodi della struttura ad albero nel controllo TreeView, iterazione"
  - "TreeView (controllo) [Windows Form], iterazione tramite nodi"
ms.assetid: 427f8928-ebcf-4beb-887f-695b905d5134
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form
A volte è utile esaminare tutti i nodi in un controllo <xref:System.Windows.Forms.TreeView>Windows Form per eseguire determinati calcoli sui valori del nodo.  Tale operazione può essere effettuata utilizzando una routine ricorsiva \(metodo ricorsivo in C\# e C\+\+\) per scorrere ciascun nodo in ogni raccolta della struttura ad albero.  
  
 Ciascun oggetto <xref:System.Windows.Forms.TreeNode> di una visualizzazione struttura ad albero supporta proprietà che consentono di esplorarla: <xref:System.Windows.Forms.TreeNode.FirstNode%2A>, <xref:System.Windows.Forms.TreeNode.LastNode%2A>, <xref:System.Windows.Forms.TreeNode.NextNode%2A>, <xref:System.Windows.Forms.TreeNode.PrevNode%2A> e <xref:System.Windows.Forms.TreeNode.Parent%2A>.  Il valore della proprietà <xref:System.Windows.Forms.TreeNode.Parent%2A> è il nodo padre del nodo corrente.  I nodi figlio del nodo corrente, se presenti, sono elencati nella relativa proprietà <xref:System.Windows.Forms.TreeNode.Nodes%2A>.  Lo stesso controllo <xref:System.Windows.Forms.TreeView> dispone della proprietà <xref:System.Windows.Forms.TreeView.TopNode%2A>, che è il nodo radice dell'intera visualizzazione struttura ad albero.  
  
### Per scorrere tutti i nodi del controllo TreeView  
  
1.  Creare una routine ricorsiva \(metodo ricorsivo in C\# e C\+\+\) per eseguire il test di ciascun nodo.  
  
2.  Chiamare la routine.  
  
     Nell'esempio qui di seguito è illustrato come stampare ogni proprietà <xref:System.Windows.Forms.TreeNode.Text%2A> dell'oggetto <xref:System.Windows.Forms.TreeNode>:  
  
    ```vb  
    Private Sub PrintRecursive(ByVal n As TreeNode)  
       System.Diagnostics.Debug.WriteLine(n.Text)  
       MessageBox.Show(n.Text)  
       Dim aNode As TreeNode  
       For Each aNode In n.Nodes  
          PrintRecursive(aNode)  
       Next  
    End Sub  
  
    ' Call the procedure using the top nodes of the treeview.  
    Private Sub CallRecursive(ByVal aTreeView As TreeView)  
       Dim n As TreeNode  
       For Each n In aTreeView.Nodes  
          PrintRecursive(n)  
       Next  
    End Sub  
  
    ```  
  
    ```csharp  
    private void PrintRecursive(TreeNode treeNode)  
    {  
       // Print the node.  
       System.Diagnostics.Debug.WriteLine(treeNode.Text);  
       MessageBox.Show(treeNode.Text);  
       // Print each node recursively.  
       foreach (TreeNode tn in treeNode.Nodes)  
       {  
          PrintRecursive(tn);  
       }  
    }  
  
    // Call the procedure using the TreeView.  
    private void CallRecursive(TreeView treeView)  
    {  
       // Print each node recursively.  
       TreeNodeCollection nodes = treeView.Nodes;  
       foreach (TreeNode n in nodes)  
       {  
          PrintRecursive(n);  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void PrintRecursive( TreeNode^ treeNode )  
       {  
          // Print the node.  
          System::Diagnostics::Debug::WriteLine( treeNode->Text );  
          MessageBox::Show( treeNode->Text );  
  
          // Print each node recursively.  
          System::Collections::IEnumerator^ myNodes = (safe_cast<System::Collections::IEnumerable^>(treeNode->Nodes))->GetEnumerator();  
          try  
          {  
             while ( myNodes->MoveNext() )  
             {  
                TreeNode^ tn = safe_cast<TreeNode^>(myNodes->Current);  
                PrintRecursive( tn );  
             }  
          }  
          finally  
          {  
             IDisposable^ disposable = dynamic_cast<System::IDisposable^>(myNodes);  
             if ( disposable != nullptr )  
                      disposable->Dispose();  
          }  
       }  
  
       // Call the procedure using the TreeView.  
       void CallRecursive( TreeView^ treeView )  
       {  
          // Print each node recursively.  
          TreeNodeCollection^ nodes = treeView->Nodes;  
          System::Collections::IEnumerator^ myNodes = (safe_cast<System::Collections::IEnumerable^>(nodes))->GetEnumerator();  
          try  
          {  
             while ( myNodes->MoveNext() )  
             {  
                TreeNode^ n = safe_cast<TreeNode^>(myNodes->Current);  
                PrintRecursive( n );  
             }  
          }  
          finally  
          {  
             IDisposable^ disposable = dynamic_cast<System::IDisposable^>(myNodes);  
             if ( disposable != nullptr )  
                      disposable->Dispose();  
          }  
       }  
    ```  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Recursive Procedures](../Topic/Recursive%20Procedures%20\(Visual%20Basic\).md)