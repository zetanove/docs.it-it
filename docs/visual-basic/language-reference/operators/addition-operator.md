---
title: "+ Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.+"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "arithmetic operators, addition"
  - "+ operator"
  - "concatenation operators, syntax"
  - "strings [Visual Basic], concatenating"
  - "sum operator"
ms.assetid: 5694778f-0a2c-4539-8009-f66f318fb46d
caps.latest.revision: 26
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 26
---
# + Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Somma due numeri o restituisce il valore positivo di un'espressione numerica.  Può essere utilizzato anche per concatenare due espressioni stringa.  
  
## Sintassi  
  
```  
  
      expression1 + expression2  
- or -  
+ expression1  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`expression1`|Obbligatorio.  Qualsiasi espressione numerica o stringa.|  
|`expression2`|Obbligatoria, a meno che con l'operatore `+` non venga calcolato un valore negativo.  Qualsiasi espressione numerica o stringa.|  
  
## Risultato  
 Se `expression1` ed `expression2` sono entrambe di tipo numerico, il risultato è rappresentato dalla relativa somma aritmetica.  
  
 Se `expression2` è assente, l'operatore `+` rappresenta l'operatore di identità *unario* per il valore non modificato di un'espressione.  In questo caso, l'operazione consiste nel mantenere il segno di `expression1`, in modo che il risultato sia negativo se `expression1` è negativa.  
  
 Se `expression1` ed `expression2` sono entrambe di tipo stringa, il risultato è rappresentato dalla concatenazione dei rispettivi valori.  
  
 Se `expression1` ed `expression2` sono di tipo diverso, l'azione eseguita dipende dal tipo, dal contenuto e dall'impostazione dell'[Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md).  Per ulteriori informazioni, vedere le tabelle nella sezione relativa alle osservazioni.  
  
## Tipi supportati  
 Tutti i tipi numerici, inclusi i tipi senza segno, a virgola mobile, `Decimal` e `String`.  
  
## Note  
 In generale, `+` esegue la somma aritmetica quando possibile e la concatenazione solo nel caso in cui entrambe le espressioni siano stringhe.  
  
 Se nessuna delle due espressioni è di tipo `Object`, verranno eseguite le operazioni riportate di seguito.  
  
|||  
|-|-|  
|Tipi di dati delle espressioni|Operazione del compilatore|  
|Entrambe le espressioni sono tipi di dati numerici \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single` o `Double`\)|Verrà eseguita una somma.  Il tipo di dati del risultato è un tipo numerico appropriato in base ai tipi di dati di `expression1` ed `expression2`.  Per informazioni, vedere le tabelle "Operazioni aritmetiche su valori integer" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).|  
|Entrambe le espressioni sono di tipo `String`|Verrà eseguita una concatenazione.|  
|Un'espressione è di tipo numerico e l'altra è una stringa|Se `Option Strict` è `On`, verrà generato un errore del compilatore.<br /><br /> Se `Option Strict` è `Off`, verranno eseguite la conversione implicita di `String` in `Double` e la somma.<br /><br /> Se `String` non può essere convertito in `Double`, verrà generata un'eccezione <xref:System.InvalidCastException>.|  
|Un'espressione è di tipo numerico e l'altra è [Nothing](../../../visual-basic/language-reference/nothing.md)|Verrà eseguita una somma assegnando a `Nothing` il valore zero.|  
|Un'espressione è una stringa e l'altra è `Nothing`|Verrà eseguita una concatenazione assegnando a `Nothing` il valore "".|  
  
 Se una delle due espressioni è di tipo `Object`, verranno eseguite le operazioni riportate di seguito.  
  
|||  
|-|-|  
|Tipi di dati delle espressioni|Operazione del compilatore|  
|L'espressione `Object` contiene un valore numerico mentre l'altra è un tipo di dati numerico|Se `Option Strict` è `On`, verrà generato un errore del compilatore.<br /><br /> Se `Option Strict` è `Off`, verrà eseguita la somma.|  
|`Object` contiene un valore numerico mentre l'altra espressione è di tipo `String`|Se `Option Strict` è `On`, verrà generato un errore del compilatore.<br /><br /> Se `Option Strict` è `Off`, verranno eseguite la conversione implicita di `String` in `Double` e la somma.<br /><br /> Se `String` non può essere convertito in `Double`, verrà generata un'eccezione <xref:System.InvalidCastException>.|  
|L'espressione `Object` contiene una stringa mentre l'altra espressione è un tipo di dati numerico|Se `Option Strict` è `On`, verrà generato un errore del compilatore.<br /><br /> Se `Option Strict` è `Off`, verranno eseguite la conversione implicita di `Object` in `Double` e la somma.<br /><br /> Se l'espressione `Object` di tipo stringa non può essere convertita in `Double`, verrà generata un'eccezione <xref:System.InvalidCastException>.|  
|`Object` contiene una stringa mentre l'altra espressione è di tipo `String`|Se `Option Strict` è `On`, verrà generato un errore del compilatore.<br /><br /> Se `Option Strict` è `Off`, verranno eseguite la conversione implicita di `Object` in `String` e la concatenazione.|  
  
 Se entrambe le espressioni sono di tipo `Object`, verranno eseguite le operazioni riportate di seguito \(solo `Option Strict Off`\).  
  
|||  
|-|-|  
|Tipi di dati delle espressioni|Operazione del compilatore|  
|Entrambe le espressioni `Object` contengono valori numerici|Verrà eseguita una somma.|  
|Entrambe le espressioni `Object` sono di tipo `String`|Verrà eseguita una concatenazione.|  
|Un'espressione `Object` contiene un valore numerico mentre l'altra contiene una stringa|Verranno eseguite la conversione implicita dell'espressione `Object` di tipo stringa in `Double` e la somma.<br /><br /> Se l'espressione `Object` di tipo stringa non può essere convertita in un valore numerico, verrà generata un'eccezione <xref:System.InvalidCastException>.|  
  
 Se una delle due espressioni `Object` restituisce [Nothing](../../../visual-basic/language-reference/nothing.md) o <xref:System.DBNull>, l'operatore `+` la considererà di tipo `String` con valore "".  
  
> [!NOTE]
>  Quando si utilizza l'operatore `+`, non sempre è possibile stabilire se verrà eseguita una somma o una concatenazione di stringhe.  Per eliminare qualsiasi ambiguità e fornire codice autodocumentato, si consiglia di utilizzare l'operatore `&` per la concatenazione.  
  
## Overload  
 L'operatore `+` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `+` viene utilizzato per eseguire la somma di numeri.  Se gli operandi sono entrambi numerici, verrà calcolato il risultato aritmetico.  Il risultato aritmetico rappresenta la somma dei due operandi.  
  
 [!code-vb[VbVbalrOperators#6](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_1.vb)]  
  
 L'operatore `+` consente anche di concatenare stringhe.  Se gli operandi sono entrambi stringhe, verrà eseguita la concatenazione.  Il risultato dell'operazione di concatenazione rappresenta una stringa singola costituita dal contenuto dei due operandi in successione.  
  
 Se gli operandi appartengono a tipi diversi, il risultato dipende dall'impostazione dell'[Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md).  Nell'esempio riportato di seguito viene illustrato il risultato che si ottiene quando `Option Strict` è `On`.  
  
 [!code-vb[VbVbalrOperators#53](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_2.vb)]  
  
 [!code-vb[VbVbalrOperators#50](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_3.vb)]  
[!code-vb[VbVbalrOperators#51](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_4.vb)]  
  
 Nell'esempio riportato di seguito viene illustrato il risultato che si ottiene quando `Option Strict` è `Off`.  
  
 [!code-vb[VbVbalrOperators#54](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_5.vb)]  
  
 [!code-vb[VbVbalrOperators#50](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_3.vb)]  
[!code-vb[VbVbalrOperators#52](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-operator_6.vb)]  
  
 Per eliminare qualsiasi ambiguità, si consiglia di eseguire la concatenazione utilizzando l'operatore `&` anziché `+`.  
  
## Vedere anche  
 [& Operator](../../../visual-basic/language-reference/operators/concatenation-operator.md)   
 [Concatenation Operators](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)