---
title: "Procedura: inclinare un elemento | Microsoft Docs"
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
  - "classi, SkewTransform"
  - "grafica, inclinazione di elementi"
  - "inclinazione di elementi"
  - "SkewTransform (classe)"
ms.assetid: 56b65f2f-dc6e-4238-923f-ca44ec53c52f
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: inclinare un elemento
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.SkewTransform> per inclinare un elemento.  Un'[inclinazione](GTMT), nota anche come distorsione, è una trasformazione che estende lo spazio delle coordinate in modo non uniforme.  Un utilizzo tipico di un oggetto <xref:System.Windows.Media.SkewTransform> è la simulazione della profondità [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)] in oggetti [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)].  
  
 Utilizzare le proprietà <xref:System.Windows.Media.SkewTransform.CenterX%2A> e <xref:System.Windows.Media.SkewTransform.CenterY%2A> per specificare il punto centrale dell'oggetto <xref:System.Windows.Media.SkewTransform>.  
  
 Utilizzare le proprietà <xref:System.Windows.Media.SkewTransform.AngleX%2A> e <xref:System.Windows.Media.SkewTransform.AngleY%2A> per specificare l'angolo di inclinazione dell'asse x e dell'asse y e per inclinare il sistema di coordinate corrente lungo questi assi.  
  
 Per prevedere l'effetto di una trasformazione di inclinazione, considerare che la proprietà <xref:System.Windows.Media.SkewTransform.AngleX%2A> inclina i valori dell'asse x relativi al sistema di coordinate originale.  Di conseguenza, per una proprietà <xref:System.Windows.Media.SkewTransform.AngleX%2A> pari a 30, l'asse y ruota di 30 gradi rispetto all'origine e inclina i valori nell'asse x di 30 gradi rispetto a tale origine.  Analogamente, una proprietà <xref:System.Windows.Media.SkewTransform.AngleY%2A> pari a 30 inclina i valori dell'asse y della forma di 30 gradi rispetto all'origine.  Si noti che questo non è lo stesso effetto ottenuto traslando \(spostando\) il sistema di coordinate di 30 gradi sull'asse x o y.  
  
 Nell'esempio riportato di seguito viene applicata un'inclinazione orizzontale di 45 gradi a un oggetto <xref:System.Windows.Shapes.Rectangle> da un punto centrale di \(0,0\).  
  
## Esempio  
 [!code-xml[transformsSample#41](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#41)]  
  
 Nell'esempio riportato di seguito viene applicata un'inclinazione orizzontale di 45 gradi a un oggetto <xref:System.Windows.Shapes.Rectangle> da un punto centrale di \(25,25\).  
  
 [!code-xml[transformsSample#42](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#42)]  
  
 Nell'esempio riportato di seguito viene applicata un'inclinazione verticale di 45 gradi a un oggetto <xref:System.Windows.Shapes.Rectangle> da un punto centrale di \(25,25\).  
  
 [!code-xml[transformsSample#43](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#43)]  
  
 Nell'illustrazione riportata di seguito vengono illustrate le diverse inclinazioni utilizzate in questo esempio.  
  
 ![Esempi di SkewTransform](../../../../docs/framework/wpf/graphics-multimedia/media/img-wcpsdk-graphicsmm-skewtransformexample.png "img\_wcpsdk\_graphicsmm\_skewtransformexample")  
Illustrazione dei tre esempi di SkewTransform  
  
 Per l'esempio completo, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.SkewTransform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)