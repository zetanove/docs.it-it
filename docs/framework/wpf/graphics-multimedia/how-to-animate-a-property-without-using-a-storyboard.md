---
title: "Procedura: animare una propriet&#224; senza utilizzare uno storyboard | Microsoft Docs"
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
  - "animazione, non storyboard (locale)"
  - "locale (animazione)"
  - "non storyboard (animazione)"
ms.assetid: d411db70-4df7-487d-82bc-95a7c1b2e7f8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: animare una propriet&#224; senza utilizzare uno storyboard
In questo esempio viene illustrata una delle modalità disponibili per applicare un'animazione a una proprietà senza utilizzare un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  
  
> [!NOTE]
>  Questa funzionalità non è disponibile in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Per informazioni sull'animazione di proprietà in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], vedere [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md).  
  
 Per applicare un'animazione locale a una proprietà, utilizzare il metodo <xref:System.Windows.UIElement.BeginAnimation%2A>.  Questo metodo accetta due parametri: <xref:System.Windows.DependencyProperty>, che specifica la proprietà da animare, e l'animazione da applicare a tale proprietà.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come animare la larghezza e il colore di sfondo di un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-cpp[animateproperty#11](../../../../samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
 Lo spazio dei nomi <xref:System.Windows.Media.Animation> contiene un'ampia varietà di classi per l'animazione di diversi tipi di proprietà.  Per ulteriori informazioni sull'animazione di proprietà, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  Per ulteriori informazioni sulle[proprietà di dipendenza](GTMT), ossia il tipo di proprietà illustrate in questi esempi, e sulle relative funzionalità, vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
 È anche possibile applicare animazioni senza utilizzare gli oggetti <xref:System.Windows.Media.Animation.Storyboard>. Per ulteriori informazioni, vedere [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.AnimationTimeline>   
 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>   
 <xref:System.Windows.Media.Animation>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)