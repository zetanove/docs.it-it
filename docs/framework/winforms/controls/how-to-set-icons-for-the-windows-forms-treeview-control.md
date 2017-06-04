---
title: "Procedura: impostare icone per il controllo TreeView Windows Form | Microsoft Docs"
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
  - "icone, impostazione per il controllo TreeView"
  - "ImageList (componente) [Windows Form], aggiunta di immagini"
  - "nodi della struttura ad albero nel controllo TreeView, icone"
  - "TreeView (controllo) [Windows Form], icone di nodi"
ms.assetid: c14ddcc0-e5a6-4c21-a2d5-6799fd491781
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: impostare icone per il controllo TreeView Windows Form
Accanto a ciascun nodo è possibile che nel controllo <xref:System.Windows.Forms.TreeView> Windows Form vengano visualizzate delle icone,  posizionate a sinistra del testo del nodo.  Per visualizzarle, è necessario associare la visualizzazione struttura ad albero a un controllo <xref:System.Windows.Forms.ImageList>.  Per ulteriori informazioni sugli elenchi di immagini vedere [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) e [Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md).  
  
> [!NOTE]
>  A causa di un bug nella versione 1.1 di Microsoft .NET Framework, non è possibile visualizzare le immagini immagini nei nodi <xref:System.Windows.Forms.TreeView> quando l'applicazione chiama il metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName>.  Per ovviare a questo bug, eseguire una chiamata al metodo <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName> nel metodo `Main` immediatamente dopo la chiamata al metodo <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>.  Questo bug è stato corretto in [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)].  
  
### Per visualizzare immagini in una visualizzazione struttura ad albero  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.TreeView.ImageList%2A> appropriata del controllo <xref:System.Windows.Forms.TreeView> sul controllo <xref:System.Windows.Forms.ImageList> esistente che si desidera utilizzare.  
  
     Queste proprietà possono essere impostate nella finestra di progettazione mediante la finestra Proprietà oppure nel codice.  
  
    ```vb  
    TreeView1.ImageList = ImageList1  
  
    ```  
  
    ```csharp  
    treeView1.ImageList = imageList1;  
  
    ```  
  
    ```cpp  
    treeView1->ImageList = imageList1;  
    ```  
  
2.  Impostare le proprietà <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> e <xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> del nodo.  La proprietà <xref:System.Windows.Forms.TreeNode.ImageIndex%2A> determina l'immagine visualizzata per gli stati normale ed espanso del nodo, mentre la proprietà <xref:System.Windows.Forms.TreeNode.SelectedImageIndex%2A> determina l'immagine visualizzata per lo stato selezionato del nodo.  
  
     Queste proprietà possono essere impostate nel codice o tramite l'editor TreeNode.  Per aprire l'editor TreeNode, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.TreeView.Nodes%2A> nella finestra Proprietà.  
  
    ```vb  
    ' (Assumes that ImageList1 contains at least two images and  
    ' the TreeView control contains a selected image.)  
    TreeView1.SelectedNode.ImageIndex = 0  
    TreeView1.SelectedNode.SelectedImageIndex = 1  
  
    ```  
  
    ```csharp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1.SelectedNode.ImageIndex = 0;  
    treeView1.SelectedNode.SelectedImageIndex = 1;  
  
    ```  
  
    ```cpp  
    // (Assumes that imageList1 contains at least two images and  
    // the TreeView control contains a selected image.)  
    treeView1->SelectedNode->ImageIndex = 0;  
    treeView1->SelectedNode->SelectedImageIndex = 1;  
    ```  
  
## Vedere anche  
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)   
 [Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [Procedura: individuare il nodo di TreeView scelto](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)