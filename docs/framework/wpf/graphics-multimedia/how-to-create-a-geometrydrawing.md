---
title: "Procedura: creare un oggetto GeometryDrawing | Microsoft Docs"
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
  - "classi, GeometryDrawing"
  - "GeometryDrawing (classe)"
  - "grafica, GeometryDrawing (classe)"
  - "forme renderizzabili"
  - "forme, renderizzabili"
ms.assetid: 11d3c096-91ba-4d41-9bba-aeac0db70f97
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare un oggetto GeometryDrawing
In questo esempio viene illustrato come creare e visualizzare <xref:System.Windows.Media.GeometryDrawing>.  <xref:System.Windows.Media.GeometryDrawing> consente di creare una forma con un riempimento e un contorno associando <xref:System.Windows.Media.Pen> e <xref:System.Windows.Media.Brush> a <xref:System.Windows.Media.Geometry>.  <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> descrive la struttura della forma, <xref:System.Windows.Media.GeometryDrawing.Brush%2A> ne descrive il riempimento e <xref:System.Windows.Media.GeometryDrawing.Pen%2A> ne descrive il contorno.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.GeometryDrawing> per il rendering di una forma.  La forma è descritta da un oggetto <xref:System.Windows.Media.GeometryGroup> e due oggetti <xref:System.Windows.Media.EllipseGeometry>.  L'interno della forma viene disegnato con <xref:System.Windows.Media.LinearGradientBrush> e il contorno con <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen>.  <xref:System.Windows.Media.GeometryDrawing> viene visualizzato tramite un elemento <xref:System.Windows.Media.ImageDrawing> e un elemento <xref:System.Windows.Controls.Image>.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#GeometryDrawingExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexamplewholepage)]  
  
 Nella figura riportata di seguito viene illustrato l'oggetto <xref:System.Windows.Media.GeometryDrawing> risultante.  
  
 ![GeometryDrawing di due ellissi](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
  
 Per creare disegni più complessi, è possibile combinare più oggetti di disegno in un singolo disegno composto utilizzando <xref:System.Windows.Media.DrawingGroup>.  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingGroup>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Creare un disegno composto](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-drawing.md)