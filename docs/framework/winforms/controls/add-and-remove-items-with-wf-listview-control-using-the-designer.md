---
title: "Procedura: aggiungere e rimuovere elementi nel controllo ListView Windows Form mediante la finestra di progettazione | Microsoft Docs"
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
  - "ListView (controllo) [Windows Form], aggiunta voci di elenco"
  - "ListView (controllo) [Windows Form], compilazione"
ms.assetid: 217611ee-fd11-4d39-9a54-a37c3e781be1
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: aggiungere e rimuovere elementi nel controllo ListView Windows Form mediante la finestra di progettazione
Il processo di aggiunta di un elemento al controllo <xref:System.Windows.Forms.ListView> Windows Form consiste principalmente nella definizione dell'elemento e nell'assegnazione delle proprietà allo stesso.  È possibile aggiungere o rimuovere le voci di elenco in qualsiasi momento.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.ListView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere o rimuovere elementi mediante la finestra di progettazione  
  
1.  Fare clic sul controllo <xref:System.Windows.Forms.ListView>.  
  
2.  Nella finestra **Proprietà**, fare clic sul pulsante con i **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.ListView.Items%2A>.  
  
     Viene visualizzato l'**Editor della raccolta ListViewItem**.  
  
3.  Per aggiungere un elemento, fare clic sul pulsante **Aggiungi**.  È possibile impostare quindi le proprietà del nuovo elemento, ad esempio le proprietà <xref:System.Windows.Forms.ListView.Text%2A> e <xref:System.Windows.Forms.ListViewItem.ImageIndex%2A>.  
  
4.  Per rimuovere un elemento, selezionarlo e fare clic sul pulsante **Rimuovi**.  
  
## Vedere anche  
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Procedura: aggiungere colonne al controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-columns-to-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare icone per il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)   
 [Procedura: raggruppare elementi in un controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-group-items-in-a-windows-forms-listview-control.md)