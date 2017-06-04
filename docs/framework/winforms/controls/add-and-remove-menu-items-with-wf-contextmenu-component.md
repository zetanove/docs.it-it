---
title: "Procedura: aggiungere e rimuovere voci di menu tramite il componente ContextMenu Windows Form | Microsoft Docs"
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
  - "menu di scelta rapida, aggiunta di elementi"
  - "menu di scelta rapida, esempi"
  - "menu di scelta rapida, rimozione di elementi"
  - "ContextMenu (componente) [Windows Form], aggiunta di elementi"
  - "ContextMenu (componente) [Windows Form], rimozione di elementi"
  - "esempi [Windows Form], menu di scelta rapida"
  - "menu di scelta rapida, aggiunta di elementi"
  - "menu di scelta rapida, esempi"
  - "menu di scelta rapida, rimozione di elementi"
ms.assetid: 426d1eaf-7fb8-4b0b-8a33-5e8721786ea4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: aggiungere e rimuovere voci di menu tramite il componente ContextMenu Windows Form
Viene illustrato come aggiungere o rimuovere voci nei menu di scelta rapida in Windows Form.  
  
 Il componente <xref:System.Windows.Forms.ContextMenu> Windows Form fornisce un menu di comandi relativi all'oggetto selezionato e utilizzati di frequente.  È possibile aggiungere voci al menu di scelta rapida aggiungendo oggetti <xref:System.Windows.Forms.MenuItem> alla raccolta <xref:System.Windows.Forms.Menu.MenuItems%2A>.  
  
 È possibile rimuovere definitivamente voci da un menu di scelta rapida. In fase di esecuzione è tuttavia preferibile nascondere o disabilitare le voci.  
  
> [!IMPORTANT]
>  Benché <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> sostituiscano i controlli <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> delle versioni precedenti aggiungendovi funzionalità, <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> vengono mantenuti per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
### Per rimuovere voci da un menu di scelta rapida  
  
1.  Utilizzare il metodo <xref:System.Windows.Forms.Menu.MenuItemCollection.Remove%2A> o <xref:System.Windows.Forms.Menu.MenuItemCollection.RemoveAt%2A> della raccolta <xref:System.Windows.Forms.Menu.MenuItems%2A> del componente <xref:System.Windows.Forms.ContextMenu> per rimuovere una determinata voce di menu.  
  
    ```vb  
    ' Removes the first item in the shortcut menu.  
    ContextMenu1.MenuItems.RemoveAt(0)  
    ' Removes a particular object from the shortcut menu.  
    ContextMenu1.MenuItems.Remove(mnuItemNew)  
  
    ```  
  
    ```csharp  
    // Removes the first item in the shortcut menu.  
    contextMenu1.MenuItems.RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1.MenuItems.Remove(mnuItemNew);  
  
    ```  
  
    ```cpp  
    // Removes the first item in the shortcut menu.  
    contextMenu1->MenuItems->RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1->MenuItems->Remove(mnuItemNew);  
    ```  
  
     In alternativa  
  
2.  Utilizzare il metodo `Clear` della raccolta `MenuItems` del componente <xref:System.Windows.Forms.ContextMenu> per rimuovere tutte le voci dal menu.  
  
    ```vb  
    ContextMenu1.MenuItems.Clear()  
  
    ```  
  
    ```csharp  
    contextMenu1.MenuItems.Clear();  
  
    ```  
  
    ```cpp  
    contextMenu1->MenuItems->Clear();  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContextMenu>   
 [Componente ContextMenu](../../../../docs/framework/winforms/controls/contextmenu-component-windows-forms.md)   
 [Cenni preliminari sul componente ContextMenu](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md)