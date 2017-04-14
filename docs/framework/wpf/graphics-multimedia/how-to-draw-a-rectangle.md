---
title: "Procedura: disegnare un rettangolo | Microsoft Docs"
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
  - "disegno, rettangoli"
  - "grafica [WPF], rettangoli"
  - "rettangoli, disegno"
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: disegnare un rettangolo
In questo esempio viene illustrato come disegnare un rettangolo utilizzando l'elemento <xref:System.Windows.Shapes.Rectangle>.  
  
 Per disegnare un rettangolo, creare un elemento <xref:System.Windows.Shapes.Rectangle> e specificare le relative proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>.  Per disegnare l'interno del rettangolo, impostare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>.  Per specificare un contorno per il rettangolo, utilizzare le proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>.  
  
 Per impostare angoli arrotondati per il rettangolo, specificare le proprietà facoltative <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> e <xref:System.Windows.Shapes.Rectangle.RadiusY%2A>.  Le proprietà <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> e <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> impostano i raggi sull'asse x e sull'asse y dell'ellisse utilizzata per arrotondare gli angoli del rettangolo.  
  
 Nell'esempio seguente vengono disegnati due elementi <xref:System.Windows.Shapes.Rectangle> in un oggetto <xref:System.Windows.Controls.Canvas>.  Il primo rettangolo ha un colore interno <xref:System.Windows.Media.Brushes.Blue%2A>.  Il secondo rettangolo ha un colore interno <xref:System.Windows.Media.Brushes.Blue%2A>, un contorno <xref:System.Windows.Media.Brushes.Black%2A> e gli angoli arrotondati.  
  
## Esempio  
 [!code-xml[drawingwithshapeelements#Rectangle1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 Anche se in questo esempio viene utilizzato un oggetto <xref:System.Windows.Controls.Canvas> per contenere i rettangoli, è possibile utilizzare elementi rettangolo, e tutti gli altri elementi forma, con qualsiasi oggetto <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.Control> che supporta contenuto non testuale.  Infatti, i rettangoli sono particolarmente utili per fornire sfondi per parti dei riquadri <xref:System.Windows.Controls.Grid>.  Per un esempio, vedere [Cenni preliminari sull'elemento Table](../../../../docs/framework/wpf/advanced/table-overview.md).  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Rectangle>   
 [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Cenni preliminari sull'elemento Table](../../../../docs/framework/wpf/advanced/table-overview.md)