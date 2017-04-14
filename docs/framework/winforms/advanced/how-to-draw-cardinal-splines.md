---
title: "Procedura: disegnare spline di tipo Cardinal | Microsoft Docs"
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
  - "spline cardinali, disegno"
  - "disegno, spline cardinali"
  - "grafica, spline cardinali"
ms.assetid: a4a41e80-4461-4b47-b6bd-2c5e68881994
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: disegnare spline di tipo Cardinal
Una spline di tipo Cardinal è una curva che passa per un dato insieme di punti.  Per disegnare una spline di tipo Cardinal, creare un oggetto <xref:System.Drawing.Graphics> e passare al metodo <xref:System.Drawing.Graphics.DrawCurve%2A> l'indirizzo di una matrice di punti.  
  
### Creazione di una spline di tipo Cardinal a campana  
  
-   Nell'esempio che segue si disegna una spline di tipo Cardinal a campana che passa attraverso cinque punti designati.  Nell'illustrazione che segue si mostra la curva e cinque punti.  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#21)]  
  
### Creazione di una spline di tipo Cardinal chiusa  
  
-   Per disegnare una spline di tipo Cardinal chiusa, utilizzare il metodo <xref:System.Drawing.Graphics.DrawClosedCurve%2A> della classe <xref:System.Drawing.Graphics>.  In questo tipo spline la curva continua fino all'ultimo punto della matrice e si collega con il primo punto di essa.  Nell'esempio che segue viene tracciata una spline di tipo Cardinal chiusa che passa attraverso sei punti designati.  Nell'illustrazione che segue si mostra la spline chiusa e i sei punti.  
  
 ![Spline di tipo Cardinal](../../../../docs/framework/winforms/advanced/media/cardinalspline1a.png "CardinalSpline1A")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#22)]  
  
### Modifica della curvatura di una spline di tipo Cardinal  
  
-   È possibile modificare la curvatura di una spline di tipo Cardinal passando un argomento di tensione al metodo <xref:System.Drawing.Graphics.DrawCurve%2A>.  Nell'esempio che segue vengono disegnate tre spline di tipo Cardinal che passano per lo stesso insieme di punti.  Nell'illustrazione che segue sono mostrate le tre curve e i relativi valori di tensione.  Si noti che quando la tensione è 0 i punti sono collegati da linee rette.  
  
 ![Spline di tipo Cardinal](../../../../docs/framework/winforms/advanced/media/cardinalspline2.png "CardinalSpline2")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingCurves#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.ConstructingDrawingCurves#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingCurves/VB/Class1.vb#23)]  
  
## Compilazione del codice  
 L'esempio riportato in precedenza è stato creato per essere utilizzato con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, un parametro del gestore eventi <xref:System.Windows.Forms.Control.Paint>.  
  
## Vedere anche  
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Costruzione e creazione di curve](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)