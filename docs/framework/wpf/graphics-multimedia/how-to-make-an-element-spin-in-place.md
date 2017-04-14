---
title: "Procedura: far ruotare sul posto un elemento | Microsoft Docs"
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
  - "classi, DoubleAnimation"
  - "classi, RotateTransform"
  - "DoubleAnimation (classe)"
  - "grafica, elementi rotanti"
  - "RotateTransform (classe)"
  - "elementi rotanti"
ms.assetid: 1f011976-8b07-4c31-9faf-019e0ddaa24c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: far ruotare sul posto un elemento
In questo esempio viene illustrato come far ruotare un elemento utilizzando una classe <xref:System.Windows.Media.RotateTransform> e una classe <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
 Nell'esempio riportato di seguito viene applicata la classe <xref:System.Windows.Media.RotateTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> dell'elemento.  Viene utilizzata una classe <xref:System.Windows.Media.Animation.DoubleAnimation> per animare la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> dell'oggetto <xref:System.Windows.Media.RotateTransform>.  Per far ruotare sul posto l'elemento, nell'esempio viene impostata la proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> dell'elemento sul punto \(0.5, 0.5\).  
  
## Esempio  
 [!code-xml[transformanimations_snip#11](../../../../samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/RotateAboutCenterExample.xaml#11)]  
  
 Per l'esempio completo, che include altre trasformazioni, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)