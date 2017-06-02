---
title: "Procedura: ruotare un oggetto | Microsoft Docs"
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
  - "grafica, rotazione di oggetti"
  - "rotazione di oggetti"
ms.assetid: ee3466cd-e66f-4e8f-8a5a-71d77bc1e390
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: ruotare un oggetto
In questo esempio viene illustrato come ruotare un oggetto.  Viene innanzitutto creato un oggetto <xref:System.Windows.Media.RotateTransform> e quindi si specifica il relativo valore <xref:System.Windows.Media.RotateTransform.Angle%2A> in gradi.  
  
 Nell'esempio seguente un oggetto <xref:System.Windows.Shapes.Polyline> viene ruotato di 45 gradi intorno all'angolo superiore sinistro.  
  
## Esempio  
 [!code-xml[Transforms_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineabouttopleft)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineabouttopleft)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineabouttopleft)]  
  
 Le proprietà <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> di <xref:System.Windows.Media.RotateTransform> specificano il punto intorno al quale viene ruotato l'oggetto.  Questo punto centrale è espresso nello spazio delle coordinate dell'elemento trasformato.  Per impostazione predefinita, la rotazione viene applicata in corrispondenza di \(0,0\), che è l'angolo superiore sinistro dell'oggetto da trasformare.  
  
 Nell'esempio seguente viene ruotato un oggetto <xref:System.Windows.Shapes.Polyline> di 45 gradi in senso orario intorno al punto \(25,50\).  
  
 [!code-xml[Transforms_snip#RotatePolylineAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineaboutcenter)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineaboutcenter)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutCenter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineaboutcenter)]  
  
 Nell'immagine seguente sono illustrati i risultati dell'applicazione di <xref:System.Windows.Media.Transform> ai due oggetti.  
  
 ![Rotazioni di 45 gradi con punti centrali diversi](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-rotatetransform45degrees.png "wcpsdk\_graphicsmm\_rotatetransform45degrees")  
Due oggetti che ruotano di 45 gradi rispetto a centri rotazionali diversi  
  
 L'oggetto <xref:System.Windows.Shapes.Polyline> negli esempi precedenti è <xref:System.Windows.UIElement>.  Quando si applica <xref:System.Windows.Media.Transform> alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> di un oggetto <xref:System.Windows.UIElement>, è possibile utilizzare la proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> per specificare un'origine per ogni <xref:System.Windows.Media.Transform> che si applica all'elemento.  Poiché la proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> utilizza coordinate relative, è possibile applicare una trasformazione al centro dell'elemento anche se non se ne conoscono le dimensioni.  Per ulteriori informazioni e un esempio, vedere [Specificare l'origine di una trasformazione utilizzando valori relativi](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-the-origin-of-a-transform-by-using-relative-values.md).  
  
 Per l'esempio completo, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)