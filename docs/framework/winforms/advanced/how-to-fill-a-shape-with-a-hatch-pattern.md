---
title: "Procedura: riempire una forma con un motivo a tratteggio | Microsoft Docs"
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
  - "pennelli, utilizzo di pennelli per il tratteggio"
  - "modelli, aggiunta alle forme"
  - "forme, riempimento con modelli"
ms.assetid: 9c8300ff-187b-404f-af1f-ebd499f5b16f
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: riempire una forma con un motivo a tratteggio
Un motivo a tratteggio è composto da due colori: uno per lo sfondo e uno per le linee che formano il motivo sopra lo sfondo.  Per riempire una forma chiusa con un motivo a tratteggio, utilizzare un oggetto <xref:System.Drawing.Drawing2D.HatchBrush>.  Nell'esempio che segue si illustra come riempire un'ellisse con un motivo a tratteggio.  
  
## Esempio  
 Il costruttore <xref:System.Drawing.Drawing2D.HatchBrush.%23ctor%2A> accetta tre argomenti: lo stile del tratteggio, il colore della linea di tratteggio e il colore dello sfondo.  L'argomento relativo allo stile del tratteggio può essere un valore qualsiasi dell'enumerazione <xref:System.Drawing.Drawing2D.HatchStyle>.  L'enumerazione <xref:System.Drawing.Drawing2D.HatchStyle> include oltre cinquanta elementi, alcuni dei quali sono elencati di seguito:  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle>  
  
 Nell'illustrazione che segue viene mostrata l'ellisse riempita.  
  
 ![Motivo a tratteggio](../../../../docs/framework/winforms/advanced/media/hatch1.png "hatch1")  
  
 [!code-csharp[System.Drawing.UsingABrush#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.UsingABrush#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#41)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Utilizzo di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)