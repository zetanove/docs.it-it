---
title: "AddHandler Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AddHandlerMethod"
  - "addhandler"
  - "vb.addhandler"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AddHandler statement"
ms.assetid: cfe69799-2a0f-42c0-a99e-09fed954da01
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# AddHandler Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di associare un evento a un gestore eventi in fase di esecuzione.  
  
## Sintassi  
  
```  
AddHandler event, AddressOf eventhandler  
```  
  
## Parti  
 `event`  
 Il nome dell'evento da gestire.  
  
 `eventhandler`  
 Il nome della routine che gestisce l'evento.  
  
## Note  
 Le istruzioni `AddHandler` e `RemoveHandler` consentono di avviare e interrompere la gestione degli eventi in qualunque momento durante l'esecuzione del programma.  
  
 La firma della routine `eventhandler` deve corrispondere a quella dell'evento `event`.  
  
 Sia la parola chiave `Handles` sia l'istruzione `AddHandler` consentono di specificare quali particolari routine devono gestire determinati eventi, ma con alcune differenze.  L'istruzione `AddHandler` consente la connessione di routine ed eventi in fase di esecuzione.  Durante la definizione di una routine, utilizzare la parola chiave `Handles` per specificare l'evento particolare da gestire.  Per ulteriori informazioni, vedere [Handles](../../../visual-basic/language-reference/statements/handles-clause.md).  
  
> [!NOTE]
>  Per eventi personalizzati, l'istruzione `AddHandler` consente di richiamare la funzione di accesso `AddHandler` dell'evento.  Per ulteriori informazioni sugli eventi personalizzate, vedere [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## Esempio  
 [!code-vb[VbVbalrEvents#17](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#17)]  
  
## Vedere anche  
 [RemoveHandler Statement](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)