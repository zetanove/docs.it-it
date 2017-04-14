---
title: "Procedura: impostare una durata per un&#39;animazione | Microsoft Docs"
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
  - "animazione, durata"
  - "durata delle animazioni"
  - "sequenze temporali, description"
ms.assetid: 155034ef-7d00-4416-a73c-b1713992d2eb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: impostare una durata per un&#39;animazione
<xref:System.Windows.Media.Animation.Timeline> rappresenta un intervallo di tempo la cui durata è determinata dall'oggetto <xref:System.Windows.Duration> della sequenza temporale.  Quando <xref:System.Windows.Media.Animation.Timeline> raggiunge la fine della propria durata, la riproduzione viene interrotta.  Se <xref:System.Windows.Media.Animation.Timeline> ha sequenze temporali figlio, anche la relativa riproduzione viene interrotta.  Nel caso di un'animazione, <xref:System.Windows.Duration> specifica il tempo impiegato dall'animazione per la transizione dal valore iniziale a quello finale.  
  
 È possibile specificare un oggetto <xref:System.Windows.Duration> con un tempo specifico finito o il valore speciale <xref:System.Windows.Duration.Automatic%2A> o <xref:System.Windows.Duration.Forever%2A>.  La durata di un'animazione deve essere sempre un valore temporale, poiché un'animazione deve sempre disporre di una durata definita e finita, in caso contrario l'animazione non sarebbe in grado di stabilire come effettuare la transizione tra i valori di destinazione.  Le sequenze temporali contenitore \(oggetti <xref:System.Windows.Media.Animation.TimelineGroup>\), ad esempio <xref:System.Windows.Media.Animation.Storyboard> e <xref:System.Windows.Media.Animation.ParallelTimeline>, hanno una durata predefinita di <xref:System.Windows.Duration.Automatic%2A>, che implica che tali sequenze temporali terminano automaticamente quando viene interrotta la riproduzione dell'ultima sequenza figlio.  
  
 Nell'esempio riportato di seguito, vengono animati la larghezza, l'altezza e colore di riempimento di <xref:System.Windows.Shapes.Rectangle>.  Le durate sono impostate su sequenze temporali di animazione e contenitore i cui effetti di animazione risultanti includono il controllo della velocità percepita di un'animazione e l'override della durata delle sequenze temporali figlio con la durata di una sequenza temporale contenitore.  
  
## Esempio  
 [!code-xml[timingbehaviors_snip#DurationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/DurationExample.xaml#durationexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Duration>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)