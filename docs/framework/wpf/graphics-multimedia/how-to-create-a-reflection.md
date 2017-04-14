---
title: "Procedura: creare una reflection | Microsoft Docs"
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
  - "pennelli, creazione di riflessi"
  - "creazione di riflessi"
  - "riflessi, creazione"
ms.assetid: 4f017e16-ab80-43c7-98df-03b6bddbb203
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: creare una reflection
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.VisualBrush> per creare una reflection.  Poiché un oggetto <xref:System.Windows.Media.VisualBrush> è in grado di visualizzare un elemento visivo esistente, è possibile utilizzare questa funzionalità per produrre effetti visivi interessanti, ad esempio reflection e ingrandimento.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.VisualBrush> per creare la reflection di un oggetto <xref:System.Windows.Controls.Border> che contiene numerosi elementi.  Nella figura riportata di seguito viene illustrato l'output che si ottiene dall'esempio.  
  
 ![Oggetto Visual riflesso](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-visualbrush-reflection-small.png "graphicsmm\_visualbrush\_reflection\_small")  
Oggetto Visual riflesso  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 Per un esempio completo che include dimostrazioni relative all'ingrandimento di parti dello schermo e alla creazione di reflection, vedere [Esempio VisualBrush](http://go.microsoft.com/fwlink/?LinkID=160049) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.VisualBrush>   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)