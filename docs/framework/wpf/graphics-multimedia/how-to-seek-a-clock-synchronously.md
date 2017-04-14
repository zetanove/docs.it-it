---
title: "Procedura: cercare un orologio in modalit&#224; sincrona | Microsoft Docs"
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
  - "orologi, ricerca in modalità sincrona"
  - "ricerca di orologi in modalità sincrona"
ms.assetid: e5b7529b-b7d0-40d2-9e1d-fa4b5e736e96
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: cercare un orologio in modalit&#224; sincrona
Utilizzare il metodo <xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> per la ricerca sincrona di un orologio per un punto specifico.  Nell'esempio seguente vengono illustrati i metodi <xref:System.Windows.Media.Animation.ClockController.Seek%2A> e <xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A> di un oggetto <xref:System.Windows.Media.Animation.ClockController>.  
  
 In questo esempio viene mostrato come cercare un oggetto <xref:System.Windows.Media.Animation.Clock>; per un esempio in cui viene illustrato come cercare un storyboard, vedere [Cercare uno storyboard in modalità sincrona](../../../../docs/framework/wpf/graphics-multimedia/how-to-seek-a-storyboard-synchronously.md).  
  
## Esempio  
 [!code-csharp[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClockController_procedural_snip/CSharp/SeekAlignedToLastTickExample.cs#clockcontrollerseekexample)]
 [!code-vb[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClockController_procedural_snip/visualbasic/seekalignedtolasttickexample.vb#clockcontrollerseekexample)]