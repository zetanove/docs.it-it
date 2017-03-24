---
title: 'Procedura: dichiarare eventi personalizzati per evitare il blocco (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- declaring events, custom
- events [Visual Basic], custom
- custom events
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
caps.latest.revision: 12
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 34b222bdbfdae0673b7150c220ca477b7e286dda
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-custom-events-to-avoid-blocking-visual-basic"></a>Procedura: dichiarare eventi personalizzati per evitare il blocco (Visual Basic)
Esistono diverse circostanze quando è importante che un gestore eventi non blocchi i gestori eventi successivi. Eventi personalizzati consentono di chiamare gestori eventi in modo asincrono l'evento.  
  
 Per impostazione predefinita, il campo archivio di backup per una dichiarazione di evento è un delegato multicast che combina in modo seriale tutti i gestori eventi. Ciò significa che se un gestore richiede molto tempo, si blocca altri gestori fino al completamento. (I gestori eventi che devono evitare di eseguire operazioni di lunga durate o di blocco.)  
  
 Invece di utilizzare l'implementazione predefinita di eventi disponibili in Visual Basic, è possibile utilizzare un evento personalizzato per eseguire i gestori eventi in modo asincrono.  
  
## <a name="example"></a>Esempio  
 In questo esempio, il `AddHandler` funzione di accesso aggiunge il delegato per ogni gestore del `Click` evento per un <xref:System.Collections.ArrayList>archiviati nel `EventHandlerList` campo.</xref:System.Collections.ArrayList>  
  
 Quando il codice genera il `Click` evento, il `RaiseEvent` funzione di accesso richiama tutti i delegati del gestore eventi in modo asincrono utilizzando il <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>(metodo).</xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> Questo metodo richiama ogni gestore su un thread di lavoro e restituisce immediatamente, in modo che i gestori non blocchino reciprocamente.  
  
 [!code-vb[VbVbalrEvents&#27;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-custom-events-to-avoid-blocking_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.ArrayList></xref:System.Collections.ArrayList>   
 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A></xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [Procedura: Dichiarare eventi personalizzati per proteggere la memoria](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)
