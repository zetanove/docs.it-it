---
title: "Procedura: creare una scena tridimensionale | Microsoft Docs"
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
  - "3D (scene)"
  - "creazione, 3D (scene)"
  - "scene, 3D"
ms.assetid: adb4a598-71a2-4dd5-b677-ea3fc11b78b2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare una scena tridimensionale
Nell'esempio viene illustrata la procedura per la creazione di un oggetto tridimensionale simile a un foglio di carta che è stato ruotato.  Per creare questa semplice scena tridimensionale si utilizzano <xref:System.Windows.Controls.Viewport3D> e i seguenti componenti:  
  
-   Viene creata una fotocamera utilizzando un oggetto <xref:System.Windows.Media.Media3D.PerspectiveCamera>.  La fotocamera consente di specificare quali parti della scena tridimensionale sono visibili.  
  
-   Viene creata una mesh per specificare la forma dell'oggetto tridimensionale \(foglio di carta\) utilizzando la proprietà <xref:System.Windows.Media.Media3D.GeometryModel3D.Geometry%2A> di <xref:System.Windows.Media.Media3D.GeometryModel3D>.  
  
-   Viene specificato un materiale da visualizzare sulla superficie dell'oggetto \(nell'esempio, una sfumatura lineare\) utilizzando la proprietà <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> di <xref:System.Windows.Media.Media3D.GeometryModel3D>.  
  
-   Viene creata una luce per illuminare l'oggetto utilizzando <xref:System.Windows.Media.Media3D.DirectionalLight>.  
  
## Esempio  
 Nel codice riportato di seguito viene illustrata la creazione di una scena tridimensionale in XAML.  
  
 [!code-xml[3DGallery_snip#Basic3DShapeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/Basic3DShapeExample.xaml#basic3dshapeexamplewholepage)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrata la creazione della stessa scena tridimensionale in codice procedurale.  
  
 [!code-csharp[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Basic3DShapeExample.cs#basic3dshapecodeexamplewholepage)]
 [!code-vb[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/basic3dshapeexample.vb#basic3dshapecodeexamplewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)