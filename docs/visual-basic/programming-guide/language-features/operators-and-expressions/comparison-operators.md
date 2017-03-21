---
title: Operatori di confronto in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- comparison operators, comparing strings
- comparison operators, comparing objects
- strings [Visual Basic], comparing
- comparison operators
- string comparison [Visual Basic], operators
- objects [Visual Basic], comparing
- numbers, comparing
- Visual Basic code, operators
- string comparison [Visual Basic]
- numeric values, comparing
- comparison operators, comparing numeric values
- operators [Visual Basic], comparison
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
caps.latest.revision: 13
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6185d1676f2cd160c9c3e855cce4a6d2bbe2ffb4
ms.lasthandoff: 03/13/2017

---
# <a name="comparison-operators-in-visual-basic"></a>Comparison Operators in Visual Basic
Operatori di confronto confrontare due espressioni e restituire un `Boolean` che rappresenta la relazione tra i relativi valori. Sono disponibili operatori per il confronto di valori numerici, operatori di confronto di stringhe e operatori di confronto di oggetti. Di seguito vengono esaminati i tre tipi di operatori.  
  
## <a name="comparing-numeric-values"></a>Confronto di valori numerici  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Confronta i valori numerici mediante sei operatori di confronto numerico. Ogni operatore ha come operandi due espressioni che restituiscono valori numerici. Nella tabella seguente sono elencati gli operatori e vengono illustrati esempi di ognuno.  
  
|Operatore|Condizione di test|Esempi|  
|--------------|----------------------|--------------|  
|`=`(Uguaglianza)|È il valore della prima espressione è uguale al valore del secondo?|`23`   `=`   `33    ' False`<br /><br /> `23`   `=`   `23    ' True`<br /><br /> `23`   `=`   `12    ' False`|  
|`<>`(Disuguaglianza)|Il valore della prima espressione non è uguale al valore del secondo?|`23`   `<>`   `33    ' True`<br /><br /> `23`   `<>`   `23    ' False`<br /><br /> `23`   `<>`   `12    ' True`|  
|`<`(Minore di)|È il valore della prima espressione minore del valore del secondo?|`23`   `<`   `33    ' True`<br /><br /> `23`   `<`   `23    ' False`<br /><br /> `23`   `<`   `12    ' False`|  
|`>`(Maggiore di)|È il valore della prima espressione è maggiore del valore del secondo?|`23`   `>`   `33    ' False`<br /><br /> `23`   `>`   `23    ' False`<br /><br /> `23`   `>`   `12    ' True`|  
|`<=`(Minore o uguale a)|Il valore della prima espressione è minore o uguale al valore del secondo?|`23`   `<=`   `33    ' True`<br /><br /> `23`   `<=`   `23    ' True`<br /><br /> `23`   `<=`   `12    ' False`|  
|`>=`(Maggiore o uguale a)|È il valore della prima espressione maggiore o uguale al valore del secondo?|`23`   `>=`   `33    ' False`<br /><br /> `23`   `>=`   `23    ' True`<br /><br /> `23`   `>=`   `12    ' True`|  
  
## <a name="comparing-strings"></a>Confronto di stringhe  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Confronta le stringhe mediante la [operatore Like](../../../../visual-basic/language-reference/operators/like-operator.md) nonché gli operatori di confronto numerico. Il `Like` operatore consente di specificare un modello. La stringa viene quindi confrontata con il modello e se corrisponde, il risultato è `True`. In caso contrario, il risultato è `False`. Operatori numerici consentono di confrontare `String` valori in base al relativo tipo di ordinamento, come illustrato nell'esempio seguente.  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 Il risultato dell'esempio precedente è `True` perché il primo carattere della prima stringa precede il primo carattere della seconda stringa. Se i primi caratteri, il confronto potrebbe continuare per il carattere successivo in entrambe le stringhe e così via. È inoltre possibile testare l'uguaglianza di stringhe tramite l'operatore di uguaglianza, come illustrato nell'esempio seguente.  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 Se una stringa è un prefisso di un altro, ad esempio "aa" e "aaa", viene considerata la stringa di lunghezza superiore a quella più corta. Questa condizione è illustrata nell'esempio seguente.  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 L'ordinamento è basato su un confronto binario o un confronto testuale in base all'impostazione di `Option Compare`. Per ulteriori informazioni vedere [istruzione Option Compare](../../../../visual-basic/language-reference/statements/option-compare-statement.md).  
  
## <a name="comparing-objects"></a>Confronto tra oggetti  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Confronta due variabili di riferimento con un oggetto di [operatore Is](../../../../visual-basic/language-reference/operators/is-operator.md) e [operatore IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md). È possibile utilizzare uno di questi operatori per determinare se due variabili di riferimento fare riferimento alla stessa istanza dell'oggetto. Questa condizione è illustrata nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#65;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_1.vb)]  
  
 Nell'esempio precedente, `x Is y` restituisce `True`, in quanto entrambe le variabili fanno riferimento alla stessa istanza. Si confronti questo risultato con l'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#66;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_2.vb)]  
  
 Nell'esempio precedente, `x Is y` restituisce `False`, perché anche se le variabili di riferiscano a oggetti dello stesso tipo, fanno riferimento a istanze diverse di quel tipo.  
  
 Quando si desidera verificare per due oggetti non fa riferimento alla stessa istanza, il `IsNot` operatore consente di evitare una combinazione grammaticalmente impropria di `Not` e `Is`. Questa condizione è illustrata nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#67;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_3.vb)]  
  
 Nell'esempio precedente, `If a IsNot b` equivale a `If Not a Is b`.  
  
### <a name="comparing-object-type"></a>Confronto tra il tipo di oggetto  
 È possibile verificare se un oggetto è di un determinato tipo con il `TypeOf`... `Is` espressione. La sintassi è la seguente:  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 Quando `typename` specifica un tipo di interfaccia, il `TypeOf`... `Is` restituisce `True` se l'oggetto implementa il tipo di interfaccia. Quando `typename` è un tipo di classe, l'espressione restituisce `True` se l'oggetto è un'istanza della classe specificata o di una classe che deriva dalla classe specificata. Questa condizione è illustrata nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators&#68;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/comparison-operators_4.vb)]  
  
 Nell'esempio precedente, il `TypeOf x Is Control` espressione viene valutata `True` perché il tipo di `x` è `Button`, che eredita da `Control`.  
  
 Per ulteriori informazioni, vedere [operatore TypeOf](../../../../visual-basic/language-reference/operators/typeof-operator.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto di valori](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Operatori di confronto](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Operatori](../../../../visual-basic/language-reference/operators/index.md)   
 [Operatori aritmetici in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Operatori di concatenazione in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Operatori logici e bit per bit in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
