---
title: "How to: Declare Custom Events To Avoid Blocking (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declaring events, custom"
  - "events [Visual Basic], custom"
  - "custom events"
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Declare Custom Events To Avoid Blocking (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esistono diverse circostanze nelle quali è importante che un gestore eventi non blocchi i gestori eventi successivi.  Gli eventi personalizzati consentono all'evento di chiamare i suoi gestori eventi in modo asincrono.  
  
 Per impostazione predefinita il campo dell'archivio di backup di una dichiarazione di evento è un delegato multicast in cui tutti i gestori eventi vengono combinati in modo seriale.  In altre parole se il completamento di un gestore richiede una notevole quantità di tempo, gli altri gestori verranno bloccati fino al termine del completamento.  I gestori eventi ben progettati non dovrebbero mai eseguire operazioni lunghe o potenzialmente bloccanti.  
  
 Anziché utilizzare l'implementazione predefinita degli eventi forniti da Visual Basic, è possibile utilizzare un evento personalizzato per l'esecuzione asincrona dei gestori eventi.  
  
## Esempio  
 In questo esempio, la funzione di accesso `AddHandler` consente di aggiungere il delegato di ogni gestore dell'evento `Click` a un <xref:System.Collections.ArrayList> memorizzato nel campo `EventHandlerList`.  
  
 Al momento della generazione dell'evento `Click` da parte del codice, alla funzione di accesso `RaiseEvent` è consentito richiamare tutti i delegati del gestore eventi in maniera asincrona tramite il metodo <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>.  Con tale metodo è possibile richiamare ogni gestore su un thread di lavoro e di restituirlo immediatamente, in modo tale che i gestori non possano bloccarsi tra loro.  
  
 [!code-vb[VbVbalrEvents#27](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#27)]  
  
## Vedere anche  
 <xref:System.Collections.ArrayList>   
 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>   
 [Events](../../../../visual-basic/programming-guide/language-features/events/events.md)   
 [How to: Declare Custom Events To Conserve Memory](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)