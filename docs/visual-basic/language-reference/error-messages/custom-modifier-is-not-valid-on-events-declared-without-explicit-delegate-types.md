---
title: "&#39;Custom&#39; modifier is not valid on events declared without explicit delegate types | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31122"
  - "bc31122"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31122"
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &#39;Custom&#39; modifier is not valid on events declared without explicit delegate types
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

A differenza di evento non personalizzato, una dichiarazione `Custom Event` richiede la presenza di una clausola `As` dopo il nome dell'evento che specifichi in modo esplicito il tipo di delegato per l'evento.  
  
 Gli eventi non personalizzati possono essere definiti con una clausola `As` e un tipo delegato esplicito oppure con un elenco di parametri immediatamente successivo al nome dell'evento.  
  
 **ID errore:** BC31122  
  
### Per correggere l'errore  
  
1.  Definire un delegato con lo stesso elenco di parametri dell'evento personalizzato.  
  
     Ad esempio, se l'evento `Custom Event` è stato definito da `Custom Event Test(ByVal sender As Object, ByVal i As Integer)`, il delegato corrispondente sarebbe il seguente:  
  
     [!code-vb[VbVbalrEventError#18](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/custom-modifier-is-not-v_1.vb)]  
  
2.  Sostituire l'elenco di parametri dell'evento personalizzato con una clausola `As` che specifica il tipo di delegato.  
  
     Continuando con l'esempio, la dichiarazione `Custom Event` verrebbe riscritta nel modo seguente.  
  
     [!code-vb[VbVbalrEventError#19](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/custom-modifier-is-not-v_2.vb)]  
  
## Esempio  
 Questo esempio dichiara un `Custom Event` e specifica la clausola `As` richiesta con un tipo delegato.  
  
 [!code-vb[VbVbalrEventError#2](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/custom-modifier-is-not-v_3.vb)]  
  
## Vedere anche  
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)