---
title: "Procedura: specificare HandoffBehavior tra le animazioni storyboard | Microsoft Docs"
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
  - "animazione, HandoffBehavior (valore)"
  - "Storyboard, HandoffBehavior (valore tra le animazioni)"
ms.assetid: 97bd6842-929b-49d9-813e-46553ae46472
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: specificare HandoffBehavior tra le animazioni storyboard
In questo esempio viene illustrato come specificare il valore HandoffBehavior tra le animazioni storyboard.  La proprietà <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> di <xref:System.Windows.Media.Animation.BeginStoryboard> specifica la modalità di interazione tra le nuove animazioni e quelle esistenti già applicate a una proprietà.  
  
## Esempio  
 Nell'esempio seguente vengono creati due pulsanti le cui dimensioni aumentano o diminuiscano a seconda che il cursore del mouse venga spostato su di essi o rimosso.  Se il cursore viene spostato su un pulsante e quindi rapidamente rimosso, la seconda animazione verrà applicata prima del completamento della prima.  In casi come questo in cui due animazioni si sovrappongono è possibile rilevare la differenza tra i valori <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> di <xref:System.Windows.Media.Animation.HandoffBehavior> e <xref:System.Windows.Media.Animation.HandoffBehavior>.  Un valore di <xref:System.Windows.Media.Animation.HandoffBehavior> combina le animazioni sovrapposte generando una transizione più fluida tra le animazioni, mentre un valore di <xref:System.Windows.Media.Animation.HandoffBehavior> causa l'immediata sostituzione della precedente animazione sovrapposta con quella nuova.  
  
 [!code-xml[timingbehaviors_snip#HandoffBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/HandoffBehaviorExample.xaml#handoffbehaviorwholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.BeginStoryboard>   
 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)