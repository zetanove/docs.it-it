---
title: "Procedura: definire una penna | Microsoft Docs"
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
  - "creazione, penne"
  - "penne, definizione"
ms.assetid: 7a4f2900-cdf9-49de-84e0-ba5d0ded4d33
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 2
---
# Procedura: definire una penna
In questo esempio viene mostrato come utilizzare un oggetto <xref:System.Windows.Media.Pen> per delineare una forma.  Per creare un oggetto <xref:System.Windows.Media.Pen>semplice è sufficiente specificarne le proprietà <xref:System.Windows.Media.Pen.Thickness%2A> e <xref:System.Windows.Media.Pen.Brush%2A>.  È possibile creare una penna più complessa specificando gli oggetti <xref:System.Windows.Media.Pen.DashStyle%2A>, <xref:System.Windows.Media.Pen.DashCap%2A>, <xref:System.Windows.Media.Pen.LineJoin%2A>, <xref:System.Windows.Media.Pen.StartLineCap%2A>e <xref:System.Windows.Media.Pen.EndLineCap%2A>.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Pen> per delineare una forma definita da un oggetto <xref:System.Windows.Media.GeometryDrawing>.  
  
 [!code-csharp[PenExamples_snip#PenExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PenExamples_snip/CSharp/PenExample.cs#penexamplewholepage)]
 [!code-vb[PenExamples_snip#PenExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PenExamples_snip/VisualBasic/PenExample.vb#penexamplewholepage)]  
  
 ![Strutture prodotte da un oggetto Pen](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple-pen.png "graphicsmm\_simple\_pen")  
Un oggetto GeometryDrawing