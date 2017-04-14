---
title: "Procedura: animare propriet&#224; materiali in una scena tridimensionale | Microsoft Docs"
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
  - "3D (scene), animazione delle proprietà Material"
  - "animazione, proprietà Material nelle scene 3D"
  - "Material (proprietà), animazione nelle scene 3D"
ms.assetid: 229fd6eb-7401-4992-b0c9-8b28de230c0f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: animare propriet&#224; materiali in una scena tridimensionale
In questo esempio viene illustrato come animare la proprietà <xref:System.Windows.Media.Brush.Opacity%2A> di <xref:System.Windows.Media.Media3D.Material> applicato a un modello [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)].  
  
 Nell'esempio di codice riportato di seguito viene definito l'oggetto <xref:System.Windows.Media.LinearGradientBrush> utilizzato come <xref:System.Windows.Media.Media3D.Material> applicato all'oggetto tridimensionale.  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline1)]  
  
 La proprietà <xref:System.Windows.Media.Brush.Opacity%2A> di questo oggetto <xref:System.Windows.Media.LinearGradientBrush> viene animata utilizzando l'esempio di codice riportato di seguito.  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline2)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexamplewholepage)]  
  
## Vedere anche  
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)