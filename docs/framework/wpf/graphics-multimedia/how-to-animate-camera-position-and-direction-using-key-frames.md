---
title: "Procedura: animare la posizione e la direzione di una fotocamera tramite fotogrammi chiave | Microsoft Docs"
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
  - "animazione, direzione della fotocamera con fotogrammi chiave"
  - "animazione, posizione della fotocamera con fotogrammi chiave"
  - "direzione della fotocamera, animazione con fotogrammi chiave"
  - "posizione della fotocamera, animazione con fotogrammi chiave"
  - "fotogrammi chiave, animazione della direzione della fotocamera"
  - "fotogrammi chiave, animazione della posizione della fotocamera"
ms.assetid: 5753024e-0057-454d-947f-43ea686879c7
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: animare la posizione e la direzione di una fotocamera tramite fotogrammi chiave
Nell'esempio riportato di seguito, viene utilizzato <xref:System.Windows.Media.Animation.Point3DAnimationUsingKeyFrames> per animare la posizione di un oggetto <xref:System.Windows.Media.Media3D.PerspectiveCamera> in una scena 3D.  Inoltre, <xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames> viene utilizzato per animare la direzione in cui è puntata la fotocamera nella scena 3D.  Entrambe le animazioni utilizzano molti fotogrammi chiave che creano una serie di effetti di animazione:  
  
1.  <xref:System.Windows.Media.Animation.LinearPoint3DKeyFrame> e <xref:System.Windows.Media.Animation.LinearVector3DKeyFrame> vengono utilizzati per creare un'interpolazione omogenea e lineare tra i valori.  
  
2.  <xref:System.Windows.Media.Animation.DiscretePoint3DKeyFrame> e <xref:System.Windows.Media.Animation.DiscreteVector3DKeyFrame> vengono utilizzati per creare "salti" improvvisi tra i valori \(nessuna interpolazione\).  
  
3.  <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame> e <xref:System.Windows.Media.Animation.SplineVector3DKeyFrame> vengono utilizzati per creare una transizione variabile tra i valori in base alla proprietà <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame.KeySpline%2A>.  Nell'esempio riportato di seguito l'animazione si avvia lentamente ma accelera in modo esponenziale verso la fine dell'intervallo di tempo.  
  
## Esempio  
 [!code-xml[Animation3DGallery_snip#PointVector3DAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationUsingKeyFramesExample.xaml#pointvector3danimationusingkeyframesexamplewholepage)]  
  
## Vedere anche  
 [Animare la posizione e la direzione di una fotocamera in una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-camera-position-and-direction-in-a-3d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)