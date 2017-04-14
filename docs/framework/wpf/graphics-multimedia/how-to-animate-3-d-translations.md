---
title: "Procedura: aggiungere un&#39;animazione alle traslazioni tridimensionali | Microsoft Docs"
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
  - "3D (conversioni), animazione"
  - "animazione, 3D (conversioni)"
ms.assetid: d4eece1f-0cd2-4a2c-8370-293354c380e4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: aggiungere un&#39;animazione alle traslazioni tridimensionali
In questo argomento viene illustrata la procedura per aggiungere un'animazione a una trasformazione di traslazione impostata in un modello [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)].  
  
 Nel codice riportato di seguito viene mostrata l'applicazione di un oggetto <xref:System.Windows.Media.Media3D.TranslateTransform3D> alla proprietà <xref:System.Windows.Media.Media3D.Model3D.Transform%2A> di un oggetto <xref:System.Windows.Media.Media3D.GeometryModel3D>.  
  
 [!code-xml[Animation3DGallery_snip#Translation3DAnimationInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationinline1)]  
  
 È possibile aggiungere un'animazione alla proprietà <xref:System.Windows.Media.Media3D.TranslateTransform3D.OffsetX%2A> di tale oggetto <xref:System.Windows.Media.Media3D.TranslateTransform3D> utilizzando il codice riportato di seguito.  
  
 [!code-xml[Animation3DGallery_snip#Translation3DAnimationInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationinline2)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[Animation3DGallery_snip#Translation3DAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationexamplewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)