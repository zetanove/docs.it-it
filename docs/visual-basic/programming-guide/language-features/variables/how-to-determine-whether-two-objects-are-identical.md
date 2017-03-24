---
title: 'Procedura: determinare se due oggetti sono identici (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- testing, objects
- objects [Visual Basic], comparing
- object variables, determining identity
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
caps.latest.revision: 19
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
ms.openlocfilehash: 3a853d9f958829eeb0fb42ecbcdae7ba912c89ed
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-determine-whether-two-objects-are-identical-visual-basic"></a>Procedura: determinare se due oggetti sono identici (Visual Basic)
In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], due riferimenti a variabili vengono considerati identici se i relativi puntatori sono uguali, vale a dire se entrambe le variabili puntano alla stessa istanza di classe nella memoria. Ad esempio, in un'applicazione Windows Form, è per un confronto per determinare se l'istanza corrente (`Me`) è uguale a un'istanza specifica, ad esempio `Form2`.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]sono disponibili due operatori per confrontare i puntatori. Il [operatore Is](../../../../visual-basic/language-reference/operators/is-operator.md) restituisce `True` se gli oggetti sono identici e [IsNot (operatore)](../../../../visual-basic/language-reference/operators/isnot-operator.md) restituisce `True` se non lo sono.  
  
## <a name="determining-if-two-objects-are-identical"></a>Determinare se due oggetti sono identici  
  
#### <a name="to-determine-if-two-objects-are-identical"></a>Per determinare se due oggetti sono identici  
  
1.  Impostare un `Boolean` espressione da testare i due oggetti.  
  
2.  Un'espressione di test, utilizzare il `Is` operatore con i due oggetti come operandi.  
  
     `Is`Restituisce `True` se gli oggetti puntano alla stessa istanza di classe.  
  
## <a name="determining-if-two-objects-are-not-identical"></a>Determinare se due oggetti non sono identici  
 A volte si desidera eseguire un'azione se i due oggetti non sono identici, ma può essere difficile combinare `Not` e `Is`, ad esempio `If Not obj1 Is obj2`. In questo caso è possibile utilizzare il `IsNot` operatore.  
  
#### <a name="to-determine-if-two-objects-are-not-identical"></a>Per determinare se due oggetti non sono identici  
  
1.  Impostare un `Boolean` espressione da testare i due oggetti.  
  
2.  Un'espressione di test, utilizzare il `IsNot` operatore con i due oggetti come operandi.  
  
     `IsNot`Restituisce `True` se gli oggetti non puntano alla stessa istanza di classe.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente verifica coppie di `Object` variabili per stabilire se puntano alla stessa istanza di classe.  
  
 [!code-vb[VbVbalrKeywords&#14;](../../../../visual-basic/language-reference/codesnippet/VisualBasic/how-to-determine-whether-two-objects-are-identical_1.vb)]  
  
 Nell'esempio precedente viene visualizzato l'output seguente.  
  
 `objA different from objB? True`  
  
 `objA identical to objC? True`  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Valori di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Is (operatore)](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot (operatore)](../../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Procedura: determinare se due oggetti sono correlati](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [Me, My, MyBase e MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
