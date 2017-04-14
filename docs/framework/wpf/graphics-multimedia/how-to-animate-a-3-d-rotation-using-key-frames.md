---
title: "Procedura: animare una rotazione tridimensionale tramite fotogrammi chiave | Microsoft Docs"
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
  - "3D (conversioni), animazione, con fotogrammi chiave (Rotation3DAnimation)"
  - "animazione, 3D (conversioni), con fotogrammi chiave (Rotation3DAnimation)"
  - "fotogrammi chiave, Rotation3DAnimation"
ms.assetid: 6f671b95-7f30-4836-9a4f-aeb7dc30121f
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: animare una rotazione tridimensionale tramite fotogrammi chiave
Nell'esempio riportato di seguito, l'oggetto <xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames> viene utilizzato per far ruotare un oggetto tridimensionale mentre il relativo asse di rotazione viene animato generando un'oscillazione.  In questa animazione vengono utilizzati i fotogrammi chiave riportati di seguito:  
  
1.  L'oggetto <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> viene utilizzato per creare un'interpolazione lineare e uniforme tra valori.  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> viene utilizzato per creare "salti" improvvisi tra valori \(senza interpolazione\).  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> viene utilizzato per creare una transizione variabile tra valori in base alla proprietà <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A>.  Nell'esempio riportato di seguito, questa parte dell'animazione si avvia lentamente, ma accelera esponenzialmente verso la fine dell'intervallo di tempo.  
  
## Esempio  
 [!code-xml[Animation3DGallery_snip#Rotation3DAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotation3DAnimationUsingKeyFramesExample.xaml#rotation3danimationusingkeyframesexamplewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Animare una rotazione tridimensionale utilizzando gli storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)   
 [Aggiungere un'animazione a una rotazione tridimensionale tramite Rotation3DAnimation](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)   
 [Aggiungere un'animazione a una rotazione tridimensionale tramite quaternioni](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-quaternions.md)   
 [Animare a una rotazione tridimensionale utilizzando i fotogrammi chiave \(QuaternionAnimationUsingKeyFrames\)](../../../../docs/framework/wpf/graphics-multimedia/animate-a-3-d-rotation-quaternionanimationusingkeyframes.md)