---
title: "How to: Protect a Procedure Argument Against Value Changes (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, arguments"
  - "procedures, parameters"
  - "procedure arguments"
  - "arguments [Visual Basic], passing by reference"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], ByVal"
  - "arguments [Visual Basic], passing by value"
  - "procedure parameters"
  - "procedures, calling"
  - "arguments [Visual Basic], ByRef"
  - "arguments [Visual Basic], changing value"
ms.assetid: d2b7c766-ce16-4d2c-8d79-3fc0e7ba2227
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Protect a Procedure Argument Against Value Changes (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se una routine dichiara un parametro come [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] assegna al codice della routine un riferimento diretto all'elemento di programmazione sottostante all'argomento nel codice chiamante.  In questo modo, la routine può modificare il valore sottostante all'argomento nel codice chiamante.  In alcuni casi è necessario proteggere il codice da questo tipo di modifica.  
  
 Per proteggere sempre un argomento da eventuali modifiche, è possibile dichiarare il parametro [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) corrispondente nella routine.  Per consentire la modifica di un determinato argomento in alcuni casi e non in altri, è possibile dichiararlo `ByRef` e lasciare che il codice chiamante determini il meccanismo di passaggio in ogni chiamata.  A tale scopo l'argomento corrispondente viene racchiuso o meno tra parentesi a seconda che debba essere passato per valore o per riferimento.  Per ulteriori informazioni, vedere [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md).  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate due routine che accettano una variabile di matrice e operano sui relativi elementi.  La routine `increase` aggiunge semplicemente uno a ogni elemento.  La routine `replace` assegna una nuova matrice al parametro `a()`, quindi aggiunge uno a ogni elemento.  Tuttavia, la riassegnazione non ha effetto sulla variabile di matrice del codice chiamante.  
  
 [!code-vb[VbVbcnProcedures#35](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#38](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#37](./codesnippet/VisualBasic/how-to-protect-a-procedure-argument-against-value-changes_3.vb)]  
  
 Alla prima chiamata di `MsgBox` viene visualizzato "After increase\(n\): 11, 21, 31, 41".  Poiché la matrice `n` è un tipo di riferimento, la routine `replace` può modificarne i membri, anche se il meccanismo di passaggio è `ByVal`.  
  
 Alla seconda chiamata di `MsgBox` viene visualizzato "After replace\(n\): 11, 21, 31, 41".  Poiché `n` viene passata `ByVal`, la routine `replace` non può modificare la variabile `n` nel codice chiamante assegnandole una nuova matrice.  Quando `replace` crea la nuova istanza di matrice `k` e la assegna alla variabile locale `a`, perde il riferimento alla variabile `n` passata dal codice chiamante.  Quando la routine in questione modifica i membri di `a`, la modifica ha effetto solo sulla matrice locale `k` .  Pertanto, `replace` non incrementa i valori della matrice `n` nel codice chiamante.  
  
## Compilazione del codice  
 Per impostazione predefinita, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] gli argomenti vengono passati per valore.   È comunque buona norma di programmazione includere la parola chiave [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) con ogni parametro dichiarato,  al fine di agevolare la lettura del codice.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Differences Between Modifiable and Nonmodifiable Arguments](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [How to: Change the Value of a Procedure Argument](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)