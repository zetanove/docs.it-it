---
title: "Procedura: definire un rettangolo utilizzando RectangleGeometry | Microsoft Docs"
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
  - "classi, RectangleGeometry"
  - "grafica [WPF], rettangoli"
  - "RectangleGeometry (classe)"
  - "rettangoli, creazione con la classe RectangleGeometry"
ms.assetid: e40b8a8e-54b8-416b-a9f2-be6dca9fdf0b
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: definire un rettangolo utilizzando RectangleGeometry
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.RectangleGeometry> per tracciare un rettangolo.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare ed eseguire il rendering di un oggetto <xref:System.Windows.Media.RectangleGeometry>.  La posizione relativa e le dimensioni del rettangolo vengono definite da una struttura <xref:System.Windows.Rect>.  La posizione relativa è `50,50` e l'altezza e la larghezza sono entrambe `25`, valori che consentono la creazione di un quadrato.  L'interno del rettangolo viene disegnato con un pennello <xref:System.Windows.Media.Brushes.LemonChiffon%2A>, mentre il contorno con un tratto di spessore <xref:System.Windows.Media.Brushes.Black%2A> pari a `1`.  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/GeometryExamples.xaml#graphicsmmrectanglegeometryexample)]  
  
 [!code-csharp[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/CSharp/GeometryExamples.cs#graphicsmmrectanglegeometryexample)]
 [!code-vb[GeometryOverviewSamples_procedural_snip#GraphicsMMRectangleGeometryExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometryOverviewSamples_procedural_snip/visualbasic/geometryexamples.vb#graphicsmmrectanglegeometryexample)]  
  
 ![RectangleGeometry](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rectangle.png "graphicsmm\_rectangle")  
RectangleGeometry  
  
 Anche se in questo esempio viene utilizzato un elemento <xref:System.Windows.Shapes.Path> per eseguire il rendering dell'oggetto <xref:System.Windows.Media.RectangleGeometry>, esistono molti altri modi per utilizzare gli oggetti <xref:System.Windows.Media.RectangleGeometry>.  Ad esempio, un oggetto <xref:System.Windows.Media.RectangleGeometry> può essere utilizzato per specificare la proprietà <xref:System.Windows.UIElement.Clip%2A> di un oggetto <xref:System.Windows.UIElement> o la proprietà <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> di un oggetto <xref:System.Windows.Media.GeometryDrawing>.  
  
 Le altre classi di geometrie semplici includono <xref:System.Windows.Media.LineGeometry> e <xref:System.Windows.Media.EllipseGeometry>.  Queste geometrie, come quelle più complesse, possono anche essere create utilizzando un oggetto <xref:System.Windows.Media.PathGeometry> o un oggetto <xref:System.Windows.Media.StreamGeometry>.  
  
## Vedere anche  
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Creare una forma composta](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)