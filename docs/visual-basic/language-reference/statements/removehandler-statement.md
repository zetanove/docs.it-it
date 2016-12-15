---
title: "RemoveHandler Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.RemoveHandlerMethod"
  - "vb.RemoveHandler"
  - "RemoveHandler"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "RemoveHandler keyword"
  - "RemoveHandler statement"
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# RemoveHandler Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di rimuovere l'associazione tra un evento e un gestore eventi.  
  
## Sintassi  
  
```  
RemoveHandler event, AddressOf eventhandler  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`event`|Il nome dell'evento gestito.|  
|`eventhandler`|Il nome della routine che gestisce l'evento.|  
  
## Note  
 Le istruzioni `AddHandler` e `RemoveHandler` consentono di avviare e interrompere la gestione degli eventi per un evento specifico in qualunque momento durante l'esecuzione del programma.  
  
> [!NOTE]
>  Per gli eventi personalizzati, l'istruzione `RemoveHandler` richiama la funzione di accesso `RemoveHandler` dell'evento.  Per ulteriori informazioni sugli eventi personalizzate, vedere [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## Esempio  
 [!code-vb[VbVbalrEvents#17](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/removehandler-statement_1.vb)]  
  
## Vedere anche  
 [AddHandler Statement](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)