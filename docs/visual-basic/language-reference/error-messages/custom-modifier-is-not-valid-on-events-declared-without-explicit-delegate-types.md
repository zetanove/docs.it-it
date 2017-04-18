---
title: "Modificatore &quot;Custom&quot; non è valido negli eventi dichiarati senza tipi delegati espliciti | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31122
- bc31122
dev_langs:
- VB
helpviewer_keywords:
- BC31122
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 0e70fca6a0608df5db43156f70196b4e5c9b2339
ms.lasthandoff: 03/13/2017

---
# <a name="39custom39-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types"></a>Modificatore 'Custom' non è valido negli eventi dichiarati senza tipi delegati espliciti
A differenza di un evento non personalizzato, un `Custom Event` dichiarazione richiede un `As` clausola dopo il nome di evento che specifica in modo esplicito il tipo di delegato per l'evento.  
  
 Gli eventi non personalizzati possono essere definiti con un `As` clausola ed esplicita tipo delegato o con un parametro elenco immediatamente dopo il nome dell'evento.  
  
 **ID errore:** BC31122  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Definire un delegato con lo stesso elenco di parametri dell'evento personalizzato.  
  
     Ad esempio, se il `Custom Event` è stato definito da `Custom Event Test(ByVal sender As Object, ByVal i As Integer)`, quindi il delegato corrispondente sarebbe il seguente.  
  
     [!code-vb[VbVbalrEventError&#18;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types_1.vb)]  
  
2.  Sostituire l'elenco di parametri dell'evento personalizzato con un `As` clausola che specifica il tipo delegato.  
  
     Continuando con l'esempio, `Custom Event` dichiarazione potrebbe essere riscritto come segue.  
  
     [!code-vb[&#19; VbVbalrEventError](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types_2.vb)]  
  
## <a name="example"></a>Esempio  
 In questo esempio dichiara un `Custom Event` e specifica le `As` clausola con un tipo delegato.  
  
 [!code-vb[VbVbalrEventError n.&2;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types_3.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Event](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate (istruzione)](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Eventi](../../../visual-basic/programming-guide/language-features/events/index.md)
