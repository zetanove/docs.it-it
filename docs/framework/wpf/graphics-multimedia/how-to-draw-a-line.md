---
title: "Procedura: disegnare una linea | Microsoft Docs"
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
  - "disegno, linee"
  - "grafica [WPF], linee"
  - "linee, disegno"
ms.assetid: 0513ee01-6b27-4bb3-85f3-3a3e6710d80e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: disegnare una linea
In questo esempio viene illustrato come disegnare righe utilizzando l'elemento <xref:System.Windows.Shapes.Line>.  
  
 Per disegnare una riga, creare un elemento <xref:System.Windows.Shapes.Line>.  Utilizzare le proprietà <xref:System.Windows.Shapes.Line.X1%2A> e <xref:System.Windows.Shapes.Line.Y1%2A> per impostare il punto di inizio e utilizzare le proprietà <xref:System.Windows.Shapes.Line.X2%2A> e <xref:System.Windows.Shapes.Line.Y2%2A> per impostare il punto di fine.  Impostare infine <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> per rendere invisibile una riga senza tratto.  
  
 L'impostazione dell'elemento <xref:System.Windows.Shapes.Shape.Fill%2A> per una riga non ha effetto, perché una riga non ha interno.  
  
 Nell'esempio riportato di seguito vengono tracciate tre righe all'interno di un elemento <xref:System.Windows.Controls.Canvas>.  
  
## Esempio  
 [!code-xml[drawingwithshapeelements#LineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Line>   
 [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037)