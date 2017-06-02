---
title: "Procedura: creare una curva di Bezier quadratica | Microsoft Docs"
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
  - "curve di Bézier, creazione"
  - "grafica [WPF], curve di Bezier quadratiche"
  - "curve di Bezier quadratiche, creazione"
ms.assetid: cd8fca4a-504e-4fd8-92ea-2969065a6e02
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare una curva di Bezier quadratica
In questo esempio viene illustrata la procedura per creare una curva di Bezier quadratica.  Per creare una curva di Bezier quadratica, utilizzare le classi <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure> e <xref:System.Windows.Media.QuadraticBezierSegment>.  
  
## Esempio  
 Negli esempi riportati di seguito viene disegnata una curva di Bézier quadratica da \(10, 100\) a \(300, 100\).  a curva presenta un punto di controllo con valore \(200, 200\).  
  
 \[xaml\]  
  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile utilizzare la sintassi di attributo per descrivere un percorso.  
  
 [!code-xml[GeometrySample#54](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#54)]  
  
 \[xaml\]  
  
 Si noti che la sintassi di attributo crea in effetti un oggetto <xref:System.Windows.Media.StreamGeometry>, una versione più semplice di un oggetto <xref:System.Windows.Media.PathGeometry>.  Per ulteriori informazioni, vedere la pagina [Sintassi di markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md).  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile disegnare una curva di Bezier quadratica anche utilizzando la sintassi per elementi oggetto.  L'esempio riportato di seguito equivale all'esempio di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 [!code-xml[GeometrySample#34](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 Questo esempio è stato estratto da un esempio più ampio; per la versione completa, vedere [Esempio di geometrie](http://go.microsoft.com/fwlink/?LinkID=159989) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Creare un arco ellittico](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-an-elliptical-arc.md)   
 [Creare una curva di Bezier cubica](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-cubic-bezier-curve.md)