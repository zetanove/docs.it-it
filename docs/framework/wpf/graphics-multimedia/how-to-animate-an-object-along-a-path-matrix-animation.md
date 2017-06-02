---
title: "Procedura: animare un oggetto lungo un percorso (animazione Matrix) | Microsoft Docs"
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
  - "animazione, oggetti lungo percorsi (animazione matrix)"
  - "Matrix (animazione)"
ms.assetid: 7000e697-1414-468c-b915-cf66062fc49e
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: animare un oggetto lungo un percorso (animazione Matrix)
In questo esempio viene illustrato come utilizzare il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> classe per animare un oggetto lungo un percorso definito da un <xref:System.Windows.Media.PathGeometry>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente aggiunge un'animazione a un oggetto lungo un percorso effettuando le operazioni seguenti:  
  
-   Si applica un <xref:System.Windows.Media.MatrixTransform> all'oggetto per spostarlo.  
  
-   Definisce il percorso utilizzando un <xref:System.Windows.Media.PathGeometry>.  
  
-   Crea un <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> e viene utilizzato per animare il <xref:System.Windows.Media.Matrix> proprietà del <xref:System.Windows.Media.MatrixTransform>. Il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> accetta il <xref:System.Windows.Media.PathGeometry> e viene utilizzato per generare <xref:System.Windows.Media.Matrix> valori.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexample.xaml#matrixanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExample.cs#matrixanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExample.vb#matrixanimationusingpathwholepage)]  
  
 Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028). Per ulteriori informazioni sui percorsi geometrici, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)