---
title: "Procedura: creare una riga utilizzando un oggetto LineGeometry | Microsoft Docs"
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
  - "classi, LineGeometry"
  - "grafica [WPF], linee"
  - "LineGeometry (classe)"
ms.assetid: 41231b22-1f74-4c26-a8e7-a55b29f8f6bd
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: creare una riga utilizzando un oggetto LineGeometry
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.LineGeometry> per tracciare una riga.  <xref:System.Windows.Media.LineGeometry> viene definito dai relativi punti di inizio e di fine.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare ed eseguire il rendering di <xref:System.Windows.Media.LineGeometry>.  Un elemento <xref:System.Windows.Shapes.Path> viene utilizzato per eseguire il rendering della riga.  Poiché una riga non presenta un’area, l’oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> dell’oggetto <xref:System.Windows.Shapes.Path> non viene specificato; vengono invece utilizzate le proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>.  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmlinegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmlinegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMLineGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmlinegeometryexample)]  
  
 ![LineGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-line.png "graphicsmm\_line")  
Un oggetto LineGeometry tracciato da \(10,20\) a \(100,130\)  
  
 Le altre classi di geometrie semplici includono <xref:System.Windows.Media.LineGeometry> e <xref:System.Windows.Media.EllipseGeometry>.  Queste geometrie, come quelle più complesse, possono anche essere create utilizzando un oggetto <xref:System.Windows.Media.PathGeometry> o un oggetto <xref:System.Windows.Media.StreamGeometry>.  Per ulteriori informazioni, vedere [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
## Vedere anche  
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Creare una forma composta](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)