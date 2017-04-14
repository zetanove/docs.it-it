---
title: "Procedura: rilevare quando il puntatore del mouse si trova sopra un ToolStripItem | Microsoft Docs"
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
  - "mouse, rilevamento del movimento nelle barre degli strumenti"
  - "barre degli strumenti [Windows Form], rilevamento del movimento del mouse"
  - "ToolStrip (controllo) [Windows Form], rilevamento del movimento del mouse"
  - "ToolStripItem (classe), rilevamento del movimento del mouse"
ms.assetid: d38b5082-aba7-4f6c-841b-bd9714e307fd
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: rilevare quando il puntatore del mouse si trova sopra un ToolStripItem
La procedura riportata di seguito consente di rilevare quando il puntatore del mouse si trova sopra un <xref:System.Windows.Forms.ToolStripItem>.  
  
### Per rilevare quanto il puntatore si trova sopra un ToolStripItem  
  
-   Utilizzare la proprietà <xref:System.Windows.Forms.ToolStripItem.Selected%2A> per gli elementi in cui la proprietà <xref:System.Windows.Forms.ToolStripItem.CanSelect%2A> è impostata su `true`.  
  
     In tal modo si evita la necessità di sincronizzare gli eventi <xref:System.Windows.Forms.ToolStripItem.MouseEnter> e <xref:System.Windows.Forms.ToolStripItem.MouseLeave>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripItem.Selected%2A>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)