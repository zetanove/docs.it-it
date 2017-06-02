---
title: "Procedura: animare un oggetto lungo un percorso (animazione Double) | Microsoft Docs"
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
  - "animazione, oggetti lungo percorsi (animazione double)"
  - "Double (animazione)"
ms.assetid: 5a3c4a99-f303-42ad-a52a-e4794bb1798e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: animare un oggetto lungo un percorso (animazione Double)
In questo esempio viene illustrato come utilizzare il <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> (classe) per spostare un oggetto lungo un percorso definito da un <xref:System.Windows.Media.PathGeometry>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono utilizzati due <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> oggetti per spostare un rettangolo lungo un percorso geometrico:  
  
-   Il primo <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> anima il <xref:System.Windows.Media.TranslateTransform.X%2A> di <xref:System.Windows.Media.TranslateTransform> applicato al rettangolo. Rende il rettangolo di spostarsi in senso orizzontale lungo il percorso.  
  
-   Il secondo <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> anima il <xref:System.Windows.Media.TranslateTransform.Y%2A> di <xref:System.Windows.Media.TranslateTransform> applicato al rettangolo. Rende il rettangolo di spostarsi in senso verticale lungo il percorso.  
  
 [!code-xml[PathAnimationGallery_snippet#DoubleAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/doubleanimationusingpathexample.xaml#doubleanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#DoubleAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/DoubleAnimationUsingPathExample.cs#doubleanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#DoubleAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/DoubleAnimationUsingPathExample.vb#doubleanimationusingpathwholepage)]  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
 Un altro modo per spostare un oggetto utilizzando un percorso geometrico consiste nell'utilizzare un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> oggetto. Per un esempio, vedere [animare un oggetto lungo un percorso di (animazione Matrix)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-matrix-animation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)