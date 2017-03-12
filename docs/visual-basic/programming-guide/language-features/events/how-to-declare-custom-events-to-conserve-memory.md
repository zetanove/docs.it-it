---
title: "How to: Declare Custom Events To Conserve Memory (Visual Basic) | Microsoft Docs"
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
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Declare Custom Events To Conserve Memory (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In molte circostanze è importante che l'utilizzo della memoria da parte di un'applicazione sia mantenuto a livelli ridotti.  Gli eventi personalizzati consentono all'applicazione di utilizzare la memoria soltanto per gli eventi che gestisce.  
  
 Per impostazione predefinita, quando una classe dichiara un evento, il compilatore assegna della memoria a un campo per l'archiviazione delle informazioni sull'evento.  Se una classe comprende molti eventi inutilizzati, essi consumano inutilmente memoria.  
  
 Anziché utilizzare l'implementazione predefinita degli eventi fornita da Visual Basic, quindi, è possibile utilizzare gli eventi personalizzati per gestire in modo più oculato l'utilizzo della memoria.  
  
## Esempio  
 In questo esempio, la classe utilizza un'istanza della classe <xref:System.ComponentModel.EventHandlerList>, archiviata nel campo `Events`, per memorizzare informazioni sugli eventi in uso.  La classe <xref:System.ComponentModel.EventHandlerList> è una classe elenco ottimizzata progettata per contenere delegati.  
  
 Tutti gli eventi della classe utilizzano il campo `Events` per tenere traccia di quali metodi stanno gestendo ciascun evento.  
  
 [!code-vb[VbVbalrEvents#22](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#22)]  
  
## Vedere anche  
 <xref:System.ComponentModel.EventHandlerList>   
 [Events](../../../../visual-basic/programming-guide/language-features/events/events.md)   
 [How to: Declare Custom Events To Avoid Blocking](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)