---
title: "Procedura: utilizzare un MatrixTransform per creare trasformazioni personalizzate | Microsoft Docs"
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
  - "classi, MatrixTransform"
  - "grafica [WPF], trasformazioni personalizzate"
  - "MatrixTransform (classe)"
ms.assetid: 919381ca-989f-47cf-86b4-1094060236e4
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: utilizzare un MatrixTransform per creare trasformazioni personalizzate
Nell'esempio seguente viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.MatrixTransform> per convertire \(spostare\) la posizione, l'adattamento e l'[inclinazione](GTMT) di un oggetto <xref:System.Windows.Controls.Button>.  
  
> [!NOTE]
>  Utilizzare la classe <xref:System.Windows.Media.MatrixTransform> per creare trasformazioni personalizzate che non sono fornite dalla classe <xref:System.Windows.Media.RotateTransform>, <xref:System.Windows.Media.SkewTransform>, <xref:System.Windows.Media.ScaleTransform> o <xref:System.Windows.Media.TranslateTransform>.  
  
## Esempio  
 [!code-xml[Transforms_snip#MatrixTransform](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/MatrixTransformExample.xaml#matrixtransform)]  
  
## Vedere anche  
 <xref:System.Windows.Media.MatrixTransform>   
 <xref:System.Windows.Media.Transform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)