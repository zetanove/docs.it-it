---
title: "Procedura: eseguire un hit test della geometria in un oggetto Visual | Microsoft Docs"
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
  - "Geometry (oggetti), oggetti Visual che includono"
  - "hit test, sugli oggetti Visual che includono gli oggetti Geometry"
  - "oggetti Visual, hit test"
ms.assetid: 8bf2643f-d7f9-4cb4-9ea6-5b893c23200d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: eseguire un hit test della geometria in un oggetto Visual
In questo esempio viene mostrato come eseguire un [hit test](GTMT) in un oggetto Visual composto da uno o più oggetti <xref:System.Windows.Media.Geometry>.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come recuperare l'oggetto <xref:System.Windows.Media.DrawingGroup> da un oggetto Visual che utilizza il metodo <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A>.  Viene quindi eseguito un hit test sul contenuto di rendering di ciascun disegno nell'oggetto <xref:System.Windows.Media.DrawingGroup> per determinare la geometria raggiunta.  
  
> [!NOTE]
>  Nella maggior parte dei casi è preferibile utilizzare il metodo <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> per determinare se un punto interseca un contenuto di un oggetto Visual di cui si è eseguito il rendering.  
  
 [!code-csharp[VisualsOverview#VisualsOverviewSnippet4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#visualsoverviewsnippet4)]
 [!code-vb[VisualsOverview#VisualsOverviewSnippet4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#visualsoverviewsnippet4)]  
  
 Il metodo <xref:System.Windows.Media.Geometry.FillContains%2A> è un metodo di overload che consente di eseguire l'hit test utilizzando un oggetto <xref:System.Windows.Point> o <xref:System.Windows.Media.Geometry> specificato.  Se viene tracciata una geometria, il tratto può estendersi oltre i limiti del riempimento.  In tal caso, è necessario chiamare <xref:System.Windows.Media.Geometry.StrokeContains%2A> oltre a <xref:System.Windows.Media.Geometry.FillContains%2A>.  
  
 Inoltre, è possibile fornire un oggetto <xref:System.Windows.Media.ToleranceType> utilizzato per la linearizzazione di Bezier.  
  
> [!NOTE]
>  In questo esempio non vengono presi in considerazione tutte le trasformazioni o i ritagli che possono essere applicati alla geometria.  Inoltre, questo esempio non è valido per un controllo a cui sono stati applicati degli stili, poiché non dispone di disegni associati direttamente.  
  
## Vedere anche  
 [Hit testing a livello visivo](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)   
 [Eseguire un hit test utilizzando la geometria come parametro](../../../../docs/framework/wpf/graphics-multimedia/how-to-hit-test-using-geometry-as-a-parameter.md)