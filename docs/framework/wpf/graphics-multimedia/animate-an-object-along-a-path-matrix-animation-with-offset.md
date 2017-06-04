---
title: "Procedura: animare un oggetto lungo un percorso (animazione Matrix con accumulazione offset) | Microsoft Docs"
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
  - "accumulazione offset"
  - "animazione, oggetti lungo percorsi (animazione matrix con accumulazione offset)"
  - "animazione Matrix con accumulazione offset"
ms.assetid: 1bca90ef-9832-4128-8ed6-62908e7ec146
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: animare un oggetto lungo un percorso (animazione Matrix con accumulazione offset)
In questo esempio viene illustrato come utilizzare il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> i valori di classe per animare un oggetto lungo un percorso e che l'animazione si accumulano con offset durante la ripetizione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> oggetto per animare il <xref:System.Windows.Media.MatrixTransform.Matrix%2A> proprietà di un <xref:System.Windows.Media.MatrixTransform> applicato a un pulsante. Di conseguenza, un pulsante si sposta lungo un percorso curvo.  
  
 Inoltre, nell'esempio viene impostato il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsOffsetCumulative%2A> proprietà `true`, in modo che l'offset della matrice animata per accumulare come la ripetizione dell'animazione. Poiché l'offset accumula, il pulsante viene spostato ulteriormente in sullo schermo quando la ripetizione dell'animazione, ma non nella posizione iniziale.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathOffsetCumulativeWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexampleoffsetcumulative.xaml#matrixanimationusingpathoffsetcumulativewholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathOffsetCumulativeWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExampleOffsetCumulative.cs#matrixanimationusingpathoffsetcumulativewholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathOffsetCumulativeWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExampleOffsetCumulative.vb#matrixanimationusingpathoffsetcumulativewholepage)]  
  
 Si noti che, sebbene il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsOffsetCumulative%2A> fa sì che valori di offset accumulare ripetizioni, ma non accumulare i valori di rotazione. Per accumulare valori di rotazione, impostare l'animazione <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> e <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.IsAngleCumulative%2A> proprietà `true`.  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028). Per un esempio che illustra come aggiungere un'animazione a un <xref:System.Windows.Media.Matrix> lungo un percorso senza accumulazione offset, vedere [animare un oggetto lungo un percorso di (animazione Matrix)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-matrix-animation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)