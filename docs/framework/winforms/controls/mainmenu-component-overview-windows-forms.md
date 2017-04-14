---
title: "Cenni preliminari sul componente MainMenu (Windows Form) | Microsoft Docs"
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
  - "MenuItem"
  - "MainMenu"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "MainMenu (controllo) [Windows Form], informazioni sul controllo MainMenu"
  - "menu"
ms.assetid: b41cc5a3-cc59-4996-aa3c-8dd9c17d3c90
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Cenni preliminari sul componente MainMenu (Windows Form)
> [!IMPORTANT]
>  Benché <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> sostituiscano i controlli <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> delle versioni precedenti aggiungendovi funzionalità, <xref:System.Windows.Forms.MainMenu> e <xref:System.Windows.Forms.ContextMenu> vengono mantenuti per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Il componente <xref:System.Windows.Forms.MainMenu> Windows Form consente la visualizzazione di un menu in fase di esecuzione.  Tutti i sottomenu del menu principale e le singole voci sono oggetti <xref:System.Windows.Forms.MenuItem>.  
  
## Proprietà principali  
 È possibile designare una voce di menu come voce predefinita impostando la proprietà <xref:System.Windows.Forms.MenuItem.DefaultItem%2A> su `true`.  La voce predefinita verrà visualizzata in grassetto quando si fa clic sul menu.  La proprietà <xref:System.Windows.Forms.MenuItem.Checked%2A> della voce di menu può essere `true` o `false` e indica se la voce di menu è selezionata.  La proprietà <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> della voce di menu consente di personalizzare l'aspetto della voce selezionata. Se <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> è impostata su `true`, accanto alla voce verrà visualizzato un pulsante di opzione. Se <xref:System.Windows.Forms.MenuItem.RadioCheck%2A> è impostata su `false`, accanto alla voce verrà visualizzato un segno di spunta.  
  
## Vedere anche  
 <xref:System.Windows.Forms.MainMenu>   
 <xref:System.Windows.Forms.Menu>   
 <xref:System.Windows.Forms.MenuItem>   
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ContextMenuStrip>   
 [Cenni preliminari sul controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)