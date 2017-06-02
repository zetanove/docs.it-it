---
title: "Procedura: arrotondare gli angoli di un oggetto RectangleGeometry | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "angoli, arrotondamento"
  - "grafica, arrotondamento degli angoli di oggetti RectangleGeometry"
  - "RectangleGeometry (classe), arrotondamento degli angoli"
  - "arrotondamento degli angoli di oggetti RectangleGeometry"
ms.assetid: 926644bc-1357-4c0b-ac81-694bd090ae87
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: arrotondare gli angoli di un oggetto RectangleGeometry
Per arrotondare gli angoli di un oggetto <xref:System.Windows.Media.RectangleGeometry>, impostare le proprietà <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> e <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> dell'oggetto su un valore maggiore di zero.  Maggiori sono i valori, più rotondi sono gli angoli del rettangolo.  
  
## Esempio  
 Nell'esempio seguente vengo mostrati diversi oggetti <xref:System.Windows.Media.RectangleGeometry> con impostazioni <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> e <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> differenti.  Gli oggetti <xref:System.Windows.Media.RectangleGeometry> vengono visualizzati mediante elementi <xref:System.Windows.Shapes.Path>.  
  
 [!code-xml[GeometryOverviewSamples_snip#GraphicsMMRoundedRectangleGeometryExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/RectangleGeometryRoundedCornerExample.xaml#graphicsmmroundedrectanglegeometryexamplewholepage)]  
  
 ![Rettangoli con impostazioni RadiusX&#47;RadiusY diverse](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rounded.png "graphicsmm\_rounded")  
Rettangoli con gli angoli arrotondati  
  
## Vedere anche  
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Creare una forma composta](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-composite-shape.md)   
 [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)