---
title: "Procedura: creare un arco ellittico | Microsoft Docs"
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
  - "archi, ellittici"
  - "archi ellittici, creazione"
  - "grafica [WPF], archi ellittici"
ms.assetid: 3dcfe502-3485-45de-99fb-d53a1367c484
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare un arco ellittico
In questo esempio viene illustrato come disegnare un arco ellittico.  Per creare un arco ellittico, utilizzare le classi <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure> e <xref:System.Windows.Media.ArcSegment>.  
  
## Esempio  
 Negli esempi riportati di seguito viene disegnato un arco ellittico da \(10,100\) a \(200,100\).  L'arco ha una proprietà <xref:System.Windows.Media.ArcSegment.Size%2A> di 100 per 50 pixel indipendenti dal dispositivo, una proprietà <xref:System.Windows.Media.ArcSegment.RotationAngle%2A> di 45 gradi, la proprietà <xref:System.Windows.Media.ArcSegment.IsLargeArc%2A> impostata su `true` e una <xref:System.Windows.Media.ArcSegment.SweepDirection%2A> impostata su <xref:System.Windows.Media.SweepDirection>.  
  
 \[xaml\]  
  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile utilizzare la sintassi di attributo per descrivere un percorso.  
  
 [!code-xml[GeometrySample#56](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#56)]  
  
 \[xaml\]  
  
 Si noti che la sintassi di attributo crea in effetti un oggetto <xref:System.Windows.Media.StreamGeometry>, una versione più semplice di un oggetto <xref:System.Windows.Media.PathGeometry>.  Per ulteriori informazioni, vedere la pagina [Sintassi di markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md).  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è anche possibile disegnare un arco ellittico utilizzando in modo esplicito tag Object.  Gli elementi seguenti sono equivalenti al markup [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 [!code-xml[GeometrySample#36](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#36)]  
  
 Questo esempio fa parte di un esempio più esaustivo.  Per l'esempio completo, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Creare una curva di Bezier quadratica.](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-quadratic-bezier-curve.md)   
 [Creare una curva di Bezier cubica](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)