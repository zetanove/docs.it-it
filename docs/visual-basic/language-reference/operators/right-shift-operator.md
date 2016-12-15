---
title: "&gt;&gt; Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.>>"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operator>>"
  - ">> operator [Visual Basic]"
  - "bit shift operators"
  - "operator >>"
  - "right shift operators"
ms.assetid: 054dc6a6-47d9-47ef-82da-cfa2b59fbf8f
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &gt;&gt; Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Esegue uno spostamento aritmetico a destra su uno schema di bit.  
  
## Sintassi  
  
```  
  
result = pattern >> amount  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Valore numerico integrale.  Risultato dello spostamento dello schema di bit.  Il tipo di dati corrisponde a quello di `pattern`.  
  
 `pattern`  
 Obbligatorio.  Espressione numerica integrale.  Schema di bit da spostare.  Il tipo di dati deve essere integrale \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` o `ULong`\).  
  
 `amount`  
 Obbligatorio.  Espressione numerica.  Numero di bit per spostare lo schema di bit.  Il tipo di dati deve essere `Integer` o ampliato a `Integer`.  
  
## Note  
 Gli spostamenti aritmetici non sono circolari. In altre parole, i bit spostati oltre una delle estremità del risultato non vengono reintrodotti all'altra estremità.  In uno spostamento aritmetico a destra, i bit spostati oltre la posizione dei bit all'estrema destra vengono ignorati e il bit all'estrema sinistra \(segno\) viene propagato nelle posizioni di bit liberate a sinistra.  Questo significa che se `pattern` ha un valore negativo, le posizioni liberate vengono impostate su uno. In caso contrario, vengono impostate su zero.  
  
 I tipi di dati `Byte`, `UShort`, `UInteger` e `ULong` sono senza segno. Non esiste pertanto alcun bit di segno da propagare.  Se `pattern` è di uno dei tipi senza segno, le posizioni liberate sono sempre impostate su zero.  
  
 Per impedire lo spostamento di un numero di bit superiore a quello che il risultato può contenere, il valore di `amount` verrà nascosto con una maschera di dimensioni corrispondente al tipo di dati di `pattern`.  Il valore binario AND di questi valori viene utilizzato per l'entità dello spostamento.  Le maschere di dimensioni sono le seguenti:  
  
|Tipo di dati di `pattern`|Maschera di dimensioni \(decimale\)|Maschera di dimensioni \(esadecimale\)|  
|-------------------------------|-----------------------------------------|--------------------------------------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 Se `amount` è uguale a zero, il valore di `result` sarà identico al valore di `pattern`.  Se `amount` è negativo, verrà accettato come valore senza segno e nascosto con la maschera di dimensioni appropriata.  
  
 Gli spostamenti aritmetici non generano mai eccezioni di overflow.  
  
## Overload  
 L'operatore `>>` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `>>` viene utilizzato per eseguire spostamenti aritmetici a destra su valori integrali.  Il risultato presenta sempre lo stesso tipo di dati dell'espressione in cui è stato effettuato lo spostamento.  
  
 [!code-vb[VbVbalrOperators#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/right-shift-operator_1.vb)]  
  
 Di seguito sono riportati i risultati dell'esempio precedente:  
  
-   `result1` è 2560 \(0000 1010 0000 0000\).  
  
-   `result2` è 160 \(0000 0000 1010 0000\).  
  
-   `result3` è 2 \(0000 0000 0000 0010\).  
  
-   `result4` è 640 \(0000 0010 1000 0000\).  
  
-   `result5` è 0 \(con uno spostamento di 15 posizioni a destra\).  
  
 L'entità dello spostamento per `result4` viene calcolata come 18 AND 15, pari a 2.  
  
 Nell'esempio riportato di seguito vengono illustrati gli spostamenti aritmetici su un valore negativo.  
  
 [!code-vb[VbVbalrOperators#55](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/right-shift-operator_2.vb)]  
  
 Di seguito sono riportati i risultati dell'esempio precedente:  
  
-   `negresult1` è \-512 \(1111 1110 0000 0000\).  
  
-   `negresult2` è \-1 \(il bit di segno è stato propagato\).  
  
## Vedere anche  
 [Bit Shift Operators](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [\>\>\= Operator](../../../visual-basic/language-reference/operators/right-shift-assignment-operator.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)