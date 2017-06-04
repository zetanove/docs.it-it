---
title: "Procedura: disegnare un&#39;ellisse o un cerchio | Microsoft Docs"
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
  - "cerchi, disegno"
  - "disegno di cerchi"
  - "disegno di ellissi"
  - "ellissi, disegno"
  - "grafica, disegno di cerchi"
  - "grafica, disegno di ellissi"
ms.assetid: 99763b8c-bfc8-44be-8231-8a70daf5481a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: disegnare un&#39;ellisse o un cerchio
In questo esempio viene illustrato come disegnare ellissi e cerchi utilizzando l'elemento <xref:System.Windows.Shapes.Ellipse>.  Per disegnare un'ellisse, creare un elemento <xref:System.Windows.Shapes.Ellipse> e specificare le relative proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>.  Utilizzare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> per specificare l'oggetto <xref:System.Windows.Media.Brush> utilizzato per disegnare l'interno dell'ellisse.  Utilizzare la proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> per specificare l'oggetto <xref:System.Windows.Media.Brush> utilizzato per disegnare il contorno dell'ellisse.  La proprietà <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> specifica lo spessore del contorno dell'ellisse.  
  
 Per disegnare un cerchio, impostare le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> dell'elemento <xref:System.Windows.Shapes.Ellipse> sullo stesso valore.  
  
 Nell'esempio seguente vengono disegnati quattro elementi <xref:System.Windows.Shapes.Ellipse> all'interno di un oggetto <xref:System.Windows.Controls.Canvas>.  
  
## Esempio  
 [!code-xml[drawingwithshapeelements#EllipseExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/ellipseexample.xaml#ellipseexample1)]  
  
 Anche se in questo esempio viene utilizzato un oggetto <xref:System.Windows.Controls.Canvas> per contenere l'ellisse, è possibile utilizzare gli elementi ellisse e tutti gli altri elementi forma con qualsiasi oggetto <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.Control> che supporta contenuto non testuale.  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Ellipse>   
 <xref:System.Windows.Shapes.Shape>   
 [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037)