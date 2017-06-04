---
title: "Procedura: ridimensionare un elemento | Microsoft Docs"
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
  - "classi, ScaleTransform"
  - "grafica, ridimensionamento di elementi"
  - "ScaleTransform (classe)"
  - "adattamento, elementi"
ms.assetid: 18158d94-bbe7-4f6a-814e-84d27fa748bf
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: ridimensionare un elemento
In questo esempio viene illustrato come utilizzare <xref:System.Windows.Media.ScaleTransform> per ridimensionare un elemento.  
  
 Utilizzare le proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> e <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> per ridimensionare l'elemento in base al fattore specificato.  Ad esempio un valore di <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> pari a 1,5 estendel'elemento fino al 150% della larghezza originale.  Un valore di <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> pari a 0,5 riduce l'altezza di un elemento del 50%.  
  
 Utilizzare le proprietà <xref:System.Windows.Media.ScaleTransform.CenterX%2A> e <xref:System.Windows.Media.ScaleTransform.CenterY%2A> per specificare il punto centrale dell'operazione di ridimensionamento.  Per impostazione predefinita, <xref:System.Windows.Media.ScaleTransform> viene centrato in corrispondenza del punto \(0,0\) che corrisponde all'angolo superiore sinistro del rettangolo.  Ne consegue che l'elemento viene spostato e appare più grande, poiché quando si applica <xref:System.Windows.Media.Transform> viene modificato lo spazio delle coordinate in cui risiede l'oggetto.  
  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.ScaleTransform> per raddoppiare le dimensioni di un oggetto <xref:System.Windows.Shapes.Rectangle> 50 x 50.  <xref:System.Windows.Media.ScaleTransform> ha un valore pari a 0 \(impostazione predefinita\) sia per <xref:System.Windows.Media.ScaleTransform.CenterX%2A>, sia per <xref:System.Windows.Media.ScaleTransform.CenterY%2A>.  
  
## Esempio  
 [!code-xml[transformsSample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#21)]  
  
 In genere, <xref:System.Windows.Media.ScaleTransform.CenterX%2A> e <xref:System.Windows.Media.ScaleTransform.CenterY%2A> vengono impostati sul centro dell'oggetto ridimensionato: \(<xref:System.Windows.FrameworkElement.Width%2A>\/2, <xref:System.Windows.FrameworkElement.Height%2A>\/2\).  
  
 Nell'esempio riportato di seguito viene illustrato un altro oggetto <xref:System.Windows.Shapes.Rectangle> con le dimensioni raddoppiate, benché <xref:System.Windows.Media.ScaleTransform> presenti un valore di 25 per <xref:System.Windows.Media.ScaleTransform.CenterX%2A> e <xref:System.Windows.Media.ScaleTransform.CenterY%2A>, che corrisponde al centro del rettangolo.  
  
 [!code-xml[transformsSample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/ScaleTransformExample.xaml#22)]  
  
 Nella figura riportata di seguito viene illustrata la differenza tra le due operazioni <xref:System.Windows.Media.ScaleTransform>.  La linea punteggiata indica la dimensione e la posizione del rettangolo prima del ridimensionamento.  
  
 ![Ridimensionamenti con raddoppiamento di valore con punti centrali diversi](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-scalecenter.png "wcpsdk\_graphicsmm\_scalecenter")  
Due operazioni ScaleTransform con valori ScaleX e ScaleY identici, ma con centri diversi  
  
 Per l'esempio completo, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.ScaleTransform>   
 [Cenni preliminari sulle trasformazioni](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)