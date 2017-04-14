---
title: "Limitazioni della propriet&#224; Interval del componente Timer di Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Interval (proprietà), limiti"
  - "Timer (componente) [Windows Form], limiti della proprietà Interval"
  - "timer, intervalli evento"
  - "timer, basato su Windows"
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Limitazioni della propriet&#224; Interval del componente Timer di Windows Form
Il componente <xref:System.Windows.Forms.Timer> di Windows Form dispone di una proprietà <xref:System.Windows.Forms.Timer.Interval%2A> tramite cui è possibile specificare il numero di millisecondi che intercorre tra un evento timer e quello successivo.  Se il componente non viene disabilitato, un timer continuerà a ricevere l'evento <xref:System.Windows.Forms.Timer.Tick> a intervalli di tempo più o meno uguali.  
  
 Il componente è progettato per l'ambiente Windows Form.  Per informazioni su un timer adatto a un ambiente server, vedere [Introduction to Server\-Based Timers](http://msdn.microsoft.com/it-it/adc0bc0a-a519-4812-bafc-fb9d1a5801fc).  
  
## Proprietà Interval  
 La proprietà <xref:System.Windows.Forms.Timer.Interval%2A> è associata ad alcune limitazioni che è necessario considerare quando si programma un componente <xref:System.Windows.Forms.Timer>.  
  
-   Se una delle applicazioni in esecuzione utilizza una notevole quantità di risorse del sistema, ad esempio mediante cicli lunghi, calcoli complessi o accessi alle unità, alla rete o alle porte, l'applicazione potrebbe non ricevere gli eventi timer con la frequenza specificata dalla proprietà <xref:System.Windows.Forms.Timer.Interval%2A>.  
  
-   L'esattezza dell'intervallo non è garantita.  Per ottenere la massima precisione possibile, sarà necessario controllare l'orologio di sistema in base alle specifiche esigenze, anziché tentare di tenere traccia del tempo accumulato internamente.  
  
-   La precisione della proprietà <xref:System.Windows.Forms.Timer.Interval%2A> è espressa in millisecondi.  Alcuni computer forniscono un contatore ad alta risoluzione con una risoluzione più elevata rispetto a quella espressa in millisecondi.  La disponibilità di tale contatore dipende dall'hardware del processore del computer.  Per ulteriori informazioni, vedere l'articolo 172338, "Come utilizzare QueryPerformanceCounter per il codice orario", in Microsoft Knowledge Base all'indirizzo http:\/\/support.microsoft.com\/?ln\=IT.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Timer>   
 [Componente Timer](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)   
 [Cenni preliminari sul componente Timer](../../../../docs/framework/winforms/controls/timer-component-overview-windows-forms.md)