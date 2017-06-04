---
title: "Procedura: ridimensionare un modello tridimensionale | Microsoft Docs"
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
  - "3D (oggetti), adattamento"
  - "adattamento, 3D (oggetti)"
ms.assetid: f3fdfe33-f7dc-44b0-84a5-e43b89947f35
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: ridimensionare un modello tridimensionale
In questo esempio viene illustrata la procedura per ridimensionare un oggetto tridimensionale.  Per ridimensionare un oggetto tridimensionale, utilizzare <xref:System.Windows.Media.Media3D.ScaleTransform3D>.  Le proprietà <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A>, <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A> e <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A> ridimensionano l'elemento con il fattore specificato.  Ad esempio un valore <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A> di 1,5 estende un oggetto fino al 150% della larghezza originale.  Un valore <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A> di 0,5 riduce l'altezza di un oggetto per il 50%.  Nel codice riportato di seguito viene mostrato l'utilizzo di un oggetto <xref:System.Windows.Media.Media3D.ScaleTransform3D> come valore per la trasformazione di <xref:System.Windows.Media.Media3D.GeometryModel3D>.  
  
 [!code-xml[3DGallery_snip#ScaleTransform3DExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexampleinline1)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[3DGallery_snip#ScaleTransform3DExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexamplewholepage)]  
  
## Vedere anche  
 [Aggiungere un'animazione alle conversioni tridimensionali](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-3-d-translations.md)   
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)