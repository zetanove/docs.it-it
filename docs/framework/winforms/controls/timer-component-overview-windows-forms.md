---
title: "Cenni preliminari sul componente Timer (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Timer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Timer (componente) [Windows Form], informazioni"
  - "timer, informazioni sui timer"
ms.assetid: e672c05b-a8b6-4b26-9e4d-9223aa9e3873
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul componente Timer (Windows Form)
Il componente <xref:System.Windows.Forms.Timer> di Windows Form genera un evento a intervalli regolari.  Il componente è progettato per l'ambiente Windows Form.  Per informazioni su un timer adatto a un ambiente server, vedere [Introduction to Server\-Based Timers](http://msdn.microsoft.com/it-it/adc0bc0a-a519-4812-bafc-fb9d1a5801fc).  
  
## Proprietà, metodi ed eventi principali  
 La lunghezza degli intervalli è definita dalla proprietà <xref:System.Windows.Forms.Timer.Interval%2A> il cui valore è espresso in millisecondi.  Quando il componente è attivato, viene generato un evento <xref:System.Windows.Forms.Timer.Tick> a ogni intervallo.  Questo rappresenta il punto in cui va aggiunto il codice da eseguire.  Per ulteriori informazioni, vedere [Procedura: eseguire routine a intervalli predefiniti con il componente Timer Windows Form](../../../../docs/framework/winforms/controls/run-procedures-at-set-intervals-with-wf-timer-component.md).  I metodi principali del componente <xref:System.Windows.Forms.Timer> sono <xref:System.Windows.Forms.Timer.Start%2A> e <xref:System.Windows.Forms.Timer.Stop%2A>, che attivano e disattivano il timer.  La disattivazione di un timer ne causa il riavvio in quanto non è possibile mettere in pausa un componente <xref:System.Windows.Forms.Timer>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Timer>   
 [Componente Timer](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)   
 [Limitazioni della proprietà Interval del componente Timer di Windows Form](../../../../docs/framework/winforms/controls/limitations-of-the-timer-component-interval-property.md)