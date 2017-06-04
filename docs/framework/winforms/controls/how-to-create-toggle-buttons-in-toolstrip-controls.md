---
title: "Procedura: creare pulsanti interruttore nei controlli ToolStrip | Microsoft Docs"
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
  - "esempi [Windows Form], barre degli strumenti"
  - "interruttori, creazione"
  - "ToolStrip (controllo) [Windows Form], creazione di interruttori"
ms.assetid: d9c197df-4c65-43f2-beee-b68b52b2befc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare pulsanti interruttore nei controlli ToolStrip
Quando si fa clic su un pulsante interruttore, questo sembra incassato e mantiene tale aspetto finché non viene di nuovo fatto clic.  
  
### Per creare un ToolStripButton interruttore  
  
-   Utilizzare codice analogo a quello di esempio riportato di seguito:  nel codice si presuppone che il form utilizzato contenga un controllo <xref:System.Windows.Forms.ToolStrip> e che la relativa raccolta <xref:System.Windows.Forms.ToolStrip.Items%2A> contenga un oggetto <xref:System.Windows.Forms.ToolStripButton> denominato `toolStripButton1`.  Si presuppone inoltre che l'utente disponga di un gestore eventi denominato `toolStripButton1_CheckedChanged`.  
  
     \[Visual Basic\]  
  
    ```  
    toolStripButton1.CheckOnClick = True  
    toolStripButton1.CheckedChanged AddressOf _  
    EventHandler(toolStripButton1_CheckedChanged);  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStripButton1.CheckOnClick = true;  
    toolStripButton1.CheckedChanged += new _  
    EventHandler(toolStripButton1_CheckedChanged);  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStripButton>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)