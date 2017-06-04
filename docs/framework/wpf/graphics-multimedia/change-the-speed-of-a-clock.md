---
title: "Procedura: modificare la velocit&#224; di un orologio senza cambiare la velocit&#224; della relativa sequenza temporale | Microsoft Docs"
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
  - "orologi, modifica della velocità"
  - "velocità dell'orologio, modifica"
ms.assetid: 72f36dd0-f085-445d-8589-19a83fe74f5e
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: modificare la velocit&#224; di un orologio senza cambiare la velocit&#224; della relativa sequenza temporale
La proprietà <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> di un oggetto <xref:System.Windows.Media.Animation.ClockController> consente di modificare la velocità di un oggetto <xref:System.Windows.Media.Animation.Clock> senza alterare la proprietà <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> dell'oggetto <xref:System.Windows.Media.Animation.Timeline> dell'orologio.  Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.ClockController> per modificare in modo interattivo <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> di un orologio.  L'evento <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeedInvalidated> e la proprietà <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeed%2A> dell'orologio sono utilizzati per visualizzare la velocità globale corrente dell'orologio tutte le volte che l'oggetto <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> interattivo viene modificato.  
  
## Esempio  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerSpeedRatioExample.cs#graphicsmmclockcontrollerspeedratioexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerspeedratioexample.vb#graphicsmmclockcontrollerspeedratioexample)]