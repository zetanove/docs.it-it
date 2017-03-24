---
title: 'Procedura: modificare il valore di un argomento di routine (Visual Basic) | Documenti di Microsoft'
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
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
caps.latest.revision: 16
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
ms.openlocfilehash: 6c42a50b75bcc70ae0a3f70771b9e1f85626004b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-change-the-value-of-a-procedure-argument-visual-basic"></a>Procedura: cambiare il valore di un argomento di routine (Visual Basic)
Quando si chiama una routine, ciascun argomento specificato corrisponde a uno dei parametri definiti nella procedura. In alcuni casi, il codice della routine può modificare il valore sottostante a un argomento nel codice chiamante. In altri casi, la routine può modificare solo la copia locale di un argomento.  
  
 Quando si chiama la routine [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea una copia locale di ogni argomento passato [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md). Per ogni argomento passato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce il codice della routine un riferimento diretto all'elemento di programmazione sottostante all'argomento nel codice chiamante.  
  
 Se l'elemento sottostante nel codice chiamante è modificabile e viene passato l'argomento `ByRef`, il codice della routine può utilizzare il riferimento diretto per modificare il valore dell'elemento nel codice chiamante.  
  
## <a name="changing-the-underlying-value"></a>La modifica del valore sottostante  
  
#### <a name="to-change-the-underlying-value-of-a-procedure-argument-in-the-calling-code"></a>Per modificare il valore sottostante di un argomento di routine del codice chiamante  
  
1.  Nella dichiarazione di routine, specificare [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) per il parametro corrisponde all'argomento.  
  
2.  Nel codice chiamante, passare un elemento di programmazione modificabile come argomento.  
  
3.  Nel codice chiamante, non racchiudere l'argomento tra parentesi nell'elenco di argomenti.  
  
4.  Nel codice della routine, utilizzare il nome del parametro per assegnare un valore per l'elemento sottostante nel codice chiamante.  
  
 Vedere l'esempio più in basso per una dimostrazione.  
  
## <a name="changing-local-copies"></a>Modifica delle copie locali  
 Se l'elemento sottostante nel codice chiamante non è modificabile o se viene passato l'argomento `ByVal`, la routine non può modificare il valore del codice chiamante. Tuttavia, la routine può modificare la copia locale di questo tipo di argomento.  
  
#### <a name="to-change-the-copy-of-a-procedure-argument-in-the-procedure-code"></a>Per modificare la copia di un argomento di routine nel codice della routine  
  
1.  Nella dichiarazione di routine, specificare [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) per il parametro corrisponde all'argomento.  
  
     -oppure-  
  
     Nel codice chiamante, racchiudere l'argomento tra parentesi nell'elenco di argomenti. In tal modo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per passare l'argomento per valore, anche se il parametro corrispondente specifica `ByRef`.  
  
2.  Nel codice della routine, utilizzare il nome del parametro per assegnare un valore per la copia locale dell'argomento. Il valore sottostante nel codice chiamante non è stato modificato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente illustra due procedure che accettano una variabile di matrice e operano sui relativi elementi. Il `increase` procedura aggiunge semplicemente uno a ogni elemento. Il `replace` procedura assegna una nuova matrice al parametro `a()` , quindi aggiunge uno a ogni elemento.  
  
 [!code-vb[VbVbcnProcedures&#35;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_1.vb)]  
  
 [!code-vb[VbVbcnProcedures&#36;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_2.vb)]  
  
 [!code-vb[VbVbcnProcedures&#37;](./codesnippet/VisualBasic/how-to-change-the-value-of-a-procedure-argument_3.vb)]  
  
 Il primo `MsgBox` chiamata viene visualizzato "dopo Increase (n): 11, 21, 31, 41". Poiché la matrice `n` è un tipo di riferimento, `replace` possibile modificare i relativi membri, anche se è il meccanismo di passaggio `ByVal`.  
  
 Il secondo `MsgBox` chiamata viene visualizzato "dopo Replace (n): 101, 201, 301". Poiché `n` viene passato `ByRef`, `replace` possibile modificare la variabile `n` nel codice chiamante e assegnare una nuova matrice. Poiché `n` è un tipo di riferimento, `replace` inoltre possibile modificare i relativi membri.  
  
 È possibile impedire la procedura di modifica la variabile nel codice chiamante. Vedere [procedura: proteggere un argomento di routine modifica del valore](./how-to-protect-a-procedure-argument-against-value-changes.md).  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Quando si passa una variabile per riferimento, è necessario utilizzare il `ByRef` (parola chiave) per specificare tale meccanismo.  
  
 Il valore predefinito in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore. Tuttavia, è buona norma includere una programmazione di [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) (parola chiave) con ogni parametro dichiarato. In questo modo il codice più facile da leggere.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 È sempre presente un potenziale rischio per consentire a una procedura per modificare il valore sottostante a un argomento nel codice chiamante. Assicurarsi che si prevede che il valore modificato e in grado di verificare la validità prima di utilizzarlo.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Differenze tra argomenti modificabili e](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differenze tra il passaggio di un argomento per valore e per riferimento](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [Procedura: proteggere un argomento di routine modifica del valore](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [Procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passaggio di argomenti in base alla posizione e in base al nome](./passing-arguments-by-position-and-by-name.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
