---
title: "Procedura: ruotare un oggetto utilizzando un percorso geometrico (animazione Matrix) | Microsoft Docs"
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
  - "percorsi geometrici, rotazione di oggetti"
  - "rotazione di oggetti tramite percorsi geometrici"
  - "Matrix (animazione)"
ms.assetid: 877dc9aa-6bdc-4beb-8772-3efaec32c0f0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: ruotare un oggetto utilizzando un percorso geometrico (animazione Matrix)
In questo esempio viene illustrato come utilizzare un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> e <xref:System.Windows.Media.MatrixTransform> per ruotare un oggetto lungo un percorso geometrico definito da un <xref:System.Windows.Media.PathGeometry> oggetto.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> oggetto per animare il <xref:System.Windows.Media.MatrixTransform.Matrix%2A> proprietà di un <xref:System.Windows.Media.MatrixTransform>. Il <xref:System.Windows.Media.MatrixTransform> viene applicato a un pulsante e determina lo spostamento lungo un percorso curvo. Poiché il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> è impostata su `true`, il rettangolo ruota lungo la tangente del percorso.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
 La versione del codice dell'esempio precedente usato un <xref:System.Windows.Media.Animation.Storyboard> per animare il <xref:System.Windows.Media.EllipseGeometry>, anche se è stata applicata un'unica animazione. Per applicare una singola animazione a una proprietà nel codice in modo più semplice consiste nell'utilizzare il <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> metodo. Per un esempio, vedere [animare una proprietà senza utilizzare uno Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)   
 [Esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028)