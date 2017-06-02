---
title: "Procedura: aggiungere un&#39;animazione a una rotazione tridimensionale tramite quaternioni | Microsoft Docs"
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
  - "3D (conversioni), animazione, con quaternioni"
  - "animazione, 3D (conversioni), con quaternioni"
  - "quaternioni"
ms.assetid: adca9cb1-066b-4de8-abbb-6b4007579ee7
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: aggiungere un&#39;animazione a una rotazione tridimensionale tramite quaternioni
In questo esempio viene illustrata la procedura per aggiungere un'animazione a una rotazione di un oggetto tridimensionale tramite l'utilizzo di quaternioni.  
  
 Nel codice riportato di seguito viene mostrato l'utilizzo di un oggetto <xref:System.Windows.Media.Media3D.QuaternionRotation3D> come valore per la proprietà <xref:System.Windows.Media.Media3D.RotateTransform3D.Rotation%2A> di <xref:System.Windows.Media.Media3D.RotateTransform3D>.  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline1)]  
  
 A questo oggetto <xref:System.Windows.Media.Media3D.QuaternionRotation3D> viene aggiunta un'animazione mediante <xref:System.Windows.Media.Animation.QuaternionAnimation> all'interno di <xref:System.Windows.Media.Animation.Storyboard> tramite il codice riportato di seguito.  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexampleinline2)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationExample.xaml#quaternionanimationexamplewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Animare una rotazione tridimensionale utilizzando gli storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [Aggiungere un'animazione a una rotazione tridimensionale tramite Rotation3DAnimation](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)