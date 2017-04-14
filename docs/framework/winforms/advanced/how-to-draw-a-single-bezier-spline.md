---
title: "Procedura: disegnare una singola spline di B&#233;zier | Microsoft Docs"
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
  - "spline di Bézier, disegno"
  - "disegno, spline di Bézier"
ms.assetid: f4f3fe30-f0a6-4743-ac91-11310cebea9f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: disegnare una singola spline di B&#233;zier
Una spline di Bézier è definita da quattro punti: un punto iniziale, due punti di controllo e un punto finale.  
  
## Esempio  
 Nell'esempio che segue viene disegnata una spline di Bézier con punto iniziale \(10, 100\) e punto finale \(200, 100\).  I punti di controllo sono \(100, 10\) e \(150, 150\).  
  
 Nell'illustrazione che segue si mostra la spline di Bézier risultante insieme ai relativi punto iniziale, punti di controllo e punto finale.  Nell'illustrazione è visibile inoltre la struttura convessa della spline, ovvero un poligono formato collegando i quattro punti con linee rette.  
  
 ![Spline Bezier](../../../../docs/framework/winforms/advanced/media/bezierspline1.png "BezierSpline1")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#31)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 <xref:System.Drawing.Graphics.DrawBezier%2A>   
 [Spline di Bézier in GDI\+](../../../../docs/framework/winforms/advanced/bezier-splines-in-gdi.md)   
 [Procedura: disegnare una sequenza di spline di Bézier](../../../../docs/framework/winforms/advanced/how-to-draw-a-sequence-of-bezier-splines.md)