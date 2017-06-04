---
title: "Procedura: creare forme tramite un oggetto StreamGeometry | Microsoft Docs"
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
  - "classi, StreamGeometry"
  - "grafica [WPF], forme"
  - "forme, creazione con la classe StreamGeometry"
  - "StreamGeometry (classe)"
ms.assetid: 08f7c8ce-074b-49cd-9aba-cc9592d4ee51
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare forme tramite un oggetto StreamGeometry
<xref:System.Windows.Media.StreamGeometry> è un'alternativa più semplice a <xref:System.Windows.Media.PathGeometry> per la creazione di forme geometriche.  Utilizzare <xref:System.Windows.Media.StreamGeometry> per descrivere una geometria complessa senza il sovraccarico dovuto al supporto dell'associazione dati, dell'animazione o della modifica.  Grazie alla sua efficienza, la classe <xref:System.Windows.Media.StreamGeometry> rappresenta una scelta ottimale per la descrizione degli strumenti decorativi visuali.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzata la sintassi dell'attributo per creare un oggetto <xref:System.Windows.Media.StreamGeometry> triangolare in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 Per ulteriori informazioni sulla sintassi dell'attributo dell'oggetto <xref:System.Windows.Media.StreamGeometry>, vedere la pagina [Sintassi di markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.StreamGeometry> per definire un triangolo nel codice.  Viene innanzitutto creato un oggetto <xref:System.Windows.Media.StreamGeometry>, dopodiché si ottiene un oggetto <xref:System.Windows.Media.StreamGeometryContext> che viene utilizzato per descrivere il triangolo.  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryTriangleExample.cs#streamgeometrytriangleexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometrytriangleexample.vb#streamgeometrytriangleexamplewholepage)]  
  
## Esempio  
 Nell'esempio seguente viene creato un metodo che utilizza gli oggetti <xref:System.Windows.Media.StreamGeometry> e <xref:System.Windows.Media.StreamGeometryContext> per definire una forma geometrica in base a parametri specifici.  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryExample.cs#streamgeometryexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometryexample.vb#streamgeometryexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Media.StreamGeometry>   
 <xref:System.Windows.Media.StreamGeometryContext>   
 [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md)   
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)