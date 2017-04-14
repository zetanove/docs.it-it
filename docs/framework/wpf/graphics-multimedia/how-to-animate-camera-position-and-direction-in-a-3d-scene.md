---
title: "Procedura: animare la posizione e la direzione di una fotocamera in una scena tridimensionale | Microsoft Docs"
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
  - "3D (scene), animazione della direzione della fotocamera"
  - "3D (scene), animazione della posizione della fotocamera"
  - "animazione, direzione della fotocamera nelle scene 3D"
  - "animazione, posizione della fotocamera nelle scene 3D"
  - "direzione della fotocamera, animazione nelle scene 3D"
  - "posizione della fotocamera, animazione nelle scene 3D"
ms.assetid: 480224b7-a5e5-4165-ba7f-ef760ddff94a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: animare la posizione e la direzione di una fotocamera in una scena tridimensionale
Nell'esempio riportato di seguito viene illustrato come animare la posizione e la direzione di una fotocamera in una scena tridimensionale.  Questa operazione viene eseguita utilizzando <xref:System.Windows.Media.Animation.Point3DAnimation> e <xref:System.Windows.Media.Animation.Vector3DAnimation> per animare le proprietà <xref:System.Windows.Media.Media3D.ProjectionCamera.Position%2A> e <xref:System.Windows.Media.Media3D.ProjectionCamera.LookDirection%2A> rispettivamente di <xref:System.Windows.Media.Media3D.PerspectiveCamera>.  È possibile utilizzare un'animazione come questa per impostare la visualizzazione dello spettatore di una scena in risposta a un evento.  
  
## Esempio  
 [!code-xml[Animation3DGallery_snip#PointVector3DAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationExample.xaml#pointvector3danimationexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.Vector3DAnimation>   
 <xref:System.Windows.Media.Animation.Point3DAnimation>   
 [Animare la posizione e la direzione di una fotocamera utilizzando i fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-camera-position-and-direction-using-key-frames.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)