---
title: "Procedura: applicare un disegno a un modello tridimensionale | Microsoft Docs"
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
  - "3D (modelli), applicazione di disegni"
  - "disegni, applicazione ai modelli 3D"
ms.assetid: 68357577-b7fc-446e-8be9-a8cc7df3a350
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: applicare un disegno a un modello tridimensionale
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.DrawingBrush> come <xref:System.Windows.Media.Media3D.Material> applicato a un modello [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)].  
  
 Nel codice riportato di seguito viene definito un oggetto <xref:System.Windows.Media.DrawingGroup> come contenuto di un oggetto <xref:System.Windows.Media.DrawingBrush>.  L'oggetto <xref:System.Windows.Media.DrawingBrush> viene impostato come proprietà <xref:System.Windows.Media.Media3D.DiffuseMaterial.Brush%2A> di <xref:System.Windows.Media.Media3D.DiffuseMaterial> applicata a un piano [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)].  
  
 **Nota:** è spesso opportuno definire oggetti e valori complessi, come il disegno riportato di seguito, come risorse che possono essere riutilizzate e che semplificano il codice.  Per ulteriori informazioni, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 [!code-xml[3DGallery_snip#ApplyDrawingToMaterialInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialinline1)]  
  
## Esempio  
 Nel codice riportato di seguito viene illustrato l'esempio completo.  
  
 [!code-xml[3DGallery_snip#ApplyDrawingToMaterialExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialexamplewholepage)]  
  
## Vedere anche  
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Creare una scena tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Cenni preliminari sulla grafica tridimensionale](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)