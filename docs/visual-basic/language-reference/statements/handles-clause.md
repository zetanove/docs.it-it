---
title: "Handles Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Handles"
  - "vb.Handles"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Handles keyword"
ms.assetid: 1b051c0e-f499-42f6-acb5-6f4f27824b40
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Handles Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Dichiara che una routine gestisce un evento specificato.  
  
## Sintassi  
  
```  
  
proceduredeclaration Handles eventlist  
```  
  
## Parti  
 `proceduredeclaration`  
 Dichiarazione `Sub` per la routine che gestirà l'evento.  
  
 `eventlist`  
 Elenco degli eventi che devono essere gestiti da `proceduredeclaration`.  Gli eventi devono essere generati dalla classe base per la classe corrente o da un oggetto dichiarato usando la parola chiave `WithEvents`.  
  
## Note  
 Usare la parola chiave `Handles` alla fine di una dichiarazione di routine per fare in modo che la routine gestisca eventi generati da una variabile oggetto dichiarata con la parola chiave `WithEvents`.  La parola chiave `Handles` può anche essere usata in una classe derivata per gestire eventi da una classe base.  
  
 La parola chiave `Handles` e l'istruzione `AddHandler` consentono entrambe di specificare che quelle particolari routine gestiscono particolari eventi, ma esistono alcune differenze.  Usare la parola chiave `Handles` quando si definisce una routine, per specificare che questa gestisce un particolare evento.  L'istruzione `AddHandler` connette le routine agli eventi in fase di esecuzione.  Per altre informazioni, vedere [AddHandler Statement](../../../visual-basic/language-reference/statements/addhandler-statement.md).  
  
 Per gli eventi personalizzati, l'applicazione richiama la funzione di accesso `AddHandler` dell'evento quando aggiunge la routine come gestore eventi.  Per altre informazioni sugli eventi personalizzati, vedere [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## Esempio  
 [!code-vb[VbVbalrEvents#2](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#2)]  
  
 L'esempio seguente illustra come una classe derivata può usare l'istruzione `Handles` per gestire un evento da una classe base.  
  
 [!code-vb[VbVbalrEvents#3](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/Class1.vb#3)]  
  
## Esempio  
 L'esempio seguente contiene due gestori eventi dei pulsanti per un progetto **Applicazione WPF**.  
  
 [!code-vb[VbVbalrEvents#41](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/class3.vb#41)]  
  
## Esempio  
 L'esempio che segue equivale a quello precedente.  L'oggetto `eventlist` nella clausola `Handles` contiene gli eventi per entrambi i pulsanti.  
  
 [!code-vb[VbVbalrEvents#42](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/VbVbalrEvents/class3.vb#42)]  
  
## Vedere anche  
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)   
 [AddHandler Statement](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler Statement](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [RaiseEvent Statement](../../../visual-basic/language-reference/statements/raiseevent-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)