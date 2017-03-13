---
title: "&lt;&lt; Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<<"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "bit shift operators"
  - "<< operator [Visual Basic]"
  - "operator <<, Visual Basic left shift operator"
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# &lt;&lt; Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue uno spostamento aritmetico a sinistra su uno schema di bit.  
  
## Sintassi  
  
```  
  
result = pattern << amount  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Valore numerico integrale.  Risultato dello spostamento dello schema di bit.  Il tipo di dati corrisponde a quello di `pattern`.  
  
 `pattern`  
 Obbligatorio.  Espressione numerica integrale.  Schema di bit da spostare.  Il tipo di dati deve essere integrale \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` o `ULong`\).  
  
 `amount`  
 Obbligatorio.  Espressione numerica.  Numero di bit per spostare lo schema di bit.  Il tipo di dati deve essere `Integer` o ampliato a `Integer`.  
  
## Note  
 Gli spostamenti aritmetici non sono circolari. In altre parole, i bit spostati oltre una delle estremità del risultato non vengono reintrodotti all'altra estremità.  In uno spostamento aritmetico a sinistra, i bit spostati oltre l'intervallo del tipo di dati del risultato vengono ignorati e le posizioni dei bit liberate a destra sono impostate su zero.  
  
 Per impedire lo spostamento di un numero di bit superiore a quello che il risultato può contenere, il valore di `amount` verrà nascosto con una maschera di dimensioni corrispondente al tipo di dati di `pattern`.  Il valore binario AND di questi valori viene utilizzato per l'entità dello spostamento.  Le maschere di dimensioni sono le seguenti:  
  
|Tipo di dati di `pattern`|Maschera di dimensioni \(decimale\)|Maschera di dimensioni \(esadecimale\)|  
|-------------------------------|-----------------------------------------|--------------------------------------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 Se `amount` è uguale a zero, il valore di `result` sarà identico al valore di `pattern`.  Se `amount` è negativo, verrà accettato come valore senza segno e nascosto con la maschera di dimensioni appropriata.  
  
 Gli spostamenti aritmetici non generano mai eccezioni di overflow.  
  
> [!NOTE]
>  L'operatore `<<` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `<<` viene utilizzato per eseguire spostamenti aritmetici a sinistra su valori integrali.  Il risultato presenta sempre lo stesso tipo di dati dell'espressione in cui è stato effettuato lo spostamento.  
  
 [!code-vb[VbVbalrOperators#12](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/left-shift-operator_1.vb)]  
  
 Di seguito sono riportati i risultati dell'esempio precedente:  
  
-   `result1` è 192 \(0000 0000 1100 0000\).  
  
-   `result2` è 3072 \(0000 1100 0000 0000\).  
  
-   `result3` è \-32768 \(1000 0000 0000 0000\).  
  
-   `result4` è 384 \(0000 0001 1000 0000\).  
  
-   `result5` è 0 \(con uno spostamento di 15 posizioni a sinistra\).  
  
 L'entità dello spostamento per `result4` viene calcolata come 17 AND 15, pari a 1.  
  
## Vedere anche  
 [Bit Shift Operators](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [\<\<\= Operator](../../../visual-basic/language-reference/operators/left-shift-assignment-operator.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)