---
title: "Procedura: modificare la terminazione alla fine di una linea o di un segmento | Microsoft Docs"
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
  - "grafica, estremità di forma"
  - "elementi forma, estremità"
  - "elementi forma, estremità"
ms.assetid: f4bf3416-b3d8-4568-b98e-3eda8f6dbf7a
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: modificare la terminazione alla fine di una linea o di un segmento
In questo esempio viene illustrato come modificare la forma all'inizio o alla fine di un elemento <xref:System.Windows.Shapes.Shape> aperto.  Per modificare la terminazione all'inizio di un elemento <xref:System.Windows.Shapes.Shape> aperto, utilizzare la proprietà <xref:System.Windows.Shapes.Shape.StrokeStartLineCap%2A>.  Per modificare la terminazione alla fine di un elemento <xref:System.Windows.Shapes.Shape> aperto, utilizzare la proprietà <xref:System.Windows.Shapes.Shape.StrokeEndLineCap%2A>.  Per visualizzare le terminazioni di linea disponibili, vedere l'enumerazione <xref:System.Windows.Media.PenLineCap>.  
  
> [!NOTE]
>  Questa proprietà influisce solo su una forma aperta, ad esempio un elemento <xref:System.Windows.Shapes.Line>, un elemento <xref:System.Windows.Shapes.Polyline> o un elemento <xref:System.Windows.Shapes.Path> aperto.  
  
 Nell'esempio seguente vengono tracciati quattro elementi <xref:System.Windows.Shapes.Polyline> e viene utilizzato un insieme diverso di forme sulle estremità di ognuno.  
  
## Esempio  
 [!code-xml[drawingwithshapeelements#ShapeLineCaps1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/linecapsandjoinsexample.xaml#shapelinecaps1)]  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Shapes.Polyline>   
 <xref:System.Windows.Media.PenLineCap>