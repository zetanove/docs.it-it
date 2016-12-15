---
title: "* Operator (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.*"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "arithmetic operators, multiplication"
  - "operators [Visual Basic], multiplication"
  - "* operator [Visual Basic]"
  - "multiplication operator, syntax"
  - "math operators"
ms.assetid: 2b210382-99da-4195-89ba-b1d06f5e89ad
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# * Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di moltiplicare due numeri.  
  
## Sintassi  
  
```  
  
number1 * number2  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`number1`|Obbligatorio.  Qualsiasi espressione numerica.|  
|`number2`|Obbligatorio.  Qualsiasi espressione numerica.|  
  
## Risultato  
 Il risultato è il prodotto di `number1` per `number2`.  
  
## Tipi supportati  
 Tutti i tipi numerici, inclusi i tipi senza segno, a virgola mobile e `Decimal`.  
  
## Note  
 Il tipo di dati del risultato varia in base ai tipi degli operandi.  Nella tabella riportata di seguito viene illustrato come si determina il tipo di dati del risultato.  
  
|||  
|-|-|  
|Tipi di dati degli operandi|Tipo di dati del risultato|  
|Entrambe le espressioni sono tipi di dati integrali \([SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md), [Short](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md), [Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md), [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)\)|Un tipo di dati numerico appropriato per i tipi di dati di `number1` e `number2`.  Per informazioni, vedere le tabelle "Operazioni aritmetiche su valori integer" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).|  
|Entrambe le espressioni sono [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`|  
|Entrambe le espressioni sono [Single](../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`|  
|Una delle espressioni è un tipo di dati a virgola mobile \(`Single` o [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)\), ma non sono entrambe `Single` \(si tenga presente che `Decimal` non è un tipo di dati a virgola mobile\)|`Double`|  
  
 Se un'espressione restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), verrà considerata uguale a zero.  
  
## Overload  
 L'operatore `*` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `*` viene utilizzato per moltiplicare due numeri.  Il risultato ottenuto sarà il prodotto dei due operandi.  
  
 [!code-vb[VbVbalrOperators#4](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/multiplication-operator_1.vb)]  
  
## Vedere anche  
 [\*\= Operator](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)