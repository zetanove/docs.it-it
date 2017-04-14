---
title: "Procedura: abilitare il tasto TAB per l&#39;uscita da un controllo ToolStrip | Microsoft Docs"
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
  - "controlli [Windows Form], spostamento tra controlli"
  - "TAB (tasto), abilitazione"
  - "ToolStrip (controllo) [Windows Form], spostamento da"
ms.assetid: 40f9e88b-09a3-428e-8da8-c00bb65079c6
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: abilitare il tasto TAB per l&#39;uscita da un controllo ToolStrip
La procedura riportata di seguito consente all'utente di premere il tasto TAB per uscire da un controllo <xref:System.Windows.Forms.ToolStrip> e passare al controllo successivo nell'ordine di tabulazione.  
  
 Il controllo <xref:System.Windows.Forms.ToolStrip> accetta la prima pressione del tasto TAB, quindi i tasti di direzione consentono di selezionare elementi all'interno di <xref:System.Windows.Forms.ToolStrip>.  Quando l'utente preme il tasto TAB per la seconda volta, il cursore passa al controllo successivo nell'ordine di tabulazione.  
  
### Per consentire all'utente di premere il tasto TAB per uscire da un ToolStrip e passare al controllo successivo  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStrip.TabStop%2A> del controllo <xref:System.Windows.Forms.ToolStrip> su `true`.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStrip.TabStop%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)