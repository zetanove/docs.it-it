---
title: "Procedura: modificare l&#39;aspetto del testo e delle immagini di una descrizione comandi in Windows Form | Microsoft Docs"
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
  - "barre degli strumenti [Windows Form], aspetto"
  - "barre degli strumenti [Windows Form], immagini"
  - "barre degli strumenti [Windows Form], testo"
  - "ToolStrip (controllo) [Windows Form], aspetto"
  - "ToolStrip (controllo) [Windows Form], immagini"
  - "ToolStrip (controllo) [Windows Form], testo"
ms.assetid: d62dc9d1-2edd-4dfa-aed7-1335d6e13d86
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: modificare l&#39;aspetto del testo e delle immagini di una descrizione comandi in Windows Form
È possibile controllare la visualizzazione di testo e immagini in una classe <xref:System.Windows.Forms.ToolStripItem> nonché il modo in cui sono allineati tra di loro e rispetto alla classe <xref:System.Windows.Forms.ToolStrip>.  
  
### Per definire ciò che viene visualizzato su un ToolStripItem  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> sul valore desiderato.  I valori possibili sono `Image`, `ImageAndText`, `None` e `Text`.  Il valore predefinito è `ImageAndText`.  
  
    ```vb  
    ToolStripButton2.DisplayStyle = _  
        System.Windows.Forms.ToolStripItemDisplayStyle.Image  
  
    ```  
  
    ```csharp  
    toolStripButton2.DisplayStyle = System.Windows.Forms.ToolStripItemDisplayStyle.Image;  
  
    ```  
  
### Per allineare testo su un ToolStripItem  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.TextAlign%2A> sul valore desiderato.  I valori possibili sono qualsiasi combinazione di allineamento in alto, al centro e in basso, a sinistra, centrato e a destra.  Il valore predefinito è `MiddleCenter`.  
  
    ```vb  
    ToolStripSplitButton1.TextAlign = _  
        System.Drawing.ContentAlignment.MiddleRight  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.TextAlign = System.Drawing.ContentAlignment.MiddleRight;  
  
    ```  
  
### Per allineare un'immagine su un ToolStripItem  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.ImageAlign%2A> sul valore desiderato.  I valori possibili sono qualsiasi combinazione di allineamento in alto, al centro e in basso, a sinistra, centrato e a destra.  Il valore predefinito è `MiddleLeft`.  
  
    ```vb  
    ToolStripSplitButton1.ImageAlign = _  
        System.Drawing.ContentAlignment.MiddleRight  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.ImageAlign = System.Drawing.ContentAlignment.MiddleRight;  
  
    ```  
  
### Per definire il modo in cui il testo e le immagini di un ToolStripItem sono visualizzati  
  
-   Impostare la proprietà <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A> sul valore desiderato.  I valori possibili sono `ImageAboveText`, `ImageBeforeText`, `Overlay`, `TextAboveImage` e `TextBeforeImage`.  Il valore predefinito è `ImageBeforeText`.  
  
    ```vb  
    ToolStripButton1.TextImageRelation = _  
        System.Windows.Forms.TextImageRelation.ImageAboveText  
  
    ```  
  
    ```csharp  
    toolStripButton1.TextImageRelation = System.Windows.Forms.TextImageRelation.ImageAboveText;  
  
    ```  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolStrip>   
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Architettura del controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)