---
title: "Procedura: associare un menu di scelta rapida a un TreeNode utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "menu di scelta rapida, associazione a TreeNode"
  - "TreeNode, collegamento a un menu di scelta rapida (finestra di progettazione)"
ms.assetid: 8e45e184-1313-4f8f-90ff-2cd5789b2268
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: associare un menu di scelta rapida a un TreeNode utilizzando la finestra di progettazione
Il controllo <xref:System.Windows.Forms.TreeView> di Windows Form consente di visualizzare una gerarchia di nodi, nello stesso modo in cui file e cartelle vengono visualizzati nel riquadro sinistro della funzionalità Esplora risorse nei sistemi operativi Windows.  Se si imposta la proprietà <xref:System.Windows.Forms.Control.ContextMenuStrip%2A>, è possibile fornire all'utente operazioni sensibili al contesto per la selezione con il pulsante destro del mouse del controllo <xref:System.Windows.Forms.TreeView>.  Se si associa un componente <xref:System.Windows.Forms.ContextMenuStrip> a singoli elementi <xref:System.Windows.Forms.TreeNode>, è possibile aggiungere un livello personalizzato di funzionalità del menu di scelta rapida ai controlli <xref:System.Windows.Forms.TreeView>.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per associare un menu di scelta rapida a un TreeNode in fase di progettazione  
  
1.  Aggiungere un controllo <xref:System.Windows.Forms.TreeView> al form, quindi aggiungervi i nodi necessari.  Per ulteriori informazioni, vedere [Procedura: aggiungere e rimuovere nodi tramite il controllo TreeView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md).  
  
2.  Aggiungere un componente <xref:System.Windows.Forms.ContextMenuStrip> al form, quindi aggiungere le voci al menu di scelta rapida che rappresentano le operazioni a livello di nodo da rendere disponibili in fase di esecuzione.  Per ulteriori informazioni, vedere [Procedura: aggiungere voci di menu a un ContextMenuStrip](../../../../docs/framework/winforms/controls/how-to-add-menu-items-to-a-contextmenustrip.md).  
  
3.  Riaprire la finestra di dialogo **Editor TreeNode** per il controllo <xref:System.Windows.Forms.TreeView>, selezionare il nodo da modificare e impostare la proprietà <xref:System.Windows.Forms.ContextMenuStrip> sul menu di scelta rapida aggiunto.  
  
4.  Quando la proprietà è impostata, il menu di scelta rapida viene visualizzato se si fa clic con il pulsante destro del mouse sul nodo.  
  
     Potrebbe inoltre essere necessario scrivere il codice per gestire gli eventi <xref:System.Windows.Forms.ToolStripItem.Click> per tali voci di menu.  
  
## Vedere anche  
 [Controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)   
 [Cenni preliminari sul controllo TreeView](../../../../docs/framework/winforms/controls/treeview-control-overview-windows-forms.md)   
 [Controllo ContextMenuStrip](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)