---
title: "Procedura: ruotare un oggetto utilizzando un percorso geometrico | Microsoft Docs"
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
ms.assetid: cb31ca4d-f05a-4c6b-9a18-4b6faaf38d45
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: ruotare un oggetto utilizzando un percorso geometrico
In questo esempio viene illustrato come ruotare un oggetto lungo un percorso geometrico definito da un <xref:System.Windows.Media.PathGeometry> oggetto.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono utilizzati tre <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> oggetti per spostare un rettangolo lungo un percorso geometrico.  
  
-   Il primo <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> anima un <xref:System.Windows.Media.RotateTransform> che viene applicato al rettangolo. L'animazione genera valori angolari. Rende il rettangolo ruotare lungo i contorni del percorso.  
  
-   I due oggetti animano il <xref:System.Windows.Media.TranslateTransform.X%2A> e <xref:System.Windows.Media.TranslateTransform.Y%2A> valori di un <xref:System.Windows.Media.TranslateTransform> che viene applicato al rettangolo. Effettuano il rettangolo spostare orizzontalmente e verticalmente lungo il percorso.  
  
 [!code-xml[PathAnimationGallery_snippet#RotateAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/rotateanimationusingpathexample.xaml#rotateanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#RotateAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/RotateAnimationUsingPathExample.cs#rotateanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#RotateAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/RotateAnimationUsingPathExample.vb#rotateanimationusingpathwholepage)]  
  
 Un altro modo per ruotare un oggetto utilizzando un percorso geometrico consiste nell'utilizzare un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> e impostare il relativo <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> proprietà `true`. Per ulteriori informazioni e un esempio, vedere [ruotare un oggetto utilizzando un percorso geometrico (animazione Matrix)](../../../../docs/framework/wpf/graphics-multimedia/how-to-rotate-an-object-by-using-a-geometric-path-matrix-animation.md).  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)