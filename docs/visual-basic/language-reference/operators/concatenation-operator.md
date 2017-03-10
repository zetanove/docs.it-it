---
title: "&amp; Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.&"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "And (&) operator"
  - "ampersand operator (&)"
  - "& operator"
  - "concatenation operators, syntax"
  - "strings [Visual Basic], concatenating"
ms.assetid: fefc3d00-cbf1-475c-8c5e-6fb213b3f85a
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &amp; Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Genera una concatenazione di stringhe di due espressioni.  
  
## Sintassi  
  
```  
  
result = expression1 & expression2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi variabile di tipo `String` o `Object`.  
  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione con un tipo di dati che viene convertito verso il tipo più grande `String`.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione con un tipo di dati che viene convertito verso il tipo più grande `String`.  
  
## Note  
 Se il tipo di dati di `expression1` o `expression2` non è `String` ma viene convertito verso il tipo più grande `String`, viene eseguita la conversione in tale tipo.  Se uno dei tipi di dati non viene convertito verso il tipo più grande `String`, viene generato un errore del compilatore.  
  
 Il tipo di dati di `result` è `String`.  Se una o entrambe le espressioni restituiscono [Nothing](../../../visual-basic/language-reference/nothing.md) o presentano un valore <xref:System.DBNull.Value?displayProperty=fullName>, vengono considerate come stringhe con valore "".  
  
> [!NOTE]
>  L'operatore `&` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
> [!NOTE]
>  Il carattere e commerciale \(&\) può essere utilizzato anche per identificare le variabili di tipo `Long`.  Per ulteriori informazioni, vedere [Type Characters](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `&` viene utilizzato per eseguire una concatenazione forzata di stringhe.  Il risultato è un valore stringa nel quale i due operandi risultano concatenati:  
  
 [!code-vb[VbVbalrOperators#2](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/concatenation-operator_1.vb)]  
  
## Vedere anche  
 [&\= Operator](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [Concatenation Operators](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Concatenation Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)