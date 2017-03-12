---
title: "\ Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.\"
  - "\"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "division operator, integer"
  - "integer division operator"
  - "zero, division by zero"
  - "arithmetic operators, division"
  - "division, by zero"
  - "backslash (\) [Visual Basic]"
  - "\ operator [Visual Basic]"
  - "integer quotient"
  - "math operators"
  - "quotients, integer"
  - "truncation, integer division"
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# \ Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Divide due numeri e restituisce un Integer.  
  
## Sintassi  
  
```  
  
expression1 \ expression2  
```  
  
## Parti  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Tipi supportati  
 Tutti i tipi numerici, inclusi i tipi senza segno, a virgola mobile e `Decimal`.  
  
## Risultato  
 Il risultato è il quoziente integer di `expression1` diviso per `expression2`, in cui l'eventuale resto viene ignorato e viene mantenuta solo la parte integer.  Questo meccanismo è noto come *troncamento*.  
  
 Il tipo di dati del risultato è un tipo numerico appropriato in base ai tipi di dati di `expression1` ed `expression2`.  Per informazioni, vedere le tabelle "Operazioni aritmetiche su valori integer" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
 L'[\/ Operator](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) restituisce il quoziente completo, incluso il resto nella parte frazionaria.  
  
## Note  
 Prima di eseguire la divisione, viene effettuato il tentativo di convertire eventuali espressioni numeriche a virgola mobile in `Long`.  Se `Option Strict` è `On`, si verifica un errore del compilatore.  Se `Option Strict` è `Off`, è possibile che si verifichi un'eccezione <xref:System.OverflowException> se il valore non è compreso nell'intervallo del [Long Data Type](../../../visual-basic/language-reference/data-types/long-data-type.md).  La conversione in `Long` è inoltre soggetta a un particolare tipo di *arrotondamento*.  Per ulteriori informazioni, vedere "Parti frazionarie" in [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
  
 Se `expression1` o `expression2` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), tale parametro viene considerato uguale a zero.  
  
## Tentativo di divisione per zero  
 Se `expression2` restituisce zero, l'operatore `\` genera un'eccezione <xref:System.DivideByZeroException>.  Lo stesso vale per tutti i tipi di dati numerici degli operandi.  
  
> [!NOTE]
>  L'operatore `\` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `\` viene utilizzato per eseguire una divisione con Integer.  Il risultato è un Integer che rappresenta il quoziente integer dei due operandi, escluso il resto.  
  
 [!code-vb[VbVbalrOperators#18](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/integer-division-operator_1.vb)]  
  
 Le espressioni nell'esempio precedente restituiscono rispettivamente i valori 2, 3, 33 e \-22.  
  
## Vedere anche  
 [\\\= Operator](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [\/ Operator](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)