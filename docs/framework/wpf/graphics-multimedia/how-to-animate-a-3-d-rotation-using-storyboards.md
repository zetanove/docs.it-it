---
title: "Procedura: animare rotazioni tridimensionali tramite storyboard | Microsoft Docs"
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
  - "3D (conversioni), animazione, con gli storyboard"
  - "animazione, 3D (conversioni), con gli storyboard"
  - "Storyboard"
ms.assetid: 1020e44e-e21e-49a8-be53-53cbc1910e83
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: animare rotazioni tridimensionali tramite storyboard
Nell'esempio riportato di seguito viene illustrato come far ruotare un oggetto tridimensionale in "fuori asse" animando le proprietà <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> e <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> di un oggetto <xref:System.Windows.Media.Media3D.AxisAngleRotation3D>.  Poiché questo oggetto <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> specifica la trasformazione di rotazione dell'oggetto tridimensionale, l'animazione delle relative proprietà consente di ottenere l'effetto di rotazione desiderato.  All'interno dello storyboard, l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene utilizzato per animare la proprietà <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A>, mentre l'oggetto <xref:System.Windows.Media.Animation.Vector3DAnimation> viene utilizzato per animare la proprietà <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A>.  
  
## Esempio  
 [!code-xml[Animation3DGallery_snip#Rotate3DUsingAxisAngleRotation3DExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotat3DUsingAxisAngleRotation3DExample.xaml#rotate3dusingaxisanglerotation3dexamplewholepage)]  
  
## Vedere anche  
 [Aggiungere un'animazione a una rotazione tridimensionale tramite Rotation3DAnimation](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [Animare a una rotazione tridimensionale utilizzando i fotogrammi chiave \(Rotation3DAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-key-frames.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)