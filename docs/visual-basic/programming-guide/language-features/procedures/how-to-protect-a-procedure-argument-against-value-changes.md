---
title: 'Procedura: proteggere un argomento di routine modifica del valore (Visual Basic) | Documenti di Microsoft'
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
- procedures, arguments
- procedures, parameters
- procedure arguments
- arguments [Visual Basic], passing by reference
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures, calling
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: d2b7c766-ce16-4d2c-8d79-3fc0e7ba2227
caps.latest.revision: 14
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
ms.openlocfilehash: 6e18f7ceefeec9c1f422d0eae4e727700ebd8b6e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-protect-a-procedure-argument-against-value-changes-visual-basic"></a>Procedura: impedire la modifica del valore di un argomento di una routine (Visual Basic)
Se una routine dichiara un parametro come [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce il codice della routine un riferimento diretto all'elemento di programmazione sottostante all'argomento nel codice chiamante. In questo modo la procedura per modificare il valore sottostante all'argomento nel codice chiamante. In alcuni casi potrebbe essere necessario il codice chiamante per proteggersi da tali modifiche.  
  
 È possibile proteggere sempre un argomento da modifica dichiarando il parametro corrispondente [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) nella procedura. Se si desidera essere in grado di modificare un determinato argomento in alcuni casi, ma non altri, è possibile dichiarare `ByRef` e consentire al codice chiamante di determinare il meccanismo di passaggio in ogni chiamata. Questo avviene racchiudere l'argomento corrispondente tra parentesi per passarlo come valore, viene racchiuso o meno tra parentesi essere passato per riferimento. Per ulteriori informazioni, vedere [procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente illustra due procedure che accettano una variabile di matrice e operano sui relativi elementi. Il `increase` procedura aggiunge semplicemente uno a ogni elemento. Il `replace` procedura assegna una nuova matrice al parametro `a()` , quindi aggiunge uno a ogni elemento. Tuttavia, la riassegnazione non influiscono sulla variabile di matrice sottostante il codice chiamante.  
  
 [!code-vb[VbVbcnProcedures&#35;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_1.vb)]  
  
 [!code-vb[VbVbcnProcedures&#38;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_2.vb)]  
  
 [!code-vb[VbVbcnProcedures&#37;](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_3.vb)]  
  
 Il primo `MsgBox` chiamata viene visualizzato "dopo Increase (n): 11, 21, 31, 41". Poiché la matrice `n` è un tipo di riferimento, `replace` possibile modificare i relativi membri, anche se è il meccanismo di passaggio `ByVal`.  
  
 Il secondo `MsgBox` chiamata viene visualizzato "dopo Replace (n): 11, 21, 31, 41". Poiché `n` viene passato `ByVal`, `replace` non può modificare la variabile `n` nel codice chiamante assegnandole una nuova matrice. Quando `replace` crea una nuova istanza di matrice `k` e lo assegna alla variabile locale `a`, perde il riferimento a `n` passato al codice chiamante. Quando si trasforma i membri di `a`, solo la matrice locale `k` è interessato. Di conseguenza, `replace` incrementa i valori della matrice `n` nel codice chiamante.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Il valore predefinito in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore. Tuttavia, è buona norma includere una programmazione di [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) (parola chiave) con ogni parametro dichiarato. In questo modo il codice più facile da leggere.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Differenze tra argomenti modificabili e](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differenze tra il passaggio di un argomento per valore e per riferimento](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [Procedura: modificare il valore di un argomento di routine](./how-to-change-the-value-of-a-procedure-argument.md)   
 [Procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passaggio di argomenti in base alla posizione e in base al nome](./passing-arguments-by-position-and-by-name.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
