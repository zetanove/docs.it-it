---
title: "Procedura: cercare uno storyboard in modo sincrono | Microsoft Docs"
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
  - "ricerca degli storyboard in modalità sincrona"
  - "Storyboard, ricerca in modalità sincrona"
ms.assetid: 03e06271-a946-4810-88ea-3fb4cfa9e0f1
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: cercare uno storyboard in modo sincrono
Nell'esempio riportato di seguito viene illustrato come utilizzare il metodo <xref:System.Windows.Media.Animation.Storyboard.SeekAlignedToLastTick%2A> di <xref:System.Windows.Media.Animation.Storyboard> per cercare in modo sincrono qualsiasi posizione dell'animazione di uno storyboard.  
  
## Esempio  
 Di seguito viene riportato il markup XAML per l'esempio.  
  
 [!code-xml[SeekStoryboard_snip#SeekStoryboardSynchronouslyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SeekStoryboard_snip/CSharp/SeekStoryboardSynchronouslyExample.xaml#seekstoryboardsynchronouslyexamplewholepage)]  
  
## Esempio  
 Di seguito viene fornito il codice utilizzato con il codice XAML riportato sopra.  
  
 [!code-csharp[SeekStoryboard_snip#SeekStoryboardSynchronouslyCodeBehindExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SeekStoryboard_snip/CSharp/SeekStoryboardSynchronouslyExample.xaml.cs#seekstoryboardsynchronouslycodebehindexamplewholepage)]
 [!code-vb[SeekStoryboard_snip#SeekStoryboardSynchronouslyCodeBehindExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SeekStoryboard_snip/VisualBasic/SeekStoryboardSynchronouslyExample.xaml.vb#seekstoryboardsynchronouslycodebehindexamplewholepage)]