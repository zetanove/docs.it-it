---
title: "Troubleshooting Inherited Event Handlers in Visual Basic | Microsoft Docs"
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
  - "troubleshooting events"
  - "inherited events"
  - "troubleshooting Visual Basic, event handlers"
  - "event handling, troubleshooting"
  - "event handlers, troubleshooting"
ms.assetid: e1c8759f-5370-4308-8476-8c48b73509bf
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Troubleshooting Inherited Event Handlers in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo argomento sono elencati i problemi comuni correlati all'uso di gestori eventi in componenti ereditati.  
  
## Procedure  
  
#### Codice del gestore eventi eseguito due volte per ogni chiamata  
  
-   Un gestore eventi ereditato non deve includere una clausola [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md).  Il metodo nella classe base è già associato all'evento e verrà generato di conseguenza.  Rimuovere la clausola `Handles` dal metodo ereditato.  
  
     [!code-vb[VbVbalrEvents#32](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/troubleshooting-inherited-event-handlers_1.vb)]  
  
-   Se il metodo ereditato non contiene una parola chiave `Handles`, verificare che il codice non contenga un'istruzione[AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md) aggiuntiva o un qualsiasi altro metodo che gestisce lo stesso evento.  
  
## Vedere anche  
 [Events](../../../../visual-basic/programming-guide/language-features/events/events.md)