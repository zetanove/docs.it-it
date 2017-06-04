---
title: "Procedura: disegnare un&#39;area con una sfumatura lineare | Microsoft Docs"
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
  - "pennelli, disegno con sfumature lineari"
  - "gradienti lineari, disegno"
  - "disegno, con sfumature lineari"
ms.assetid: 00e0cd04-48c0-4ec5-850e-d321beb37a34
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: disegnare un&#39;area con una sfumatura lineare
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.LinearGradientBrush> per disegnare un'area con una sfumatura lineare.  Nell'esempio riportato di seguito <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Rectangle> viene disegnato con una sfumatura lineare diagonale che passa dal giallo al rosso al blu al verde limone.  
  
## Esempio  
 [!code-xml[GradientBrushExamples_snip#DiagonalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]  
  
 Nell'immagine riportata di seguito viene illustrata la sfumatura creata nell'esempio precedente.  
  
 ![Sfumatura lineare diagonale](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-diagonallgb.png "graphicsmm\_DiagonalLGB")  
  
 Per creare una sfumatura lineare orizzontale, impostare <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> e <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> di <xref:System.Windows.Media.LinearGradientBrush> su \(0,0.5\) and \(1,0.5\).  Nell'esempio riportato di seguito <xref:System.Windows.Shapes.Rectangle> viene disegnato con una sfumatura lineare orizzontale.  
  
 [!code-xml[GradientBrushExamples_snip#HorizontalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]  
  
 Nell'immagine riportata di seguito viene illustrata la sfumatura creata nell'esempio precedente.  
  
 ![Sfumatura lineare orizzontale](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-horizontallgb.png "graphicsmm\_HorizontalLGB")  
  
 Per creare una sfumatura lineare verticale, impostare <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> e <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> di <xref:System.Windows.Media.LinearGradientBrush> su \(0.5,0\) and \(0.5,1\).  Nell'esempio riportato di seguito <xref:System.Windows.Shapes.Rectangle> viene disegnato con una sfumatura lineare verticale.  
  
 [!code-xml[GradientBrushExamples_snip#VerticalGradient1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]  
  
 Nell'immagine riportata di seguito viene illustrata la sfumatura creata nell'esempio precedente.  
  
 ![Sfumatura lineare verticale](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-verticallgb.png "graphicsmm\_VerticalLGB")  
  
> [!NOTE]
>  Negli esempi di questo argomento viene utilizzato il sistema di coordinate predefinito per impostare i punti iniziali e quelli finali.  Il sistema di coordinate predefinito è relativo a un riquadro delimitatore del testo, dove 0 e 1 indicano rispettivamente lo 0% e il 100% del riquadro delimitatore del testo.  Tale sistema di coordinate può essere modificato impostando la proprietà <xref:System.Windows.Media.GradientBrush.MappingMode%2A> sul valore <xref:System.Windows.Media.BrushMappingMode?displayProperty=fullName>.  Un sistema di coordinate assoluto non è relativo a un riquadro delimitatore del testo.  I valori vengono interpretati direttamente nello spazio locale.  
  
 Per ulteriori esempi, vedere [Esempio Brush](http://go.microsoft.com/fwlink/?LinkID=159973) \(la pagina potrebbe essere in inglese\).  Per ulteriori informazioni sulle sfumature e su altri tipi di pennelli, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).