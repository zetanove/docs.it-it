---
title: "Procedura: creare pi&#249; percorsi secondari in un PathGeometry | Microsoft Docs"
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
  - "grafica [WPF], percorsi secondari"
  - "più percorsi secondari"
  - "PathGeometry (classe)"
  - "percorsi secondari"
ms.assetid: 104a862c-dde2-4e62-ac87-80660dd1681c
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare pi&#249; percorsi secondari in un PathGeometry
In questo esempio viene illustrato come creare più percorsi secondari in un oggetto <xref:System.Windows.Media.PathGeometry>.  Per creare più percorsi secondari, viene creato un oggetto <xref:System.Windows.Media.PathFigure> per ogni percorso secondario.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono creati due percorsi secondari, ciascuno dei quali è un triangolo.  
  
 [!code-xml[GeometrySample#38](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#38)]  
  
 Nell'esempio riportato di seguito viene illustrato come creare più percorsi secondari utilizzando un oggetto <xref:System.Windows.Shapes.Path> e la sintassi di attributo di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Ogni `M` crea un nuovo percorso secondario, pertanto vengono creati due percorsi secondari ciascuno dei quali disegna un triangolo.  
  
 [!code-xml[GeometrySample#58](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#58)]  
  
 Si noti che la sintassi di attributo crea in effetti un oggetto <xref:System.Windows.Media.StreamGeometry>, una versione più semplice di un oggetto <xref:System.Windows.Media.PathGeometry>.  Per ulteriori informazioni, vedere la pagina [Sintassi di markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md).  
  
## Vedere anche  
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)