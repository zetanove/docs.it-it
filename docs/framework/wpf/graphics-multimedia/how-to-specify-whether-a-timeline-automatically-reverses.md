---
title: "Procedura: specificare se una sequenza temporale viene automaticamente invertita o meno | Microsoft Docs"
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
  - "AutoReverse (proprietà delle sequenze temporali)"
  - "sequenze temporali, AutoReverse (proprietà)"
ms.assetid: 1648dd90-1bee-409a-ac69-ac729867f557
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: specificare se una sequenza temporale viene automaticamente invertita o meno
La proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> di una sequenza temporale determina se tale sequenza viene riprodotta in senso inverso dopo il completamento di un'iterazione diretta.  Nell'esempio riportato di seguito vengono illustrate diverse animazioni con durata e valori di destinazione identici, ma con impostazioni <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> diverse.  Per dimostrare il comportamento della proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> con impostazioni <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> diverse, viene impostata la ripetizione di alcune animazioni.  Nell'ultima animazione viene illustrato il funzionamento della proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> su sequenze temporale annidate.  
  
## Esempio  
 [!code-xml[timingbehaviors_snip#AutoReverseAndRepeatBehaviorExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AutoReverseExample.xaml#autoreverseandrepeatbehaviorexamplewholepage)]