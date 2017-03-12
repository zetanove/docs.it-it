---
title: "Differences Between Modifiable and Nonmodifiable Arguments (Visual Basic) | Microsoft Docs"
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
  - "procedure arguments"
  - "arguments [Visual Basic], nonmodifiable"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], modifiable"
ms.assetid: 87b2df69-e1f7-4657-9caf-b3f48d693428
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Differences Between Modifiable and Nonmodifiable Arguments (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si chiama una routine, generalmente si passano uno o più argomenti.  Ogni argomento corrisponde a un elemento di programmazione sottostante.  Sia gli elementi sottostanti che gli argomenti stessi possono essere modificabili o meno.  
  
## Elementi modificabili e non modificabili  
 Un elemento di programmazione può essere un *elemento modificabile*, ovvero con un valore che può essere modificato, o un *elemento non modificabile*, ovvero con  un valore che resta fisso in seguito alla relativa creazione.  
  
 Nella tabella riportata di seguito sono elencati elementi di programmazione modificabili e non modificabili.  
  
|Elementi modificabili|Elementi non modificabili|  
|---------------------------|-------------------------------|  
|Variabili locali dichiarate all'interno delle routine, incluse le variabili oggetto, ad eccezione di quelle di sola lettura|Variabili, campi e proprietà di sola lettura|  
|Campi \(variabili membro di moduli, classi e strutture\), ad eccezione di quelli di sola lettura|Costanti e valori letterali|  
|Proprietà, ad eccezione di quelle di sola lettura|Membri di enumerazione|  
|Elementi di matrice|Espressioni \(anche se i relativi elementi sono modificabili\)|  
  
## Argomenti modificabili e non modificabili  
 Un *argomento modificabile* contiene un elemento sottostante modificabile.  È possibile memorizzare un nuovo valore nel codice chiamante in qualsiasi momento, nonché modificare l'elemento sottostante di tale codice mediante il codice della routine se l'argomento viene passato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  
  
 Un *argomento non modificabile* contiene un elemento sottostante non modificabile o viene passato [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md).  Non è possibile modificare l'elemento sottostante nel codice chiamante mediante la routine, anche se si tratta di un elemento modificabile.  Se è un elemento non modificabile, non può essere modificato mediante il codice chiamante.  
  
 La routine chiamata può modificare la rispettiva copia locale di un argomento non modificabile, ma tale modifica non ha effetto sull'elemento sottostante nel codice chiamante.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [How to: Change the Value of a Procedure Argument](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [How to: Protect a Procedure Argument Against Value Changes](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [How to: Force an Argument to Be Passed by Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)