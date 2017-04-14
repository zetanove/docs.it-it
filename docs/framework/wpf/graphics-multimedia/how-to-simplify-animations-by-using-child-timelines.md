---
title: "Procedura: semplificare le animazioni utilizzando oggetti Timeline figlio | Microsoft Docs"
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
  - "animazione, semplificazione per sequenze temporali figlie"
  - "sequenze temporali figlie"
  - "semplificazione delle animazioni per sequenze temporali figlie"
ms.assetid: 8335d770-d13d-42bd-8dfa-63f92c0327e2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: semplificare le animazioni utilizzando oggetti Timeline figlio
In questo esempio viene illustrato come semplificare le animazioni utilizzando oggetti <xref:System.Windows.Media.Animation.ParallelTimeline> figlio.  <xref:System.Windows.Media.Animation.Storyboard> è un tipo di oggetto <xref:System.Windows.Media.Animation.Timeline> che fornisce informazioni sulla destinazione per gli oggetti Timeline che contiene.  Utilizzare un oggetto <xref:System.Windows.Media.Animation.Storyboard> per fornire informazioni sulla destinazione degli oggetti Timeline, tra cui informazioni su oggetti e proprietà.  
  
 Per iniziare un'animazione, utilizzare uno o più oggetti <xref:System.Windows.Media.Animation.ParallelTimeline> come elementi figlio annidati di un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  Questi oggetti <xref:System.Windows.Media.Animation.ParallelTimeline> possono contenere altre animazioni e pertanto possono incapsulare in modo più efficace le sequenze temporali nelle animazioni complesse.  Ad esempio, se si applica l'animazione a un oggetto <xref:System.Windows.Controls.TextBlock> e a diverse forme nello stesso oggetto <xref:System.Windows.Media.Animation.Storyboard>, è possibile separare le animazioni per l'oggetto <xref:System.Windows.Controls.TextBlock> e per le forme, inserendole ognuna in un oggetto <xref:System.Windows.Media.Animation.ParallelTimeline> distinto.  Poiché ogni oggetto <xref:System.Windows.Media.Animation.ParallelTimeline> include una proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> e tutti gli elementi figlio dell'oggetto <xref:System.Windows.Media.Animation.ParallelTimeline> iniziano in base a questa proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A>, le sequenze temporali risultano incapsulate in modo migliore.  
  
 Nell'esempio seguente vengono animate due parti di testo \(oggetti<xref:System.Windows.Controls.TextBlock>\) dall'interno dello stesso oggetto <xref:System.Windows.Media.Animation.Storyboard>.  Un oggetto <xref:System.Windows.Media.Animation.ParallelTimeline> incapsula le animazioni di uno degli oggetti <xref:System.Windows.Controls.TextBlock>.  
  
 **Nota sulle prestazioni:** anche se è possibile annidare gli oggetti Timeline <xref:System.Windows.Media.Animation.Storyboard> uno nell'altro, gli oggetti <xref:System.Windows.Media.Animation.ParallelTimeline> sono più adatti per l'annidamento perché l'overhead richiesto è minore.  La classe <xref:System.Windows.Media.Animation.Storyboard> eredita dalla classe <xref:System.Windows.Media.Animation.ParallelTimeline>.  
  
## Esempio  
 [!code-xml[Timelines_snip#ParallelTimelineWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Timelines_snip/CS/ParallelTimelineExample.xaml#paralleltimelinewholepage)]  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Specificare HandoffBehavior tra le animazioni storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-handoffbehavior-between-storyboard-animations.md)