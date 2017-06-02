---
title: "Procedura: individuare il nodo di TreeView scelto (Windows Form) | Microsoft Docs"
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
  - "TreeNode"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "esempi [Windows Form], TreeView (controllo)"
  - "nodi della struttura ad albero nel controllo TreeView, rilevamento nodo selezionato"
  - "TreeView (controllo) [Windows Form], rilevamento nodo selezionato"
ms.assetid: 06a4a191-d918-42af-9f49-956c93eff261
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: individuare il nodo di TreeView scelto (Windows Form)
Quando si utilizza il controllo <xref:System.Windows.Forms.TreeView> Windows Form, un'attività comune consiste nello stabilire quale nodo è stato scelto e nel fornire la risposta appropriata.  
  
### Per stabilire il nodo di TreeView scelto  
  
1.  Utilizzare l'oggetto <xref:System.EventArgs> per restituire un riferimento all'oggetto nodo scelto.  
  
2.  Per determinare il nodo scelto, verificare la classe <xref:System.Windows.Forms.TreeViewEventArgs>, che contiene i dati relativi all'evento.  
  
    ```vb  
    Private Sub TreeView1_AfterSelect(ByVal sender As System.Object, _  
    ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       ' Determine by checking the Node property of the TreeViewEventArgs.  
       MessageBox.Show(e.Node.Text)  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,   
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       // Determine by checking the Text property.  
       MessageBox.Show(e.Node.Text);  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          // Determine by checking the Text property.  
          MessageBox::Show(e->Node->Text);  
       }  
    ```  
  
    > [!NOTE]
    >  In alternativa è possibile utilizzare l'argomento <xref:System.Windows.Forms.MouseEventArgs> dell'evento <xref:System.Windows.Forms.Control.MouseDown> o <xref:System.Windows.Forms.Control.MouseUp> per ottenere i valori delle coordinate <xref:System.Drawing.Point.X%2A> e <xref:System.Drawing.Point.Y%2A> dell'oggetto <xref:System.Drawing.Point> in cui è stato fatto clic.  Utilizzare quindi il metodo <xref:System.Windows.Forms.TreeView.GetNodeAt%2A> del controllo <xref:System.Windows.Forms.TreeView> per determinare il nodo scelto.  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)