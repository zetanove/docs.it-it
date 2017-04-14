---
title: "Procedura: disabilitare i ToolStripMenuItems con la finestra di progettazione | Microsoft Docs"
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
  - "voci di menu, disabilitazione"
  - "menu, disabilitazione di elementi"
  - "MenuStrip (controllo) [Windows Form], disabilitazione di voci di menu nella finestra di progettazione"
  - "ToolStripMenuItems, disabilitazione nella finestra di progettazione"
ms.assetid: 985e311e-7d67-4205-b5a3-d045b68a4a03
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: disabilitare i ToolStripMenuItems con la finestra di progettazione
L'abilitazione e la disabilitazione di voci di menu in risposta alle attività dell'utente consentono di limitare o aumentare il numero di comandi che l'utente può eseguire.  Per impostazione predefinita, le voci di menu vengono attivate al momento della creazione, ma l'impostazione può essere modificata tramite la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>.  È possibile modificare la proprietà in fase di progettazione nella finestra **Proprietà** o impostandola a livello di codice.  Per ulteriori informazioni, vedere [Procedura: disabilitare ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per disabilitare una voce di menu in fase di progettazione  
  
1.  Una volta selezionata la voce di menu nel form, impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> su `false`.  
  
    > [!TIP]
    >  Se si disabilita la prima voce o la voce di primo livello in un menu, vengono disabilitate tutte le voci in esso contenute.  Analogamente, disabilitando una voce di menu che contiene voci di sottomenu si disabilitano le voci di sottomenu.  Se nessun comando di un determinato menu risulta disponibile per l'utente, è opportuno nascondere e disabilitare l'intero menu per rendere più chiara l'interfaccia utente.  È necessario nascondere e disabilitare il menu, in quanto nasconderlo solamente non impedisce l'accesso a un comando di menu tramite un tasto di scelta rapida.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> di una voce di menu di primo livello su `false` per nascondere l'intero menu.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Procedura: nascondere ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-hide-toolstripmenuitems.md)   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)