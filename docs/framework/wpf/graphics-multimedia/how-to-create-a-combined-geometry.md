---
title: "Procedura: creare una geometria combinata | Microsoft Docs"
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
  - "combinazione di geometrie"
  - "geometrie, combinazione"
  - "grafica, combinazione di geometrie"
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare una geometria combinata
In questo esempio viene illustrato come combinare le geometrie.  Per combinare due geometrie, utilizzare un oggetto <xref:System.Windows.Media.CombinedGeometry>.  Impostare le proprietà <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> con le due geometrie da combinare e impostare la proprietà <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A>, che determina il modo in cui le geometrie saranno combinate insieme, su `Union`, `Intersect`, `Exclude` o `Xor`.  
  
 Per creare una geometria composta da due o più geometrie, utilizzare <xref:System.Windows.Media.GeometryGroup>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definito <xref:System.Windows.Media.CombinedGeometry> con una modalità di combinazione di geometrie impostata su `Exclude`.  Entrambi gli oggetti <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> sono definiti come cerchi dello stesso raggio, ma con offset dei centri di 50.  
  
 [!code-xml[GeometrySample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![Risultati della modalità di combinazione Exclude](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-exclude.png "mil\_task\_combined\_geometry\_exclude")  
Geometria combinata Exclude  
  
 Nel markup riportato di seguito viene definito <xref:System.Windows.Media.CombinedGeometry> con una modalità di combinazione `Intersect`.  Entrambi gli oggetti <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> sono definiti come cerchi dello stesso raggio, ma con offset dei centri di 50.  
  
 [!code-xml[GeometrySample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![Risultati della modalità di combinazione Intersect](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-intersect.png "mil\_task\_combined\_geometry\_intersect")  
Geometria combinata Intersect  
  
 Nel markup riportato di seguito viene definito <xref:System.Windows.Media.CombinedGeometry> con una modalità di combinazione `Union`.  Entrambi gli oggetti <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> sono definiti come cerchi dello stesso raggio, ma con offset dei centri di 50.  
  
 [!code-xml[GeometrySample#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Risultati della modalità di combinazione Union](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-union.png "mil\_task\_combined\_geometry\_union")  
Geometria combinata Union  
  
 Nel markup riportato di seguito viene definito <xref:System.Windows.Media.CombinedGeometry> con una modalità di combinazione `Xor`.  Entrambi gli oggetti <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> e <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> sono definiti come cerchi dello stesso raggio, ma con offset dei centri di 50.  
  
 [!code-xml[GeometrySample#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Risultati della modalità di combinazione Xor](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-xor.png "mil\_task\_combined\_geometry\_xor")  
Geometria combinata Xor