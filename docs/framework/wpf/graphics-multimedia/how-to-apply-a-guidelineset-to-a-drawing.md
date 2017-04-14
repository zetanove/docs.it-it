---
title: "Procedura: applicare un GuidelineSet a un disegno | Microsoft Docs"
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
  - "grafica [WPF], GuidelineSet (proprietà)"
  - "GuidelineSet (proprietà), applicazione ai disegni"
ms.assetid: 45f3e0b4-8820-45a7-b865-b8ea5b17b0c8
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: applicare un GuidelineSet a un disegno
In questo esempio viene illustrato come applicare un oggetto <xref:System.Windows.Media.GuidelineSet> a un oggetto <xref:System.Windows.Media.DrawingGroup>.  
  
 La classe <xref:System.Windows.Media.DrawingGroup> è il solo tipo di oggetto <xref:System.Windows.Media.Drawing> che presenta una proprietà <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>.  Per applicare un oggetto <xref:System.Windows.Media.GuidelineSet> ad un altro tipo di <xref:System.Windows.Media.Drawing>, aggiungerlo a un oggetto <xref:System.Windows.Media.DrawingGroup>, quindi applicare l'oggetto <xref:System.Windows.Media.GuidelineSet> a <xref:System.Windows.Media.DrawingGroup>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono creati due oggetti <xref:System.Windows.Media.DrawingGroup> praticamente identici. L'unica differenza è che il secondo oggetto <xref:System.Windows.Media.DrawingGroup> presenta un oggetto <xref:System.Windows.Media.GuidelineSet>, a differenza del primo.  
  
 Nella figura riportata di seguito viene illustrato l'output dell'esempio.  Poiché la differenza di rendering tra i due oggetti <xref:System.Windows.Media.DrawingGroup> è minima, alcune parti dei disegni sono ingrandite.  
  
 ![DrawingGroup con e senza GuidelineSet](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawinggroup-guidelineset.png "graphicsmm\_drawinggroup\_guidelineset")  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMDrawingGroupGuidelineSetExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupGuidelineSetExample.cs#graphicsmmdrawinggroupguidelinesetexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMDrawingGroupGuidelineSetExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupGuidelineSetExample.xaml#graphicsmmdrawinggroupguidelinesetexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingGroup>   
 <xref:System.Windows.Media.GuidelineSet>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)