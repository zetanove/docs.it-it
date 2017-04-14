---
title: "Procedura: animare un oggetto lungo un percorso (animazione Point) | Microsoft Docs"
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
  - "animazione, oggetti lungo percorsi (animazione point)"
  - "animazione Point"
ms.assetid: 1fa3f817-35bc-41a1-b366-f5a20b70da0c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: animare un oggetto lungo un percorso (animazione Point)
In questo esempio viene illustrato come utilizzare un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> oggetto per animare un <xref:System.Windows.Point> lungo un percorso curvo.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente sposta un <xref:System.Windows.Media.EllipseGeometry> lungo un percorso definito da un <xref:System.Windows.Media.PathGeometry>. La geometria dell'ellisse <xref:System.Windows.Media.EllipseGeometry.Center%2A> proprietà, che accetta un <xref:System.Windows.Point> valore, specifica la posizione; per spostare la geometria dell'ellisse, si anima la <xref:System.Windows.Media.EllipseGeometry.Center%2A> proprietà. Nell'esempio viene utilizzato un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> per animare il <xref:System.Windows.Media.EllipseGeometry> dell'oggetto <xref:System.Windows.Media.EllipseGeometry.Center%2A> proprietà.  
  
 [!code-xml[PathAnimationGallery_snippet#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/pointanimationusingpathexample.xaml#pointanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/PointAnimationUsingPathExample.cs#pointanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/PointAnimationUsingPathExample.vb#pointanimationusingpathwholepage)]  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
 La versione del codice dell'esempio precedente usato un <xref:System.Windows.Media.Animation.Storyboard> per animare il <xref:System.Windows.Media.EllipseGeometry>, anche se è stata applicata un'unica animazione. Oggetto <xref:System.Windows.Media.Animation.Storyboard> è spesso il modo più semplice per applicare più animazioni, poiché è possono controllare queste animazioni dallo stesso <xref:System.Windows.Media.Animation.Storyboard>. Tuttavia, per applicare una singola animazione a una proprietà quando si utilizza codice in modo più semplice consiste nell'utilizzare il <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> metodo. Per un esempio, vedere [animare una proprietà senza utilizzare uno Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)