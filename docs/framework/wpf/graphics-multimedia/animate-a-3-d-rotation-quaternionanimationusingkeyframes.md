---
title: "Procedura: animare una rotazione tridimensionale tramite i fotogrammi chiave (QuaternionAnimationUsingKeyFrames) | Microsoft Docs"
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
  - "3D (conversioni), animazione, con fotogrammi chiave (QuaternionAnimationUsingKeyFrames)"
  - "animazione, 3D (conversioni), con fotogrammi chiave (QuaternionAnimationUsingKeyFrames)"
  - "fotogrammi chiave, QuaternionAnimationUsingKeyFrames"
ms.assetid: 09e5707b-7523-4a08-9aa7-bb13cbedccdf
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: animare una rotazione tridimensionale tramite i fotogrammi chiave (QuaternionAnimationUsingKeyFrames)
Nell'esempio seguente viene utilizzato <xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames> per ruotare un oggetto tridimensionale.  In questa animazione vengono utilizzati i fotogrammi chiave riportati di seguito:  
  
1.  L'oggetto <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> viene utilizzato per creare un'interpolazione lineare e uniforme tra valori.  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> viene utilizzato per creare "salti" improvvisi tra valori \(senza interpolazione\).  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> viene utilizzato per creare una transizione variabile tra valori in base alla proprietà <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A>.  Nell'esempio riportato di seguito, questa parte dell'animazione si avvia lentamente, ma accelera esponenzialmente verso la fine dell'intervallo di tempo.  
  
## Esempio  
 [!code-xml[Animation3DGallery_snip#QuaternionAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationUsingKeyFramesExample.xaml#quaternionanimationusingkeyframesexamplewholepage)]  
  
## Vedere anche  
 [Animare una rotazione tridimensionale utilizzando gli storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [Aggiungere un'animazione a una rotazione tridimensionale tramite Rotation3DAnimation](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [Aggiungere un'animazione a una rotazione tridimensionale tramite quaternioni](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-quaternions.md)   
 [Animare a una rotazione tridimensionale utilizzando i fotogrammi chiave \(Rotation3DAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-key-frames.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)