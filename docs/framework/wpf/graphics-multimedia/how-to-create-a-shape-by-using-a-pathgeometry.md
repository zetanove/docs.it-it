---
title: "Procedura: creare una forma tramite un oggetto PathGeometry | Microsoft Docs"
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
  - "classi, PathGeometry"
  - "grafica [WPF], forme"
  - "PathGeometry (classe)"
  - "forme, creazione con la classe PathGeometry"
ms.assetid: 49a4a8b7-e738-45be-8dac-b54a6d8f5b21
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare una forma tramite un oggetto PathGeometry
In questo esempio viene illustrato come creare una forma utilizzando la classe <xref:System.Windows.Media.PathGeometry>.  Gli oggetti <xref:System.Windows.Media.PathGeometry> sono composti da uno o più oggetti <xref:System.Windows.Media.PathFigure>, ciascuno dei quali rappresenta una figura o forma diversa.  Ciascun oggetto <xref:System.Windows.Media.PathFigure> è a sua volta composto da uno o più oggetti <xref:System.Windows.Media.PathSegment>, ciascuno dei quali rappresenta una parte collegata della figura o forma.  I tipi di segmenti comprendono <xref:System.Windows.Media.LineSegment>, <xref:System.Windows.Media.ArcSegment> e <xref:System.Windows.Media.BezierSegment>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.PathGeometry> per creare un triangolo.  <xref:System.Windows.Media.PathGeometry> viene visualizzato tramite un elemento <xref:System.Windows.Shapes.Path>.  
  
 [!code-xml[GeometrySample#49](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#49)]  
  
 Nella figura seguente viene mostrata la forma creata nell'esempio precedente.  
  
 ![PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-pathgeometry-triangle.png "wcpsdk\_graphicsmm\_pathgeometry\_triangle")  
Triangolo creato con un oggetto PathGeometry  
  
 Nell'esempio precedente viene illustrato come creare una forma relativamente semplice, un triangolo.  È possibile utilizzare <xref:System.Windows.Media.PathGeometry> anche per creare forme più complesse, tra cui archi e curve.  Vedere ad esempio [Creare un arco ellittico](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md), [Creare una curva di Bezier cubica](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md) e [Creare una curva di Bezier quadratica.](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md).  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.GeometryDrawing>   
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989)