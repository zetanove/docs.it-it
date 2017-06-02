---
title: "Procedura: attivare un&#39;animazione quando il valore di una propriet&#224; viene modificato | Microsoft Docs"
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
  - "animazione, avvio al variare dei valori di una proprietà"
  - "Storyboard, avvio al variare dei valori di una proprietà"
  - "generazione di animazione"
ms.assetid: 12399c21-0300-4f4f-9e3a-d92d9907e5f5
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: attivare un&#39;animazione quando il valore di una propriet&#224; viene modificato
In questo esempio viene illustrato come utilizzare un <xref:System.Windows.Trigger> per avviare uno <xref:System.Windows.Media.Animation.Storyboard> quando viene modificato il valore di una proprietà.  È possibile utilizzare <xref:System.Windows.Trigger> all'interno di <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate> o <xref:System.Windows.DataTemplate>.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato <xref:System.Windows.Trigger> per animare <xref:System.Windows.UIElement.Opacity%2A> di <xref:System.Windows.Controls.Button> quando la relativa proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> diventa `true`.  
  
 [!code-xml[AnimatePropertyStoryboards#PropertyTriggerExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/PropertyTriggerExample.xaml#propertytriggerexample)]  
  
 Le animazioni applicate tramite oggetti <xref:System.Windows.Trigger> di proprietà dimostrano un comportamento più complesso rispetto alle animazioni <xref:System.Windows.EventTrigger> o a quelle avviate tramite i metodi <xref:System.Windows.Media.Animation.Storyboard>.  Vengono fornite con animazioni definite da altri oggetti <xref:System.Windows.Trigger>, ma possono essere combinate con animazioni <xref:System.Windows.EventTrigger> e con animazioni attivate tramite metodi.  
  
## Vedere anche  
 <xref:System.Windows.Trigger>   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)