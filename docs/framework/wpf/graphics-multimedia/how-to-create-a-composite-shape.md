---
title: "Procedura: creare una forma composta | Microsoft Docs"
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
  - "forme composte"
  - "grafica, forme composte"
  - "forme, composte"
ms.assetid: 8e5c7ef4-d7ed-4c43-afc9-ca01325c300b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare una forma composta
In questo esempio viene mostrato come creare forme composte utilizzando gli oggetti <xref:System.Windows.Media.Geometry> e come visualizzarle tramite un elemento <xref:System.Windows.Shapes.Path>.  Nell'esempio seguente, vengono utilizzati gli oggetti <xref:System.Windows.Media.LineGeometry>, <xref:System.Windows.Media.EllipseGeometry> e <xref:System.Windows.Media.RectangleGeometry> con <xref:System.Windows.Media.GeometryGroup> per creare una forma composta.  Le geometrie vengono quindi disegnate utilizzando un elemento <xref:System.Windows.Shapes.Path>.  
  
## Esempio  
 [!code-xml[GeometrySample#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#19)]  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/CompositeShapeExample.cs#compositeshapecodeexampleinline1)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/compositeshapeexample.vb#compositeshapecodeexampleinline1)]  
  
 Nella figura seguente viene mostrata la forma creata nell'esempio precedente.  
  
 ![Geometria composta creata con GeometryGroup](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-compositegeometryexample1.png "wcpsdk\_graphicsmm\_compositegeometryexample1")  
Geometria composta  
  
 Forme più complesse, ad esempio poligoni e forme con segmenti curvi, possono essere create utilizzando <xref:System.Windows.Media.PathGeometry>.  Per un esempio in cui viene mostrato come creare una forma utilizzando <xref:System.Windows.Media.PathGeometry>, vedere [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md).  Sebbene in questo esempio venga eseguito il rendering di una forma sullo schermo utilizzando un elemento <xref:System.Windows.Shapes.Path>, è anche possibile utilizzare gli oggetti <xref:System.Windows.Media.Geometry> per descrivere il contenuto di un oggetto <xref:System.Windows.Media.GeometryDrawing> o di un oggetto <xref:System.Windows.Media.DrawingContext>.  Tali oggetti possono essere utilizzati anche per ritagliare e per eseguire l'hit test.  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989) \(la pagina potrebbe essere in inglese\).