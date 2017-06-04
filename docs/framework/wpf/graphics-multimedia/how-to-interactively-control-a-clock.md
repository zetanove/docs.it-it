---
title: "Procedura: controllare in modo interattivo un oggetto Clock | Microsoft Docs"
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
  - "orologi, controllo in modo interattivo"
  - "controllo degli orologi in modo interattivo"
ms.assetid: d0b520e0-2f18-4cef-977f-2909e709548a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: controllare in modo interattivo un oggetto Clock
La proprietà <xref:System.Windows.Media.Animation.ClockController> di un oggetto <xref:System.Windows.Media.Animation.Clock> consente di avviare, sospendere, riprendere, cercare e arrestare l'oggetto clock, nonché di spostarlo alla fine del segmento di tempo.  Solo l'oggetto clock radice di una struttura ad albero delle temporizzazioni può essere controllato in modo interattivo.  
  
> [!NOTE]
>  Sono disponibili altre modalità per controllare in modo interattivo le animazioni che non richiedono l'utilizzo diretto di oggetti clock da parte dell'utente; ad esempio, è possibile utilizzare gli storyboard.  Gli storyboard sono supportati nel markup e nel codice.  Per un esempio, vedere [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md) oppure [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Nell'esempio seguente vengono utilizzati vari pulsanti per controllare in modo interattivo clock dell'animazione.  
  
## Esempio  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerExample.cs#graphicsmmclockcontrollerexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerexample.vb#graphicsmmclockcontrollerexample)]  
  
## Vedere anche  
 [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)