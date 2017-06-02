---
title: "Procedura: creare una curva di Bezier cubica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "curve di Bézier, cubiche"
  - "creazione, curve di Bézier cubiche"
  - "curve di Bézier cubiche"
  - "curve, Bézier cubiche"
  - "grafica, curve di Bézier cubiche"
ms.assetid: 450a3a77-7c57-48b0-a008-0f6051add980
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare una curva di Bezier cubica
In questo esempio viene illustrato come creare una curva di Bezier cubica.  Per creare una curva di Bezier cubica, utilizzare le classi <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure> e <xref:System.Windows.Media.BezierSegment>.  Per visualizzare la geometria risultante, utilizzare un elemento <xref:System.Windows.Shapes.Path> o utilizzarlo con <xref:System.Windows.Media.GeometryDrawing> o con <xref:System.Windows.Media.DrawingContext>.  Negli esempi riportati di seguito viene disegnata una curva di Bézier cubica da \(10, 100\) a \(300, 100\).  La curva presenta punti di controllo con valori \(100, 0\) e \(200, 200\).  
  
## Esempio  
 \[xaml\]  
  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile utilizzare la sintassi di markup abbreviata per descrivere un percorso.  
  
 [!code-xml[GeometrySample#53](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#53)]  
  
 \[xaml\]  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è anche possibile tracciare una curva di Bezier cubica utilizzando tag di oggetto.  L'esempio riportato di seguito equivale all'esempio di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 [!code-xml[GeometrySample#33](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#33)]  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Creare un arco ellittico](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md)   
 [Creare un oggetto LineSegment in un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-linesegment-in-a-pathgeometry.md)   
 [Create a Cubic Bezier Curve](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)   
 [Creare una curva di Bezier quadratica.](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md)