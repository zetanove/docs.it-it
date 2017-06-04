---
title: "Procedura: applicare una trasformazione a un elemento quando si verifica un evento | Microsoft Docs"
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
  - "grafica, trasformazione come risposte di eventi"
  - "LayoutTransform (proprietà)"
  - "proprietà, LayoutTransform"
  - "proprietà, RenderTransform"
  - "RenderTransform (proprietà)"
  - "trasformazione come risposte di eventi"
ms.assetid: 71e4327e-ca57-444c-a3cf-09fb381491a0
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: applicare una trasformazione a un elemento quando si verifica un evento
In questo esempio viene mostrato come applicare <xref:System.Windows.Media.ScaleTransform> quando si verifica un evento.  Il concetto illustrato è identico a quello utilizzato per applicare altri tipi di trasformazioni.  Per ulteriori informazioni sui tipi disponibili di trasformazioni, vedere la classe <xref:System.Windows.Media.Transform> o [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md).  
  
 È possibile applicare una trasformazione a un elemento in uno dei due modi seguenti:  
  
-   Se *non* si desidera che la trasformazione influisca sul layout, utilizzare la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> dell'elemento.  
  
-   Se si desidera che la trasformazione influisca sul layout, utilizzare la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> dell'elemento.  
  
 Nell'esempio seguente viene applicata una classe <xref:System.Windows.Media.ScaleTransform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> di un pulsante.  Quando il mouse viene spostato sul pulsante, le proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> e <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> di <xref:System.Windows.Media.ScaleTransform> vengono impostate su `2`, ingrandendo in questo modo il pulsante.  Quando il mouse viene spostato dal pulsante, le proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> e <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> vengono impostate su `1`, ripristinando le dimensioni originali del pulsante.  
  
## Esempio  
 [!code-xml[ButtonTransform#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml#1)]  
  
 [!code-csharp[ButtonTransform#1cb](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ButtonTransform/CSharp/ButtonTransformExample.xaml.cs#1cb)]
 [!code-vb[ButtonTransform#1cb](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ButtonTransform/VisualBasic/ButtonTransformExample.xaml.vb#1cb)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.ScaleTransform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)