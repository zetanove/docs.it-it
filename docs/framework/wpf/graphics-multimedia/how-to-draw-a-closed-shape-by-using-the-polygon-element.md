---
title: "Procedura: disegnare una forma chiusa utilizzando l&#39;elemento poligono | Microsoft Docs"
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
  - "forme chiuse, disegno con elementi poligono"
  - "disegno, forme chiuse con elementi poligono"
  - "grafica, poligono (elementi)"
  - "poligono (elementi)"
ms.assetid: 4b0ca008-29ce-48dd-8bc3-f3a20ffca6a6
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: disegnare una forma chiusa utilizzando l&#39;elemento poligono
In questo esempio viene illustrato come disegnare una forma chiusa utilizzando l'elemento <xref:System.Windows.Shapes.Polygon>.  Per disegnare una forma chiusa, creare un elemento <xref:System.Windows.Shapes.Polygon> e utilizzare la relativa proprietà <xref:System.Windows.Shapes.Polygon.Points%2A> per specificare i vertici della forma.  Viene tracciata automaticamente una riga che collega il primo e l'ultimo punto.  Infine, specificare una proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>, una proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> o entrambe.  
  
## Esempio  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], la sintassi valida per i punti è un elenco delimitato da spazi di coppie di coordinate x e y separate da virgole.  
  
 [!code-xml[drawingwithshapeelements#PolygonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polygonexample.xaml#polygonexample1)]  
  
 Anche se nell'esempio viene utilizzato un oggetto <xref:System.Windows.Controls.Canvas> per contenere i poligoni, è possibile utilizzare elementi poligono, e tutti gli altri elementi forma, con qualsiasi oggetto <xref:System.Windows.Controls.Panel> o <xref:System.Windows.Controls.Control> che supporti contenuto non testuale.  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di elementi forma](http://go.microsoft.com/fwlink/?LinkID=160037) \(la pagina potrebbe essere in inglese\).