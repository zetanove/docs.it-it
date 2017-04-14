---
title: "Spline di B&#233;zier in GDI+ | Microsoft Docs"
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
  - "spline di Bézier"
  - "GDI+, spline di Bézier"
  - "spline, Bézier"
ms.assetid: 5774ce1e-87d4-4bc7-88c4-4862052781b8
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Spline di B&#233;zier in GDI+
Una spline Bézier è una curva specificata da quattro punti: due punti finali \(p1 e p2\) e due punti di controllo \(c1 e c2\).  La curva inizia in p1 e finisce in p2  e non attraversa i punti di controllo, che tuttavia fungono da magneti, attirando la curva in determinate direzioni e influenzandone la curvatura.  Nell'immagine seguente vengono mostrati una curva Bézier con i relativi punti finali e punti di controllo.  
  
 ![Spline Bezier](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art11a.png "Aboutgdip02\_art11a")  
  
 Si noti che la curva inizia in p1 e si sposta verso il punto di controllo c1.  La tangente della curva in p1 è la linea che unisce p1 e c1.  Si noti inoltre che la tangente nel punto finale p2 è la linea che unisce c2 e p2.  
  
## Creazione di spline di Bézier  
 Per tracciare una spline Bézier, sono necessari un'istanza della classe <xref:System.Drawing.Graphics> e <xref:System.Drawing.Pen>.  L'istanza della classe <xref:System.Drawing.Graphics> fornisce il metodo <xref:System.Drawing.Graphics.DrawBezier%2A>, mentre in <xref:System.Drawing.Pen> sono memorizzati gli attributi, quali lo spessore e il colore, della linea utilizzata per eseguire il rendering della curva.  L'oggetto <xref:System.Drawing.Pen> viene passato come uno degli argomenti al metodo <xref:System.Drawing.Graphics.DrawBezier%2A>.  Gli argomenti rimanenti passati al metodo <xref:System.Drawing.Graphics.DrawBezier%2A> rappresentano i punti finali e i punti di controllo.  L'esempio seguente consente di tracciare una spline Bézier con punto iniziale \(0, 0\), punti di controllo \(40, 20\) e \(80, 150\) e punto finale \(100, 10\):  
  
 [!code-csharp[LinesCurvesAndShapes#71](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#71)]
 [!code-vb[LinesCurvesAndShapes#71](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#71)]  
  
 Nell'immagine seguente vengono mostrati la curva, i punti di controllo e due tangenti.  
  
 ![Spline Bezier](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art12.png "Aboutgdip02\_art12")  
  
 Le spline Bézier furono concepite da Pierre Bézier per la progettazione nell'industria automobilistica.  Si sono successivamente rivelate utili in svariati tipi di progettazioni assistite dal computer e vengono utilizzate anche per definire i contorni dei caratteri.  Le spline Bézier consentono di ottenere una vasta gamma di forme, alcune delle quali sono mostrate nell'immagine qui di seguito.  
  
 ![Percorsi](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art13.png "Aboutgdip02\_art13")  
  
## Vedere anche  
 <xref:System.Drawing.Graphics?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Costruzione e creazione di curve](../../../../docs/framework/winforms/advanced/constructing-and-drawing-curves.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Procedura: creare un oggetto Pen](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)