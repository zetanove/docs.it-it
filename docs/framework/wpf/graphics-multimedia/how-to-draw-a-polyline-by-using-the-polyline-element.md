---
title: "Procedura: disegnare una polilinea utilizzando l&#39;elemento polilinea | Microsoft Docs"
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
  - "linee collegate"
  - "disegno, polilinee"
  - "grafica [WPF], polilinee"
  - "linee, collegate (vedere polilinee)"
  - "polilinee, disegno"
ms.assetid: 65db8935-d047-4295-87c4-b427ff3ad293
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: disegnare una polilinea utilizzando l&#39;elemento polilinea
In questo esempio viene illustrato come disegnare una polilinea, ovvero una serie di righe collegate, utilizzando l'elemento <xref:System.Windows.Shapes.Polyline>.  
  
 Per disegnare una polilinea, creare un elemento <xref:System.Windows.Shapes.Polyline> e utilizzare la relativa proprietà <xref:System.Windows.Shapes.Polyline.Points%2A> per specificare i vertici della forma.  Infine, utilizzare le proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> per descrivere i contorni della polilinea perché una linea senza un tratto è invisibile.  
  
> [!NOTE]
>  Poiché l'elemento <xref:System.Windows.Shapes.Polyline> non è una forma chiusa, la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> non produce effetti, anche se si chiudono intenzionalmente i contorni della forma.  Per creare una forma chiusa con una proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>, utilizzare un elemento <xref:System.Windows.Shapes.Polygon>.  
  
 Nell'esempio riportato di seguito vengono disegnati due elementi <xref:System.Windows.Shapes.Polyline> all'interno di un oggetto <xref:System.Windows.Controls.Canvas>.  
  
## Esempio  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], la sintassi valida per i punti è un elenco delimitato da spazi di coppie di coordinate x e y separate da virgole.  
  
 [!code-xml[drawingwithshapeelements#PolylineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polylineexample.xaml#polylineexample1)]  
  
 Anche se in questo esempio viene utilizzato un oggetto <xref:System.Windows.Controls.Canvas> per contenere le polilinee, è possibile utilizzare elementi polilinea, e tutti gli altri elementi forma, con qualsiasi oggetto <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.Control> che supporta contenuto non testuale.  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Polyline>   
 <xref:System.Windows.Shapes.Polygon>   
 <xref:System.Windows.Shapes.Shape>   
 [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)