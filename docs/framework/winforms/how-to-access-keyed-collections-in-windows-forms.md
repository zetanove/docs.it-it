---
title: "How to: Access Keyed Collections in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "keyed collections [Windows Forms]"
  - "collections, accessing with keys"
ms.assetid: b9b79b8b-d9bf-4f8c-b9d6-9578bc3219d3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Access Keyed Collections in Windows Forms
-   È possibile accedere ai singoli elementi di una raccolta tramite chiave.  Questa funzionalità è stata aggiunta a molte classi di raccolte che vengono in genere utilizzate dalle applicazioni Windows Form.  Nell'elenco seguente sono illustrate alcune classi di raccolte che contengono raccolte con chiavi accessibili:  
  
-   <xref:System.Windows.Forms.ListView.ListViewItemCollection>  
  
-   <xref:System.Windows.Forms.ListViewItem.ListViewSubItemCollection>  
  
-   <xref:System.Windows.Forms.Control.ControlCollection>  
  
-   <xref:System.Windows.Forms.TabControl.TabPageCollection>  
  
-   <xref:System.Windows.Forms.TreeNodeCollection>  
  
 La chiave associata a un elemento di una raccolta corrisponde in genere al nome dell'elemento.  Nelle procedure seguenti viene illustrato come utilizzare le classi di raccolte per eseguire attività comuni.  
  
### Per trovare un controllo annidato in una raccolta di controlli e portarlo allo stato attivo  
  
-   Utilizzare i metodi <xref:System.Windows.Forms.Control.ControlCollection.Find%2A> e <xref:System.Windows.Forms.Control.Focus%2A> per specificare il nome del controllo da trovare e portare allo stato attivo.  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#1)]  
  
### Per accedere a un'immagine in una raccolta di immagini  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.ImageList.ImageCollection.Item%2A> per specificare il nome dell'immagine cui si desidera accedere.  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#2)]  
  
### Per impostare una scheda come scheda selezionata  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.TabControl.SelectedTab%2A> con la proprietà <xref:System.Windows.Forms.TabControl.TabPageCollection.Item%2A> per specificare il nome della scheda da impostare come scheda selezionata.  
  
     [!code-csharp[System.Windows.Forms.KeyedCollectionsEx#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.KeyedCollectionsEx#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyedCollectionsEx/VB/Form1.vb#3)]  
  
## Vedere anche  
 [Getting Started with Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)   
 [Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form](../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)