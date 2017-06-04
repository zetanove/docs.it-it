---
title: "Procedura: aggiungere e rimuovere nodi nel controllo TreeView Windows Form mediante la finestra di progettazione | Microsoft Docs"
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
  - "esempi [Windows Form], TreeView (controllo)"
  - "nodi della struttura ad albero nel controllo TreeView"
  - "TreeView (controllo) [Windows Form], aggiunta di nodi"
  - "TreeView (controllo) [Windows Form], rimozione di nodi"
ms.assetid: 35bf1750-045e-4ec5-97cb-b47b0dbdaa2c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: aggiungere e rimuovere nodi nel controllo TreeView Windows Form mediante la finestra di progettazione
Dal momento che il controllo <xref:System.Windows.Forms.TreeView> Windows Form consente di visualizzare i nodi in modo gerarchico, nell'aggiunta di un nodo è necessario prestare attenzione alla posizione del corrispondente nodo padre.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.TreeView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere o rimuovere nodi nella finestra di progettazione  
  
1.  Fare clic sul controllo <xref:System.Windows.Forms.TreeView>.  
  
2.  Nella finestra **Proprietà**, fare clic sul pulsante con i **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.TreeView.Nodes%2A>.  
  
     Verrà visualizzato l'**Editor TreeNode**.  
  
3.  Per aggiungere dei nodi, è necessario che esista un nodo di primo livello. In caso contrario, occorre aggiungere una radice facendo clic sul pulsante **Aggiungi radice**.  È quindi possibile aggiungere i nodi figlio selezionando la radice o qualsiasi altro nodo e facendo clic sul pulsante **Aggiungi figlio**.  
  
4.  Per eliminare un nodo, selezionarlo e fare clic sul pulsante **Elimina**.  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [Procedura: impostare icone per il controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-set-icons-for-the-windows-forms-treeview-control.md)   
 [Procedura: scorrere tutti i nodi di un controllo TreeView Windows Form](../../../../docs/framework/winforms/controls/how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)   
 [Procedura: individuare il nodo di TreeView scelto](../../../../docs/framework/winforms/controls/how-to-determine-which-treeview-node-was-clicked-windows-forms.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)