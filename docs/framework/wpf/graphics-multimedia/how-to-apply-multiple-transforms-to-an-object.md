---
title: "Procedura: applicare pi&#249; trasformazioni a un oggetto | Microsoft Docs"
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
  - "grafica, raggruppamento di oggetti Transform"
  - "raggruppamento di oggetti Transform"
  - "Transform (oggetti), raggruppamento"
  - "TransformGroup"
ms.assetid: 98cd1921-12bc-4bf5-8193-529228fb7402
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: applicare pi&#249; trasformazioni a un oggetto
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.TransformGroup> per raggruppare due o più oggetti <xref:System.Windows.Media.Transform> in un singolo oggetto <xref:System.Windows.Media.Transform> composito.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.TransformGroup> per applicare un oggetto <xref:System.Windows.Media.ScaleTransform> e un oggetto <xref:System.Windows.Media.RotateTransform> a un  oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[Transforms_snip#MultipleTransformExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/MultipleTransformExample.xaml#multipletransformexamplewholepage)]  
  
 [!code-csharp[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/MultipleTransformsExample.cs#multipletransformscodeexamplewholepage)]
 [!code-vb[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/MultipleTransformsExample.vb#multipletransformscodeexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.UIElement.RenderTransform%2A>   
 <xref:System.Windows.Media.TransformGroup>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252)