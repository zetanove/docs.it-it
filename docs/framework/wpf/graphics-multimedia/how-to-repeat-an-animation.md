---
title: "Procedura: ripetere un&#39;animazione | Microsoft Docs"
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
  - "animazione, ripetizione"
  - "RepeatBehavior (proprietà delle sequenze temporali)"
  - "ripetizione dell'animazione"
  - "sequenze temporali (proprietà RepeatBehavior)"
ms.assetid: e6f3b068-eeeb-47fd-8d40-8848c31f1e1e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: ripetere un&#39;animazione
In questo esempio viene illustrato come utilizzare la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> per controllare il comportamento di ripetizione di un'animazione.  
  
## Esempio  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> controlla il numero di volte in cui la durata semplice di un'animazione viene ripetuta.  Utilizzando <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>, è possibile specificare che un oggetto <xref:System.Windows.Media.Animation.Timeline> deve essere ripetuto per un determinato numero di volte \(un conteggio di iterazioni\) o per un periodo di tempo specificato.  In entrambi i casi, l'animazione viene eseguita dall'inizio alla fine per il numero di volte necessario per soddisfare il conteggio o la durata richiesta.  
  
 Per impostazione predefinita, le sequenze temporali prevedono un conteggio di ripetizioni pari a 1,0, il che significa che vengono riprodotte una sola volta e non vengono ripetute.  Tuttavia, se si imposta la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> su <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>, la sequenza temporale viene ripetuta all'infinito.  
  
 Nell'esempio seguente viene illustrato come utilizzare la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> per controllare il comportamento di ripetizione di un'animazione.  Viene animata la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di cinque rettangoli, utilizzando per ognuno di essi un tipo diverso di comportamento di ripetizione.  
  
 [!code-xml[timingbehaviors_snip#RepeatBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/RepeatBehaviorExample.xaml#repeatbehaviorwholepage)]  
  
 Per l'esempio completo, vedere [Esempio di comportamento temporale di un'animazione](http://go.microsoft.com/fwlink/?LinkID=159970) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Accumulare valori di animazione durante i cicli ripetuti](../../../../docs/framework/wpf/graphics-multimedia/how-to-accumulate-animation-values-during-repeat-cycles.md)   
 [Specificare se una sequenza temporale viene invertita automaticamente](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-whether-a-timeline-automatically-reverses.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Esempio di comportamento temporale di un'animazione](http://go.microsoft.com/fwlink/?LinkID=159970)