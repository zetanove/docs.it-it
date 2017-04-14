---
title: "Procedura: nascondere ToolStripMenuItems | Microsoft Docs"
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
  - "voci di menu nascoste"
  - "voci di menu, nascondere"
  - "menu, voci di menu nascoste"
  - "MenuStrip (controllo) [Windows Form], voci di menu nascoste"
  - "ToolStripMenuItems, nascondere"
ms.assetid: 418a768f-808a-44cd-8cef-f4e161883621
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: nascondere ToolStripMenuItems
Nascondere voci di menu è un modo per controllare l'interfaccia utente dell'applicazione e limitare il numero dei comandi accessibili.  Spesso risulta necessario nascondere un intero menu se tutte le voci che ne fanno parte non sono disponibili,  per evitare distrazioni all'utente.  Oltre a nascondere il menu o la voce di menu, potrebbe essere necessario disabilitarlo, in quanto nasconderlo solamente non ne impedisce l'accesso tramite un tasto di scelta rapida.  
  
### Per nascondere una voce di menu a livello di codice  
  
-   All'interno del metodo in cui sono state impostate le proprietà della voce di menu, aggiungere codice per impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.Visible%2A> su `false`.  
  
    ```vb  
    MenuItem3.Visible = False  
  
    ```  
  
    ```csharp  
    menuItem3.Visible = false;  
  
    ```  
  
    ```cpp  
    menuItem3->Visible = false;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripItem.Visible%2A>   
 <xref:System.Windows.Forms.MenuStrip>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)   
 [Procedura: disabilitare ToolStripMenuItems](../../../../docs/framework/winforms/controls/how-to-disable-toolstripmenuitems.md)