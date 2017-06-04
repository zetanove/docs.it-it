---
title: "Procedura: ricevere una notifica quando uno stato dell&#39;orologio viene modificato | Microsoft Docs"
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
  - "orologi, notifiche di modifiche dello stato"
  - "notifiche, modifiche dello stato degli orologi"
ms.assetid: ecb10fc9-d0c2-45c3-b0a1-7b11baa733da
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: ricevere una notifica quando uno stato dell&#39;orologio viene modificato
L'evento <xref:System.Windows.Media.Animation.Clock.CurrentStateInvalidated> di un orologio si verifica quando il relativo oggetto <xref:System.Windows.Media.Animation.Clock.CurrentState%2A> diventa non valido, ad esempio quando l'orologio viene avviato o interrotto.  È possibile eseguire la registrazione per questo evento utilizzando direttamente un oggetto <xref:System.Windows.Media.Animation.Clock> oppure è possibile eseguire la registrazione tramite un oggetto <xref:System.Windows.Media.Animation.Timeline>.  
  
 Nell'esempio seguente, un oggetto <xref:System.Windows.Media.Animation.Storyboard> e due oggetti <xref:System.Windows.Media.Animation.DoubleAnimation> vengono utilizzati per aggiungere un'animazione alla larghezza di due rettangoli.  L'evento <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> viene utilizzato per essere in ascolto dei cambiamenti di stato dell'orologio.  
  
## Esempio  
 [!code-xml[timingbehaviors_snip#_graphicsmm_StateExampleMarkupWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml#_graphicsmm_stateexamplemarkupwholepage)]  
  
 [!code-csharp[timingbehaviors_snip#_graphicsmm_StateEventHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/StateExample.xaml.cs#_graphicsmm_stateeventhandlers)]
 [!code-vb[timingbehaviors_snip#_graphicsmm_StateEventHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/stateexample.xaml.vb#_graphicsmm_stateeventhandlers)]  
  
 Nell'immagine seguente vengono mostrati i diversi stati attraversati dalle animazioni man mano che la sequenza temporale padre \(*Storyboard*\) avanza.  
  
 ![Stati di clock per uno storyboard con due animazioni](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-3timelines.png "graphicsmm\_3timelines")  
  
 Nella tabella seguente vengono mostrati i momenti in cui l'evento <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> dell'*Animazione1* viene generato:  
  
||||||||  
|-|-|-|-|-|-|-|  
|Tempo \(secondi\)|1|10|19|21|30|39|  
|Stato|Active|Active|Stopped|Active|Active|Stopped|  
  
 Nella tabella seguente vengono mostrati i momenti in cui l'evento <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> dell'*Animazione2* viene generato:  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
|Tempo \(secondi\)|1|9|11|19|21|29|31|39|  
|Stato|Active|Riempimento|Active|Stopped|Active|Riempimento|Active|Stopped|  
  
 Tenere presente che l'evento <xref:System.Windows.Media.Animation.Timeline.CurrentStateInvalidated> dell'*Animazione1* viene generato a 10 secondi, anche se il relativo stato rimane <xref:System.Windows.Media.Animation.ClockState>.  Questa situazione si verifica perché lo stato è cambiato a 10 secondi, ma è stato modificato da <xref:System.Windows.Media.Animation.ClockState> a <xref:System.Windows.Media.Animation.ClockState> e quindi nuovamente riportato a <xref:System.Windows.Media.Animation.ClockState> nello stesso ciclo.