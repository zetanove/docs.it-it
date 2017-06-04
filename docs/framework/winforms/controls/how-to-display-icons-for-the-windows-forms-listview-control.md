---
title: "Procedura: visualizzare icone per il controllo ListView Windows Form | Microsoft Docs"
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
  - "icone, visualizzazione per i controlli ListView"
  - "ImageList (componente) [Windows Form], con controllo ListView"
  - "visualizzazioni elenco, visualizzazione di icone"
  - "elenchi, visualizzazione di icone"
  - "ListView (controllo) [Windows Form], visualizzazione di icone"
ms.assetid: 9d577542-8595-429b-99e5-078770ec9d35
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: visualizzare icone per il controllo ListView Windows Form
Il controllo <xref:System.Windows.Forms.ListView> di Windows Form può visualizzare le icone da tre elenchi immagini.  Le visualizzazioni List, Details e SmallIcon visualizzano le immagini dell'elenco specificato nella proprietà <xref:System.Windows.Forms.ListView.SmallImageList%2A>,  mentre la visualizzazione LargeIcon visualizza le immagini dell'elenco specificato nella proprietà <xref:System.Windows.Forms.ListView.LargeImageList%2A>.  Una visualizzazione elenco può anche visualizzare un ulteriore insieme di icone, impostato nella proprietà <xref:System.Windows.Forms.ListView.StateImageList%2A>, accanto alle icone grandi o piccole.  Per ulteriori informazioni sugli elenchi di immagini vedere [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) e [Procedura: aggiungere o rimuovere immagini tramite il componente ImageList Windows Form](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md).  
  
### Per visualizzare le immagini in una visualizzazione elenco  
  
1.  Impostare la proprietà appropriata, <xref:System.Windows.Forms.ListView.SmallImageList%2A>, <xref:System.Windows.Forms.ListView.LargeImageList%2A> o <xref:System.Windows.Forms.ListView.StateImageList%2A>, sul componente <xref:System.Windows.Forms.ImageList> esistente che si desidera utilizzare.  
  
     Queste proprietà possono essere impostate nella finestra di progettazione mediante la finestra Proprietà oppure nel codice.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#41)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#41)]  
  
2.  Impostare la proprietà <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A> o <xref:System.Windows.Forms.ListViewItem.StateImageIndex%2A> per ciascuna voce di elenco con un'icona associata.  
  
     Queste proprietà possono essere impostate nel codice o all'interno dell'**editor della raccolta ListViewItem**.  Per aprire l'**editor della raccolta ListViewItem**, fare clic sul pulsante con i puntini di sospensione \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.ListView.Items%2A> nella finestra **Proprietà**.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#42)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#42)]  
  
## Vedere anche  
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [Componente ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)