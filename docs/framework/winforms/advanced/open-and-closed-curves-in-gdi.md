---
title: "Curve aperte e chiuse in GDI+ | Microsoft Docs"
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
  - "curve"
  - "curve, disegno"
  - "curve, riempimento"
  - "GDI+, curve"
ms.assetid: 08d2cc9a-dc9d-4eed-bcbb-2c8e2ca5d3ae
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Curve aperte e chiuse in GDI+
Nell'immagine seguente vengono mostrate due curve, una aperta e una chiusa.  
  
 ![Curve aperte e chiuse](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art24.png "Aboutgdip02\_art24")  
  
## Interfaccia gestita per le curve  
 Le curve chiuse dispongono di una zona interna ed è quindi possibile riempirle con un pennello.  La classe <xref:System.Drawing.Graphics> in [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] fornisce i seguenti metodi per il riempimento di forme e curve chiuse: <xref:System.Drawing.Graphics.FillRectangle%2A>, <xref:System.Drawing.Graphics.FillEllipse%2A>, <xref:System.Drawing.Graphics.FillPie%2A>, <xref:System.Drawing.Graphics.FillPolygon%2A>, <xref:System.Drawing.Graphics.FillClosedCurve%2A>, <xref:System.Drawing.Graphics.FillPath%2A> e <xref:System.Drawing.Graphics.FillRegion%2A>.  Ogni volta che si chiama uno di questi metodi, è necessario passare il tipo di pennello specifico \(<xref:System.Drawing.SolidBrush>, <xref:System.Drawing.Drawing2D.HatchBrush>, <xref:System.Drawing.TextureBrush>, <xref:System.Drawing.Drawing2D.LinearGradientBrush> o <xref:System.Drawing.Drawing2D.PathGradientBrush>\) come argomento.  
  
 Il metodo <xref:System.Drawing.Graphics.FillPie%2A> è correlato al metodo <xref:System.Drawing.Graphics.DrawArc%2A>.  Analogamente al metodo <xref:System.Drawing.Graphics.DrawArc%2A>, che consente di tracciare una porzione del contorno di un'ellisse, il metodo <xref:System.Drawing.Graphics.FillPie%2A> riempie una porzione dell'interno di un'ellisse.  L'esempio seguente consente di tracciare un arco e di riempire la porzione corrispondente dell'interno di un'ellisse.  
  
 [!code-csharp[LinesCurvesAndShapes#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#21)]
 [!code-vb[LinesCurvesAndShapes#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#21)]  
  
 Nell'immagine seguente vengono mostrati l'arco e l'ellisse riempita.  
  
 ![Curve aperte e chiuse](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art25.png "Aboutgdip02\_art25")  
  
 Il metodo <xref:System.Drawing.Graphics.FillClosedCurve%2A> è correlato al metodo <xref:System.Drawing.Graphics.DrawClosedCurve%2A>.  Entrambi i metodi consentono di chiudere automaticamente la curva collegandone il punto finale e il punto iniziale.  L'esempio seguente consente di tracciare una curva che attraversa \(0, 0\), \(60, 20\) e \(40, 50\).  La curva viene quindi chiusa automaticamente collegando \(40, 50\) al punto iniziale \(0, 0\) e l'interno viene riempito con un colore a tinta unita.  
  
 [!code-csharp[LinesCurvesAndShapes#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#22)]
 [!code-vb[LinesCurvesAndShapes#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#22)]  
  
 Il metodo <xref:System.Drawing.Graphics.FillPath%2A> consente di riempire l'interno di pezzi separati di un percorso.  Se un pezzo di percorso non costituisce una curva o una forma chiusa, il metodo <xref:System.Drawing.Graphics.FillPath%2A> chiude automaticamente tale pezzo del percorso prima di riempirlo.  L'esempio seguente consente di tracciare e riempire un percorso costituito da un arco, una spline di tipo Cardinal, una stringa e una torta:  
  
 [!code-csharp[LinesCurvesAndShapes#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#23)]
 [!code-vb[LinesCurvesAndShapes#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#23)]  
  
 Nell'immagine seguente viene mostrato i percorso con e senza il riempimento a tinta unita.  Si noti che tramite il metodo <xref:System.Drawing.Graphics.DrawPath%2A> sono stati tracciati i contorni del testo della stringa senza riempimento.  Per riempire l'interno dei caratteri della stringa, è necessario utilizzare il metodo <xref:System.Drawing.Graphics.FillPath%2A>.  
  
 ![Stringa in un percorso](../../../../docs/framework/winforms/advanced/media/aboutgdip02-art26.png "Aboutgdip02\_art26")  
  
## Vedere anche  
 <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=fullName>   
 <xref:System.Drawing.Pen?displayProperty=fullName>   
 <xref:System.Drawing.Point?displayProperty=fullName>   
 [Linee, curve e forme](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [Procedura: creare oggetti Graphics per disegnare](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [Costruzione e creazione di percorsi](../../../../docs/framework/winforms/advanced/constructing-and-drawing-paths.md)