---
title: "Procedura: specificare la propriet&#224; FillBehavior di un oggetto Timeline che ha raggiunto la fine del periodo di attivit&#224; | Microsoft Docs"
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
  - "FillBehavior (proprietà per sequenze temporali inattive)"
  - "sequenze temporali, FillBehavior (proprietà)"
ms.assetid: db805f59-d513-4dac-af15-47005dae3199
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: specificare la propriet&#224; FillBehavior di un oggetto Timeline che ha raggiunto la fine del periodo di attivit&#224;
In questo esempio viene illustrato come specificare la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> per l'oggetto <xref:System.Windows.Media.Animation.Timeline> inattivo di una proprietà animata.  
  
## Esempio  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> determina ciò che si verifica per il valore di una proprietà animata quando non viene animata, ossia quando l'oggetto <xref:System.Windows.Media.Animation.Timeline> è inattivo ma il relativo oggetto <xref:System.Windows.Media.Animation.Timeline> padre è nel periodo di attività o di attesa,  ad esempio se al termine di un'animazione il valore di una proprietà animata rimane impostato sul valore finale o se viene ripristinato il valore esistente prima dell'inizio dell'animazione.  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> per animare la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di due rettangoli.  Ogni rettangolo utilizza un oggetto <xref:System.Windows.Media.Animation.Timeline> diverso.  
  
 Un oggetto <xref:System.Windows.Media.Animation.Timeline> include una proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> impostata su <xref:System.Windows.Media.Animation.FillBehavior>. In questo caso al termine dell'oggetto <xref:System.Windows.Media.Animation.Timeline>, viene ripristinato il valore della larghezza del rettangolo esistente prima dell'animazione.  L'altro oggetto <xref:System.Windows.Media.Animation.Timeline> include una proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> impostata su <xref:System.Windows.Media.Animation.FillBehavior>. In questo caso al termine dell'oggetto <xref:System.Windows.Media.Animation.Timeline>, la larghezza rimane impostata sul valore finale.  
  
 [!code-xml[timingbehaviors_snip#FillBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/FillBehaviorExample.xaml#fillbehaviorwholepage)]  
  
 Per l'esempio completo, vedere [Raccolta di esempi di animazioni](http://go.microsoft.com/fwlink/?LinkID=159969) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.DoubleAnimation>   
 <xref:System.Windows.FrameworkElement.Width%2A>   
 <xref:System.Windows.Media.Animation.Timeline>   
 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>   
 <xref:System.Windows.Media.Animation.FillBehavior>   
 <xref:System.Windows.Media.Animation.FillBehavior>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)