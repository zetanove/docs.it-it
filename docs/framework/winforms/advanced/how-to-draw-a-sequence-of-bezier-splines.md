---
title: "Procedura: disegnare una sequenza di spline di B&#233;zier | Microsoft Docs"
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
  - "spline di Bézier, disegno di sequenze"
  - "spline, disegno di Bézier"
ms.assetid: 37a0bedb-20c2-4cf0-91fa-a5509e826b30
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: disegnare una sequenza di spline di B&#233;zier
Per creare una sequenza di spline Bézier collegate, è possibile utilizzare il metodo <xref:System.Drawing.Graphics.DrawBeziers%2A> della classe <xref:System.Drawing.Graphics>.  
  
## Esempio  
 Nell'esempio qui di seguito viene tracciata una curva composta da due spline Bézier collegate.  Il punto finale della prima spline Bézier corrisponde al punto d'inizio della seconda spline Bézier.  
  
 Nell'illustrazione che segue sono visibili le curve collegate e i sette punti.  
  
 ![Spline Bezier](../../../../docs/framework/winforms/advanced/media/bezierspline2.png "BezierSpline2")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#11)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Grafica e disegno in Windows Form](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [Spline di Bézier in GDI\+](../../../../docs/framework/winforms/advanced/bezier-splines-in-gdi.md)   
 [Costruzione e creazione di curve](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)