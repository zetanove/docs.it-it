---
title: "Comparison Operators (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<>"
  - "vb.>="
  - "vb.<="
  - "vb.>"
  - "vb.<"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "greater than or equal to operator [Visual Basic]"
  - ">= operator [Visual Basic]"
  - "= operator [Visual Basic]"
  - "< operator [Visual Basic]"
  - "less than operator [Visual Basic]"
  - "relational operators, syntax"
  - "Like operator [Visual Basic]"
  - "<> operator [Visual Basic]"
  - "> operator [Visual Basic]"
  - "equal operator [Visual Basic]"
  - "less than or equal to operator [Visual Basic]"
  - "symbols, operators"
  - "greater than operator [Visual Basic]"
  - "comparing values [Visual Basic]"
  - "operators [Visual Basic], relational"
  - "string comparison [Visual Basic]"
  - "not equal to comparison operator [Visual Basic]"
  - "<= operator [Visual Basic]"
  - "operators [Visual Basic], comparison"
  - "Is operator [Visual Basic]"
  - "comparison operators, Visual Basicl"
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Comparison Operators (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Di seguito sono riportati gli operatori di confronto definiti in Visual Basic:  
  
 Operatore `<`  
  
 Operatore `<=`  
  
 Operatore `>`  
  
 Operatore `>=`  
  
 Operatore `=`  
  
 Operatore `<>`  
  
 [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md)  
  
 [IsNot Operator](../../../visual-basic/language-reference/operators/isnot-operator.md)  
  
 [Like Operator](../../../visual-basic/language-reference/operators/like-operator.md)  
  
 Questi operatori consentono di confrontare due espressioni per determinare se sono uguali e, se non lo sono, quali sono le differenze.  Gli operatori `Is`, `IsNot` e `Like` verranno descritti in dettaglio in pagine specifiche della Guida.  In questa pagina, invece, vengono fornite informazioni dettagliate sugli operatori di confronto relazionali.  
  
## Sintassi  
  
```  
  
      result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Valore `Boolean` che rappresenta il risultato del confronto.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione.  
  
 `comparisonoperator`  
 Obbligatorio.  Qualsiasi operatore di confronto relazionale.  
  
 `object1`, `object2`  
 Obbligatorio.  Qualsiasi nome di oggetto di riferimento.  
  
 `string`  
 Obbligatorio.  Qualsiasi espressione `String`.  
  
 `pattern`  
 Obbligatorio.  Qualsiasi intervallo di caratteri o espressione `String`.  
  
## Note  
 Nella tabella riportata di seguito sono elencati gli operatori di confronto relazionali e le condizioni che determinano se `result` è `True` o `False`.  
  
|Operatore|`True` se|`False` se|  
|---------------|---------------|----------------|  
|`<` \(minore di\)|`expression1` \< `expression2`|`expression1` \>\= `expression2`|  
|`<=` \(minore o uguale a\)|`expression1` \<\= `expression2`|`expression1` \> `expression2`|  
|`>` \(maggiore di\)|`expression1` \> `expression2`|`expression1` \<\= `expression2`|  
|`>=` \(maggiore o uguale a\)|`expression1` \>\= `expression2`|`expression1` \< `expression2`|  
|`=` \(uguale a\)|`expression1` \= `expression2`|`expression1` \<\> `expression2`|  
|`<>` \(diverso da\)|`expression1` \<\> `expression2`|`expression1` \= `expression2`|  
  
> [!NOTE]
>  L'[\= Operator](../../../visual-basic/language-reference/operators/assignment-operator.md) viene utilizzato anche come operatore di assegnazione.  
  
 Gli operatori `Is`, `IsNot` e `Like` offrono funzionalità di confronto specifiche, diverse da quelle degli operatori inclusi nella precedente tabella.  
  
## Confronto tra numeri  
 Quando si confronta un'espressione di tipo `Single` con una di tipo `Double`, l'espressione `Single` viene convertita in `Double` contrariamente a quanto accadeva in Visual Basic 6.  
  
 Analogamente, quando si confronta un'espressione di tipo `Decimal` con una di tipo `Single` o `Double`, l'espressione `Decimal` viene convertita in `Single` o `Double`.  Per le espressioni di tipo `Decimal`, è possibile che vada perduto qualsiasi valore frazionario minore di 1E\-28.  Tali perdite potrebbero falsare il confronto tra due valori, facendoli risultare uguali anche se non lo sono.  È quindi consigliabile prestare la massima attenzione quando si utilizza il segno di uguaglianza \(`=`\) per confrontare due variabili a virgola mobile  ed è preferibile eseguire un test per verificare se il valore assoluto della differenza tra i due numeri è inferiore a una tolleranza minima accettabile.  
  
### Imprecisione dei numeri a virgola mobile  
 Quando si utilizzano numeri a virgola mobile, tenere presente che non vengono sempre memorizzati con una rappresentazione precisa.  Per questo motivo è possibile che determinate operazioni restituiscano risultati imprevisti, quali il confronto di valori e l'[Operatore Mod](../../../visual-basic/language-reference/operators/mod-operator.md).  Per ulteriori informazioni, vedere [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
## Confronto di stringhe  
 Quando viene eseguito un confronto tra stringhe, le espressioni stringa vengono valutate in base al relativo ordinamento alfabetico, che dipende dall'impostazione `Option Compare`.  
  
 `Option Compare Binary` consente di eseguire confronti tra stringhe basati su un tipo di ordinamento derivato dalle rappresentazioni binarie interne dei caratteri.  Il criterio di ordinamento è determinato dalla tabella codici.  Nell'esempio riportato di seguito viene illustrato un tipico criterio di ordinamento binario.  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 `Option Compare Text` consente di eseguire confronti tra stringhe basati su un criterio di ordinamento testuale, senza distinzione tra maiuscole e minuscole, determinato dalle impostazioni locali dell'applicazione.  Quando si imposta `Option Compare Text` e si ordinano i caratteri indicati nell'esempio precedente, viene applicato il criterio di ordinamento testuale riportato di seguito.  
  
 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`  
  
### Dipendenza dalle impostazioni locali  
 Quando si imposta `Option Compare Text`, il risultato di un confronto tra stringhe può dipendere dalle impostazioni locali con cui viene eseguita l'applicazione.  A seguito di un confronto è possibile che due caratteri risultino uguali con determinate impostazioni locali, ma non con altre.  Se si utilizza il confronto tra stringhe per decisioni importanti, ad esempio se accettare o meno un tentativo di accesso, si consiglia di prestare particolare attenzione alla sensibilità alle impostazioni locali.  È opportuno prendere in considerazione l'utilizzo dell'impostazione `Option Compare Binary` o la chiamata della <xref:Microsoft.VisualBasic.Strings.StrComp%2A>, che tiene conto delle impostazioni locali.  
  
## Programmazione senza tipi con operatori di confronto relazionali  
 L'utilizzo di operatori di confronto relazionali con espressioni `Object` non è consentito se è impostato `Option Strict On`.  Se `Option Strict` è impostato su `Off` e `expression1` o `expression2` è un'espressione `Object`, la modalità di confronto è determinata dai tipi in fase di esecuzione.  Nella tabella riportata di seguito vengono illustrate le modalità di confronto tra le espressioni e i relativi risultati in base al tipo degli operandi in fase di esecuzione.  
  
|Tipo di operandi|Modalità di confronto|  
|----------------------|---------------------------|  
|Entrambi `String`|Il confronto sarà basato sulle caratteristiche di ordinamento delle stringhe.|  
|Entrambi numerici|Gli oggetti verranno convertiti in `Double` e verrà eseguito il confronto numerico.|  
|Uno numerico e l'altro `String`|`String` verrà convertito nel tipo `Double` e verrà eseguito il confronto numerico.  Se non è possibile convertire l'operatore `String` in `Double`, verrà generata un'eccezione <xref:System.InvalidCastException>.|  
|Uno o entrambi gli operandi sono tipi di riferimento non di tipo `String`.|Viene generata un'eccezione <xref:System.InvalidCastException>.|  
  
 Nei confronti numerici `Nothing` viene considerato come 0.  I confronti di stringhe considerano `Nothing` come `""` \(una stringa vuota\).  
  
## Overload  
 Gli operatori di confronto relazionali \(`<`.  `<=`, `>`, `>=`, `=`, `<>`\) possono essere sottoposti a *overload*, ovvero una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza uno di questi operatori su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
 L'[\= Operator](../../../visual-basic/language-reference/operators/assignment-operator.md) può essere sottoposto a overload solo come operatore di confronto relazionale, non come operatore di assegnazione.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrati diversi utilizzi degli operatori di confronto relazionali che consentono di confrontare espressioni.  Gli operatori di confronto relazionali restituiscono un risultato `Boolean` che indica se l'espressione specificata è `True`.  Quando si applicano alle stringhe gli operatori `>` e `<`, il confronto viene eseguito utilizzando il normale criterio di ordinamento alfabetico delle stringhe,  che può dipendere dalle impostazioni locali.  La distinzione tra maiuscole e minuscole, ad esempio, dipende dall'impostazione di [Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md).  
  
 [!code-vb[VbVbalrOperators#1](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/comparison-operators_1.vb)]  
  
 Nell'esempio precedente il primo confronto restituisce `False`, mentre gli altri confronti restituiscono `True`.  
  
## Vedere anche  
 <xref:System.InvalidCastException>   
 [\= Operator](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Comparison Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)