---
title: "Procedura: creare un disegno composto | Microsoft Docs"
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
  - "classi, DrawingGroup"
  - "disegni composti"
  - "DrawingGroup (classe)"
  - "disegni, composte"
  - "grafica, disegni composti"
ms.assetid: 066eb0ab-5f0e-439d-85c6-dca60af269fc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare un disegno composto
In questo esempio viene illustrato come utilizzare <xref:System.Windows.Media.DrawingGroup> per creare disegni complessi combinando più oggetti <xref:System.Windows.Media.Drawing> in un solo disegno composto.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.DrawingGroup> per creare un disegno composto dagli oggetti <xref:System.Windows.Media.GeometryDrawing> e <xref:System.Windows.Media.ImageDrawing>.  Nella figura riportata di seguito viene illustrato l'output che si ottiene dall'esempio.  
  
 ![DrawingGroup con più disegni](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple.png "graphicsmm\_simple")  
Disegno composto creato utilizzando DrawingGroup  
  
 Si noti il bordo grigio che indica i limiti del disegno.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 È possibile utilizzare <xref:System.Windows.Media.DrawingGroup> per applicare <xref:System.Windows.Media.DrawingGroup.Transform%2A>, un'impostazione di <xref:System.Windows.Media.DrawingGroup.Opacity%2A>, <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>, <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>, <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A> o <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A> ai disegni che contiene.  Poiché <xref:System.Windows.Media.DrawingGroup> è anche <xref:System.Windows.Media.Drawing>, può contenere altri oggetti <xref:System.Windows.Media.DrawingGroup>.  
  
 L'esempio riportato di seguito è simile a quello precedente, tranne per il fatto che vengono utilizzati altri oggetti <xref:System.Windows.Media.DrawingGroup> per applicare effetti bitmap e una maschera di opacità ad alcuni dei disegni.  Nella figura riportata di seguito viene illustrato l'output che si ottiene dall'esempio.  
  
 ![DrawingGroup con più disegni](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-multiple.png "graphicsmm\_multiple")  
Disegno composto con più oggetti DrawingGroup  
  
 Si noti il bordo grigio che indica i limiti del disegno.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmmultipledrawinggroupsexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMMultipleDrawingGroupsExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmmultipledrawinggroupsexample)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Drawing>, vedere [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>   
 <xref:System.Windows.Media.DrawingGroup.Transform%2A>   
 <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>   
 <xref:System.Windows.Media.DrawingGroup.Opacity%2A>   
 <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>   
 <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)