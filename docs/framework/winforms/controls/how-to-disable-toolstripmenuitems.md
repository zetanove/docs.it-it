---
title: "Procedura: disabilitare ToolStripMenuItems | Microsoft Docs"
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
  - "disabilitazione voci di menu"
  - "voci di menu, disabilitazione"
  - "voci di menu, abilitazione"
  - "menu, disabilitazione voci di menu"
  - "ToolStripMenuItems, disabilitazione"
  - "ToolStripMenuItems, abilitazione"
ms.assetid: bcc1da84-50fd-41d2-8475-103b581d5654
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: disabilitare ToolStripMenuItems
L'abilitazione e la disabilitazione di voci di menu in risposta alle attività dell'utente consentono di limitare o aumentare il numero di comandi che l'utente può eseguire.  Per impostazione predefinita, le voci di menu vengono attivate al momento della creazione, ma l'impostazione può essere modificata tramite la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>.  È possibile modificare la proprietà in fase di progettazione nella finestra **Proprietà** o impostandola a livello di codice.  
  
### Per disabilitare una voce di menu a livello di codice  
  
-   Nell'ambito del metodo in cui si impostano le proprietà della voce di menu aggiungere il codice per impostare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A> su `false`.  
  
    ```vb  
    MenuItem1.Enabled = False  
    ```  
  
    ```csharp  
    menuItem1.Enabled = false;  
    ```  
  
    ```cpp  
    menuItem1->Enabled = false;  
    ```  
  
    > [!TIP]
    >  Se si disabilita la prima voce o la voce di primo livello in un menu, vengono nascoste ma non disabilitate tutte le voci in esso contenute.  Analogamente, disabilitando una voce di menu che contiene voci di sottomenu si nascondono ma non si disabilitano le voci di sottomenu.  Se nessun comando di un determinato menu risulta disponibile per l'utente, è opportuno nascondere e disabilitare l'intero menu per rendere più chiara l'interfaccia utente.  È necessario nascondere e disabilitare il menu nonché disabilitare tutte le voci di menu e sottomenu in esso contenute, in quanto nasconderlo solamente non impedisce l'accesso a un comando di menu tramite un tasto di scelta rapida.  Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> di una voce di menu di primo livello su `false` per nascondere l'intero menu.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [Procedura: nascondere ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-hide-toolstripmenuitems.md)   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)