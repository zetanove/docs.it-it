---
title: Precedenza tra operatori in Visual Basic | Documenti di Microsoft
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
- arithmetic operators, precedence
- operator precedence
- logical operators, precedence
- operators [Visual Basic], associativity
- operators [Visual Basic], resolution
- associativity of operators
- operators [Visual Basic], precedence
- precedence, of operators
- comparison operators, precedence
- math operators
- order of precedence
ms.assetid: cbbdb282-f572-458e-a520-008a675f8063
caps.latest.revision: 18
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
ms.openlocfilehash: 6532fc0c26db3b736c863be075571570a3d25eef
ms.lasthandoff: 03/13/2017

---
# <a name="operator-precedence-in-visual-basic"></a>Precedenza tra gli operatori in Visual Basic
Quando vengono eseguite diverse operazioni in un'espressione, ogni parte viene valutata e risolta in un ordine predeterminato definito *precedenza degli operatori*.  
  
## <a name="precedence-rules"></a>Regole di precedenza  
 Se un'espressione contiene operatori da più di una categoria, vengono valutati in base alle regole seguenti:  
  
-   Gli operatori aritmetici e di concatenazione hanno l'ordine di precedenza descritta nella sezione seguente, e hanno maggiore precedenza rispetto a confronto, logici e bit per bit.  
  
-   Tutti gli operatori di confronto hanno la stessa precedenza e tutti hanno la precedenza maggiore rispetto agli operatori logici e bit per bit, ma una precedenza più bassa rispetto agli operatori aritmetici e di concatenazione.  
  
-   Gli operatori logici e bit per bit di ordine di precedenza descritta nella sezione seguente e tutti gli aritmetica, di concatenazione e gli operatori di confronto.  
  
-   Gli operatori con uguale precedenza vengono valutati da sinistra a destra nell'ordine in cui appaiono nell'espressione.  
  
## <a name="precedence-order"></a>Ordine di precedenza  
 Gli operatori vengono valutati nell'ordine di precedenza seguente:  
  
### <a name="await-operator"></a>Operatore Await  
 Await  
  
### <a name="arithmetic-and-concatenation-operators"></a>Operazioni aritmetiche e concatenazione (operatori)  
 Elevamento a potenza (`^`)  
  
 Unario identità e negazione (`+`, `–`)  
  
 Moltiplicazione e divisione a virgola mobile (`*`, `/`)  
  
 Divisione di interi (`\`)  
  
 Il modulo aritmetico (`Mod`)  
  
 Addizione e sottrazione (`+`, `–`)  
  
 Concatenazione di stringhe (`&`)  
  
 Bit aritmetico (`<<`, `>>`)  
  
### <a name="comparison-operators"></a>Operatori di confronto  
 All comparison operators (`=`, `<>`, `<`, `<=`, `>`, `>=`, `Is`, `IsNot`, `Like`, `TypeOf`... `Is`)  
  
### <a name="logical-and-bitwise-operators"></a>Operatori logici e bit per bit  
 Negazione (`Not`)  
  
 Insieme (`And`, `AndAlso`)  
  
 Disgiunzione (`Or`, `OrElse`)  
  
 Disgiunzione (`Xor`)  
  
### <a name="comments"></a>Commenti  
 Il `=` operatore è solo l'operatore di confronto uguaglianza, non l'operatore di assegnazione.  
  
 L'operatore di concatenazione di stringhe (`&`) non è un operatore aritmetico, ma in precedenza si è raggruppato con gli operatori aritmetici.  
  
 Il `Is` e `IsNot` gli operatori sono operatori di confronto di riferimento di oggetto. Essi non confrontare i valori di due oggetti. si verifica solo per determinare se due variabili oggetto fanno riferimento alla stessa istanza dell'oggetto.  
  
## <a name="associativity"></a>Associazione  
 Quando gli operatori uguale precedenza vengono visualizzati insieme in un'espressione, ad esempio una moltiplicazione e divisione, il compilatore valuta ogni operazione che viene rilevato da sinistra a destra. Questa condizione è illustrata nell'esempio seguente.  
  
```  
Dim n1 As Integer = 96 / 8 / 4  
Dim n2 As Integer = (96 / 8) / 4  
Dim n3 As Integer = 96 / (8 / 4)  
```  
  
 La prima espressione valuta la divisione 96 / 8 (che restituisce 12) e quindi la divisione 12 / 4, che restituisce 3. Poiché il compilatore valuta le operazioni per `n1` da sinistra a destra, la valutazione è lo stesso quando quest'ordine è indicato in modo esplicito per `n2`. Entrambi `n1` e `n2` avranno come risultato&3;. Al contrario, `n3` il risultato di 48, perché le parentesi forzano il compilatore può valutare 8 / 4 prima.  
  
 Questo comportamento, gli operatori sono definiti a *associazione all'operando sinistro* in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## <a name="overriding-precedence-and-associativity"></a>Si esegue l'override di precedenza e associatività  
 È possibile utilizzare parentesi per forzare alcune parti di un'espressione da valutare prima degli altri. Questo consente di ignorare l'ordine di precedenza sia l'associazione a sinistra. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]esegue sempre le operazioni che sono racchiusi tra parentesi prima di quelli all'esterno. Tuttavia, all'interno delle parentesi, viene mantenuta la precedenza e associatività, a meno che non si usano le parentesi all'interno delle parentesi. Questa condizione è illustrata nell'esempio seguente.  
  
```  
Dim a, b, c, d, e, f, g As Double  
a = 8.0  
b = 3.0  
c = 4.0  
d = 2.0  
e = 1.0  
f = a - b + c / d * e  
' The preceding line sets f to 7.0. Because of natural operator   
' precedence and associativity, it is exactly equivalent to the   
' following line.  
f = (a - b) + ((c / d) * e)  
' The following line overrides the natural operator precedence   
' and left associativity.  
g = (a - (b + c)) / (d * e)  
' The preceding line sets g to 0.5.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [= Operatore](../../../visual-basic/language-reference/operators/assignment-operator.md)   
 [Is (operatore)](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot (operatore)](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [LIKE (operatore)](../../../visual-basic/language-reference/operators/like-operator.md)   
 [Operatore TypeOf](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [Await (operatore)](../../../visual-basic/language-reference/operators/await-operator.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operatori ed espressioni](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
