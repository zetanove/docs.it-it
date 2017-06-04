---
title: "Procedura: controllare un&#39;animazione mediante i valori From, To e By | Microsoft Docs"
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
  - "animazione, a/da"
  - "animazione di base"
  - "animazione, l'animazione di base"
  - "From/To/By (animazione)"
ms.assetid: 59afba57-6fc1-44c8-987e-8a5f4142adad
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: controllare un&#39;animazione mediante i valori From, To e By
Un "From/To/By" o "base" viene creata una transizione tra due valori di destinazione (vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) per un'introduzione ai diversi tipi di animazioni). Per impostare i valori di destinazione un'animazione di base, utilizzare il <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> proprietà.  Nella tabella seguente sono riepilogati come <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> proprietà possono essere utilizzate insieme o separatamente i valori per determinare di destinazione di un'animazione.  
  
|Proprietà specificate|Comportamento risultante|  
|--------------------------|------------------------|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>|L'animazione avanza dal valore specificato per il <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> proprietà al valore di base della proprietà viene aggiunta un'animazione o un'animazione precedente valore, a seconda della configurazione di un'animazione precedente di output.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> and                              <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|L'animazione avanza dal valore specificato per il <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> proprietà sul valore specificato per il <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> proprietà.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> and                              <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|L'animazione avanza dal valore specificato per il <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> proprietà sul valore specificato per la somma del <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> proprietà.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>|L'animazione avanza dal valore di base della proprietà animate o un'animazione precedente il valore specificato dal valore di output di <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> proprietà.|  
|<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>|L'animazione avanza dal valore di base della proprietà viene aggiunta un'animazione o un'animazione precedente valore di output per la somma di tale valore e il valore specificato per il <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> proprietà.|  
  
> [!NOTE]
>  Non impostare contemporaneamente il <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> proprietà e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> proprietà sulla stessa animazione.  
  
 Per utilizzare altri metodi di interpolazione o aggiungere un'animazione tra più di due valori di destinazione, utilizzare un'animazione con fotogrammi chiave. Vedere [Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md) per ulteriori informazioni.  
  
 Per informazioni sull'applicazione di più animazioni a una singola proprietà, vedere [Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
 L'esempio seguente illustra i diversi effetti dell'impostazione <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>, e <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> proprietà animazioni.  
  
## <a name="example"></a>Esempio  
 [!code-xml[BasicAnimations_snippet#AnimationTargetValuesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snippet/CS/AnimationTargetValuesExample.xaml#animationtargetvalueswholepage)]  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [FROM, To e dall'esempio valori di destinazione dell'animazione](http://go.microsoft.com/fwlink/?LinkID=159988)