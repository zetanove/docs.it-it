---
title: "/ Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb./"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "division operator, floating point"
  - "floating-point numbers, division operator"
  - "slash (/) operator"
  - "zero, division by zero"
  - "operators [Visual Basic], arithmetic"
  - "arithmetic operators, division"
  - "division, by zero"
  - "operators [Visual Basic], division"
  - "division operator, syntax"
  - "/ operator [Visual Basic]"
  - "math operators"
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# / Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Divide due numeri e restituisce un risultato a virgola mobile.  
  
## Sintassi  
  
```  
  
expression1 / expression2  
```  
  
## Parti  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Tipi supportati  
 Tutti i tipi numerici, inclusi i tipi senza segno, a virgola mobile e `Decimal`.  
  
## Risultato  
 Il risultato è il quoziente completo di `expression1` diviso per `expression2`, incluso l'eventuale resto.  
  
 L'[\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md) restituisce il quoziente espresso in valore integer, ossia senza resto.  
  
## Note  
 Il tipo di dati del risultato varia in base ai tipi degli operandi.  Nella tabella riportata di seguito viene illustrato come si determina il tipo di dati del risultato.  
  
|Tipi di dati degli operandi|Tipo di dati del risultato|  
|---------------------------------|--------------------------------|  
|Entrambe le espressioni sono tipi di dati integrali \([SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md), [Short](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md), [Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md), [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)\)|`Double`|  
|Un'espressione è costituita da un tipo di dati [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) e l'altra non è costituita da un tipo [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Single`|  
|Un'espressione è costituita da un tipo di dati [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) e l'altra non è costituita da un tipo [Single](../../../visual-basic/language-reference/data-types/single-data-type.md) o [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Decimal`|  
|Una delle espressioni è costituita da un tipo di dati [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
  
 Prima di eseguire la divisione, le espressioni numeriche integrali vengono convertite verso il tipo di dati più grande `Double`.  Se il risultato viene assegnato a un tipo di dati integrale, verrà eseguito il tentativo di convertire il risultato da `Double` in tale tipo.  Questo può generare un'eccezione se il risultato non corrisponde a questo tipo.  Per informazioni, vedere in particolare "Tentativo di divisione per zero" in questa pagina della Guida.  
  
 Se `expression1` o `expression2` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), tale parametro viene considerato uguale a zero.  
  
## Tentativo di divisione per zero  
 Se `expression2` restituisce zero, l'operatore `/` si comporta in maniera differente per i diversi tipi di dati degli operandi.  Nella tabella riportata di seguito vengono illustrati i possibili comportamenti.  
  
|Tipi di dati degli operandi|Comportamento se `expression2` è zero|  
|---------------------------------|-------------------------------------------|  
|Virgola mobile \(`Single` o `Double`\)|Restituisce infinito \(<xref:System.Double.PositiveInfinity> o <xref:System.Double.NegativeInfinity>\) oppure <xref:System.Double.NaN> \(non un numero\) se anche `expression1` è zero|  
|`Decimal`|Genera <xref:System.DivideByZeroException>|  
|Integrale \(con o senza segno\)|Se si tenta la conversione inversa al tipo integrale, viene generata un'eccezione <xref:System.OverflowException>, in quanto tutti i tipi integrali non accettano <xref:System.Double.PositiveInfinity>, <xref:System.Double.NegativeInfinity> o <xref:System.Double.NaN>|  
  
> [!NOTE]
>  L'operatore `/` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `/` viene utilizzato per eseguire una divisione a virgola mobile.  Il risultato è il quoziente dei due operandi.  
  
 [!code-vb[VbVbalrOperators#16](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/floating-point-division-operator_1.vb)]  
  
 Le espressioni dell'esempio precedente restituiscono i valori di 2,5 e 3,333333.  Il risultato è sempre a virgola mobile \(`Double`\), anche se entrambi gli operandi sono costanti integer.  
  
## Vedere anche  
 [\/\= Operator](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)