---
title: "Comparison Operators in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "comparison operators, comparing strings"
  - "comparison operators, comparing objects"
  - "strings [Visual Basic], comparing"
  - "comparison operators"
  - "string comparison [Visual Basic], operators"
  - "objects [Visual Basic], comparing"
  - "numbers, comparing"
  - "Visual Basic code, operators"
  - "string comparison [Visual Basic]"
  - "numeric values, comparing"
  - "comparison operators, comparing numeric values"
  - "operators [Visual Basic], comparison"
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Comparison Operators in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli operatori di confronto consentono di confrontare due espressioni e di ottenere un valore `Boolean` che rappresenta la relazione esistente tra i valori delle espressioni.  Esistono operatori per il confronto di valori numerici, operatori per il confronto di stringhe e operatori per il confronto di oggetti.  Di seguito vengono esaminati i tre tipi di operatori.  
  
## Confronto di valori numerici  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] confronta i valori numerici mediante sei operatori di confronto numerico.  Ciascun operatore considera come operandi due espressioni che restituiscono valori numerici.  Nella tabella riportata di seguito vengono elencati gli operatori e vengono visualizzati esempi per ciascuno di essi.  
  
|Operatore|Condizione verificata|Esempi|  
|---------------|---------------------------|------------|  
|`=` \(uguaglianza\)|Il valore della prima espressione è uguale al valore della seconda?|`23`   `=`   `33    ' False`<br /><br /> `23`   `=`   `23    ' True`<br /><br /> `23`   `=`   `12    ' False`|  
|`<>` \(diseguaglianza\)|Il valore della prima espressione è diverso dal valore della seconda?|`23`   `<>`   `33    ' True`<br /><br /> `23`   `<>`   `23    ' False`<br /><br /> `23`   `<>`   `12    ' True`|  
|`<` \(minore di\)|Il valore della prima espressione è minore del valore della seconda?|`23`   `<`   `33    ' True`<br /><br /> `23`   `<`   `23    ' False`<br /><br /> `23`   `<`   `12    ' False`|  
|`>` \(maggiore di\)|Il valore della prima espressione è maggiore del valore della seconda?|`23`   `>`   `33    ' False`<br /><br /> `23`   `>`   `23    ' False`<br /><br /> `23`   `>`   `12    ' True`|  
|`<=` \(minore o uguale a\)|Il valore della prima espressione è minore o uguale al valore della seconda?|`23`   `<=`   `33    ' True`<br /><br /> `23`   `<=`   `23    ' True`<br /><br /> `23`   `<=`   `12    ' False`|  
|`>=` \(maggiore o uguale a\)|Il valore della prima espressione è maggiore o uguale al valore della seconda?|`23`   `>=`   `33    ' False`<br /><br /> `23`   `>=`   `23    ' True`<br /><br /> `23`   `>=`   `12    ' True`|  
  
## Confronto di stringhe  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] confronta le stringhe mediante l'operatore [Like Operator](../../../../visual-basic/language-reference/operators/like-operator.md) e utilizzando gli operatori di confronto numerico.  L'operatore `Like` consente di specificare un modello.  La stringa quindi viene confrontata con il modello e, in caso di corrispondenza, il risultato è `True`.  In caso contrario, il risultato sarà `False`.  Gli operatori numerici consentono di confrontare valori `String` in base al relativo tipo di ordinamento, come illustrato nell'esempio seguente.  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 Il risultato dell'esempio precedente è `True` perché il primo carattere della prima stringa, secondo l'ordinamento, precede il primo carattere della seconda stringa.  Se i primi caratteri fossero uguali, verrebbe eseguito il confronto con il carattere successivo di entrambe le stringhe e così via.  È possibile anche verificare l'uguaglianza delle stringhe per mezzo dell'operatore di uguaglianza, come indicato nell'esempio seguente.  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 Se una stringa è il prefisso di un'altra, come nel caso di "aa" e "aaa", la stringa più lunga viene considerata maggiore di quella più corta.  Questa condizione è illustrata nell'esempio che segue.  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 Il criterio di ordinamento verrà basato su un confronto binario o un confronto testuale, a seconda dell'impostazione di `Option Compare`.  Per ulteriori informazioni, vedere [Option Compare Statement](../../../../visual-basic/language-reference/statements/option-compare-statement.md).  
  
## Confronto di oggetti  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] confronta due variabili di riferimento a oggetti mediante gli operatori [Is Operator](../../../../visual-basic/language-reference/operators/is-operator.md) e [IsNot Operator](../../../../visual-basic/language-reference/operators/isnot-operator.md).  È possibile utilizzare uno di questi operatori per stabilire se due variabili di riferimento si riferiscono alla stessa istanza di un oggetto.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#65](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_1.vb)]  
  
 Nell'esempio precedente, `x Is y` restituisce `True`, perché entrambe le variabili fanno riferimento alla stessa istanza.  Si confronti questo risultato con il seguente esempio.  
  
 [!code-vb[VbVbalrOperators#66](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_2.vb)]  
  
 Nell'esempio precedente, `x Is y` restituisce `False` perché, sebbene le variabili si riferiscano a oggetti dello stesso tipo, fanno riferimento a istanze diverse di quel tipo.  
  
 Quando si desidera effettuare un controllo su due oggetti che non puntano alla stessa istanza, l'operatore `IsNot` consente di evitare una combinazione grammaticalmente impropria di `Not` e `Is`.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#67](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_3.vb)]  
  
 Nell'esempio precedente, `If a IsNot b` è equivalente a `If Not a Is b`.  
  
### Confronto del tipo di oggetto  
 Per verificare se un oggetto è di un particolare tipo, utilizzare l'espressione `TypeOf`...`Is`.  La sintassi è la seguente:  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 Quando l'oggetto `typename` specifica un tipo di interfaccia, l'espressione `TypeOf`...`Is` restituisce `True` se l'oggetto implementa il tipo di interfaccia.  Quando l'oggetto `typename` è un tipo di classe, l'espressione restituisce `True` se l'oggetto è un'istanza della classe specificata o di una classe da essa derivata.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#68](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_4.vb)]  
  
 Nell'esempio precedente, l'espressione `TypeOf x Is Control` restituisce `True` perché il tipo di `x` è `Button`, che eredita da `Control`.  
  
 Per ulteriori informazioni, vedere [TypeOf Operator](../../../../visual-basic/language-reference/operators/typeof-operator.md).  
  
## Vedere anche  
 [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Comparison Operators](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Operators](../../../../visual-basic/language-reference/operators/index.md)   
 [Arithmetic Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Concatenation Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)