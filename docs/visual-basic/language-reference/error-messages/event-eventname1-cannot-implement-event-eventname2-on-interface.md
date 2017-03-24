---
title: "Evento &quot;&lt;eventname1&gt;&quot;non può implementare l&quot;evento&quot;&lt;eventname2&gt;&quot;nell&quot;interfaccia&quot;&lt;interfaccia&gt;&quot; perché i tipi di delegati&lt;delegate1&gt;&quot;e&quot;&lt;delegate2&gt;&quot; non corrispondono a | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31423
- bc31423
dev_langs:
- VB
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
caps.latest.revision: 6
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
ms.openlocfilehash: b6253b3e9ad07c3715c55a8cfd0891792b45a452
ms.lasthandoff: 03/13/2017

---
# <a name="event-39lteventname1gt39-cannot-implement-event-39lteventname2gt39-on-interface-39ltinterfacegt39-because-their-delegate-types-39ltdelegate1gt39-and-39ltdelegate2gt39-do-not-match"></a>Evento '&lt;eventname1&gt;'non può implementare l'evento'&lt;eventname2&gt;'nell'interfaccia'&lt;interfaccia&gt;' perché i tipi di delegati&lt;delegate1&gt;'e'&lt;delegate2&gt;' non corrispondono
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Impossibile implementare un evento perché il tipo di delegato dell'evento non corrisponde al tipo di delegato dell'evento nell'interfaccia. Questo errore può insorgere quando si definiscono più eventi in un'interfaccia e si prova a implementarli assieme con lo stesso evento. Un evento può implementare due o più eventi solo se tutti gli eventi implementati vengono dichiarati usando la sintassi `As` e se tutti specificano lo stesso tipo delegato.  
  
 **ID errore:** BC31423  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Implementare gli eventi separatamente.  
  
     -oppure-  
  
-   Definire gli eventi nell'interfaccia utilizzando il `As` sintassi e specificare lo stesso tipo di delegato.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate (istruzione)](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
