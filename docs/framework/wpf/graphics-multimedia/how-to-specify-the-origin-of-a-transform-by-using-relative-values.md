---
title: "Procedura: specificare l&#39;origine di una trasformazione utilizzando valori relativi | Microsoft Docs"
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
  - "grafica, origini di trasformazioni"
  - "origini di trasformazioni"
  - "Trasformazioni, origini"
ms.assetid: f4dbc29d-93c7-41cd-96d8-5cfd8624b470
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: specificare l&#39;origine di una trasformazione utilizzando valori relativi
In questo esempio viene illustrato come utilizzare valori relativi per specificare l'origine di una proprietà <xref:System.Windows.UIElement.RenderTransform%2A> applicata a <xref:System.Windows.FrameworkElement>.  
  
 Quando si utilizza la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> per ruotare, ridimensionare o [inclinare](GTMT) un oggetto <xref:System.Windows.FrameworkElement>, per impostazione predefinita la trasformazione viene applicata all'angolo superiore sinistro dell'elemento.  Se si desidera eseguire la rotazione, il ridimensionamento o l'inclinazione dal centro dell'elemento, è possibile compensare impostando il centro della trasformazione sul centro dell'elemento.  Tuttavia, questa soluzione richiede di conoscere le dimensioni dell'elemento.  Per applicare una trasformazione al centro di un elemento in modo più semplice, è possibile impostare la relativa proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> su \(0,5, 0,5\), anziché impostare un valore centrale sulla trasformazione stessa.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare un oggetto <xref:System.Windows.Controls.Button> di 45 gradi in senso orario.  Poiché nell'esempio non viene specificato un centro, il pulsante ruota intorno al punto \(0, 0\), che corrisponde all'angolo superiore sinistro.  L'oggetto <xref:System.Windows.Media.RotateTransform> viene applicato alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A>.  
  
 Nell'immagine seguente è illustrato il risultato della trasformazione per l'esempio che segue.  
  
 ![Pulsante trasformato usando RenderTransform](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm\_RenderTransformWithDefaultCenter")  
Rotazione di 45 gradi in senso orario tramite la proprietà RenderTransform  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 Anche nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare un <xref:System.Windows.Controls.Button> di 45 gradi in senso orario; tuttavia in questo esempio viene impostata la <xref:System.Windows.UIElement.RenderTransformOrigin%2A> del pulsante su \(0,5, 0,5\).  Di conseguenza, la rotazione viene applicata al centro del pulsante anziché nell'angolo superiore sinistro.  
  
 Nell'immagine seguente è illustrato il risultato della trasformazione per l'esempio che segue.  
  
 ![Pulsante trasformato rispetto al proprio centro](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformrelativecenter.png "graphicsmm\_RenderTransformRelativeCenter")  
Rotazione di 45 gradi tramite la proprietà RenderTransform con RenderTransformOrigin di \(0,5, 0,5\)  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 Per ulteriori informazioni sulla trasformazione di oggetti <xref:System.Windows.FrameworkElement>, vedere [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)