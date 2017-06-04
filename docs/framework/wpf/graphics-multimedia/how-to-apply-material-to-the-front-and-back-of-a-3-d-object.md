---
title: "Procedura: applicare un oggetto Material alle parti anteriore e posteriore di un oggetto tridimensionale | Microsoft Docs"
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
  - "3D (oggetti), applicazione della classe Material"
  - "classi, Materiale"
  - "Material (classe), applicazione ai due lati dell'oggetto 3D"
ms.assetid: d93c8ad6-4939-4d29-9544-4d16d98093c1
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: applicare un oggetto Material alle parti anteriore e posteriore di un oggetto tridimensionale
Nell'esempio seguente viene illustrata la procedura di applicazione di un oggetto <xref:System.Windows.Media.Media3D.Material> alle parti anteriore e posteriore di un oggetto tridimensionale e l'aggiunta di un'animazione che consente di visualizzare entrambi i lati di tale oggetto.  La proprietà <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> di <xref:System.Windows.Media.Media3D.GeometryModel3D> viene utilizzata per applicare un oggetto <xref:System.Windows.Media.Brush> rosso al lato anteriore dell'oggetto, mentre la proprietà <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> di <xref:System.Windows.Media.Media3D.GeometryModel3D> viene utilizzata per applicare un oggetto <xref:System.Windows.Media.Brush> blu al lato posteriore dell'oggetto.  Nel codice riportato di seguito viene mostrata l'applicazione dei materiali all'oggetto:  
  
 [!code-xml[Animation3DGallery_snip#BackMaterialAnimationExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexampleinline1)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[Animation3DGallery_snip#BackMaterialAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexamplewholepage)]  
  
## Vedere anche  
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [Animare le proprietà Material in una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-material-properties-in-a-3-d-scene.md)   
 [Applicare EmissiveMaterial a un oggetto 3D](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-emissive-material-to-a-3-d-object.md)