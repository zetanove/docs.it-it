---
title: "Operatore Mod (Visual Basic) | Microsoft Docs"
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
  - "vb.Mod"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "resto (operatore Mod)"
  - "operatore di divisione, operatore Mod"
  - "modulo (operatore), Visual Basic"
  - "Mod (operatore) [Visual Basic]"
  - "operatori [Visual Basic], divisione"
  - "operatori aritmetici, Mod"
  - "matematici (operatori)"
ms.assetid: 6ff7e40e-cec8-4c77-bff6-8ddd2791c25b
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operatore Mod (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Divide due numeri e restituisce solo il resto.  
  
## Sintassi  
  
```  
  
number1 Mod number2  
```  
  
## Parti  
 `number1`  
 Necessario.  Qualsiasi espressione numerica.  
  
 `number2`  
 Necessario.  Qualsiasi espressione numerica.  
  
## Tipi supportati  
 Tutti i tipi numerici.  Sono inclusi i tipi non firmati e a virgola mobile e `Decimal`.  
  
## Risultato  
 Il risultato è il resto della divisione di `number1` per `number2`.  Ad esempio, l'espressione `14 Mod 4` restituisce 2.  
  
## Note  
 Se `number1` o `number2` sono valori a virgola mobile, viene restituito il resto a virgola mobile della divisione.  Il tipo di dati del risultato corrisponde al tipo di dati più piccolo che può contenere tutti i possibili valori risultanti dalla divisione con i tipi di dati di `number1` e `number2`.  
  
 Se `number1` o `number2` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), tale parametro viene considerato uguale a zero.  
  
 Gli operatori correlati includono gli elementi seguenti:  
  
-   [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md) restituisce il quoziente intero di una divisione.  Ad esempio, l'espressione `14 \ 4` restituisce 3.  
  
-   [\/ Operator](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) restituisce il quoziente completo, incluso il resto, come un numero a virgola mobile.  Ad esempio, l'espressione `14 / 4` restituisce 3,5.  
  
## Tentativo di divisione per zero  
 Se `number2` restituisce zero, il comportamento dell'operatore `Mod` dipenderà dal tipo di dati degli operandi.  Una divisione integrale genera un'eccezione <xref:System.DivideByZeroException>.  Una divisione a virgola mobile restituisce <xref:System.Double.NaN>.  
  
## Formula equivalente  
 L'espressione `a Mod b` è equivalente a una delle seguenti formule:  
  
 `a - (b * (a \ b))`  
  
 `a - (b * Fix(a / b))`  
  
## Imprecisione dei valori a virgola mobile  
 Quando si utilizzano numeri a virgola mobile, tenere presente che non sempre contengono una rappresentazione precisa in memoria.  Per questo motivo, è possibile che determinate operazioni restituiscano risultati imprevisti, come il confronto dei valori e l'operatore `Mod`.  Per ulteriori informazioni, vedere [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
## Overload  
 È possibile eseguire l'*overload* dell'operatore `Mod`; ciò significa che una classe o una struttura possono ridefinire il relativo comportamento.  Se il codice applica `Mod` a un'istanza di una classe o di una struttura che include tale overload, assicurarsi di avere compreso il comportamento ridefinito.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Mod` viene utilizzato per dividere due numeri e restituire solo il resto.  Se uno dei numeri è a virgola mobile, il risultato sarà il resto espresso con un numero a virgola mobile.  
  
 [!code-vb[VbVbalrOperators#31](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/mod-operator_1.vb)]  
  
## Esempio  
 Nell''esempio riportato di seguito viene illustrata la potenziale imprecisione degli operandi a virgola mobile.  Nella prima istruzione gli operandi sono `Double` e 0.2 è una frazione binaria ripetuta all'infinito con un valore memorizzato pari a 0.20000000000000001.  Nella seconda istruzione il carattere di tipo letterale `D` impone che entrambi gli operandi siano `Decimal` e la rappresentazione di 0.2 è precisa.  
  
 [!code-vb[VbVbalrOperators#32](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/mod-operator_2.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Conversion.Int%2A>   
 <xref:Microsoft.VisualBasic.Conversion.Fix%2A>   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md)