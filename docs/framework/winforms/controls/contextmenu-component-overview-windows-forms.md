---
title: "Cenni preliminari sul componente ContextMenu (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ContextMenu"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "menu di scelta rapida, ContextMenu (componente)"
  - "ContextMenu (componente) [Windows Form], informazioni sul componente ContextMenu"
  - "menu di scelta rapida, ContextMenu (componente)"
ms.assetid: 49d6398f-d3c4-4679-84fa-1de07b68b05e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Cenni preliminari sul componente ContextMenu (Windows Form)
> [!IMPORTANT]
>  Benché <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> sostituiscano i controlli <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> delle versioni precedenti aggiungendovi funzionalità, <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> vengono mantenuti per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Il componente <xref:System.Windows.Forms.ContextMenu> Windows Form può essere utilizzato per offrire agli utenti un menu facilmente accessibile di comandi utilizzati di frequente, associati all'oggetto selezionato.  Le voci di un menu di scelta rapida sono spesso un sottoinsieme delle voci dei menu principali visualizzati in altri punti dell'applicazione.  È in genere possibile accedere a un menu di scelta rapida facendo clic con il pulsante destro del mouse.  Nei Windows Form i menu di scelta rapida sono associati ai controlli.  
  
## Proprietà principali  
 È possibile associare un menu di scelta rapida a un controllo impostando la proprietà <xref:System.Windows.Forms.Control.ContextMenu%2A> del controllo sul componente <xref:System.Windows.Forms.ContextMenu>.  È possibile associare un singolo menu di scelta rapida a più controlli, ma a ciascun controllo è possibile associare un solo menu di scelta rapida.  
  
 La proprietà principale del componente <xref:System.Windows.Forms.ContextMenu> è <xref:System.Windows.Forms.Menu.MenuItems%2A>.  È possibile aggiungere voci di menu a livello di codice creando oggetti <xref:System.Windows.Forms.MenuItem> e aggiungendoli all'insieme <xref:System.Windows.Forms.Menu.MenuItemCollection> del menu di scelta rapida.  Poiché le voci di un menu di scelta rapida sono in genere tratte da altri menu, nella maggior parte dei casi per aggiungere voci a un menu di scelta rapida è possibile copiarle.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContextMenu>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>