---
title: 'Procedura: dichiarare eventi personalizzati per risparmiare memoria (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
caps.latest.revision: 11
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
ms.openlocfilehash: 4f8ce32a3b4da411a73010119283ce9661b82a6c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-custom-events-to-conserve-memory-visual-basic"></a>Procedura: dichiarare eventi personalizzati per proteggere la memoria (Visual Basic)
Esistono diverse circostanze quando è importante che un'applicazione mantenere l'utilizzo della memoria insufficiente. Gli eventi personalizzati consentono all'applicazione di utilizzare memoria solo per gli eventi che gestisce.  
  
 Per impostazione predefinita, quando una classe dichiara un evento, il compilatore alloca memoria per un campo archiviare le informazioni sull'evento. Se una classe dispone di molti eventi inutilizzati, essi consumano inutilmente memoria.  
  
 Anziché utilizzare l'implementazione predefinita di eventi disponibili in Visual Basic, è possibile utilizzare gli eventi personalizzati per gestire più attentamente l'utilizzo della memoria.  
  
## <a name="example"></a>Esempio  
 In questo esempio, la classe utilizza un'istanza di <xref:System.ComponentModel.EventHandlerList>(classe), archiviati nel `Events` campo, per archiviare le informazioni sugli eventi in uso.</xref:System.ComponentModel.EventHandlerList> Il <xref:System.ComponentModel.EventHandlerList>è una classe elenco ottimizzata progettata per contenere delegati.</xref:System.ComponentModel.EventHandlerList>  
  
 Tutti gli eventi della classe utilizzano il `Events` campo per tenere traccia di quali metodi stanno gestendo ciascun evento.  
  
 [!code-vb[VbVbalrEvents&#22;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-custom-events-to-conserve-memory_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ComponentModel.EventHandlerList></xref:System.ComponentModel.EventHandlerList>   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [Procedura: Dichiarare eventi personalizzati per evitare il blocco](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)
