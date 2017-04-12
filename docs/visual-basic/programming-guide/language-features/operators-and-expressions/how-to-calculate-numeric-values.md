---
title: 'Procedura: calcolare valori numerici (Visual Basic) | Documenti di Microsoft'
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
- operator precedence
- operators [Visual Basic]
- expressions [Visual Basic], numeric
- calculations, numeric expressions
- precedence, of operators
- Visual Basic code, operators
- Visual Basic code, expressions
- numeric expressions
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: d844e2af3892d897125e21d3fd7047a8b295d10a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-calculate-numeric-values-visual-basic"></a>Procedura: calcolare valori numerici (Visual Basic)
È possibile calcolare valori numerici tramite l'utilizzo di espressioni numeriche. Oggetto *espressione numerica* è un'espressione che contiene i valori letterali, costanti e variabili che rappresentano valori numerici e operatori che agiscono su quei valori.  
  
## <a name="calculating-numeric-values"></a>Calcolo di valori numerici  
  
#### <a name="to-calculate-a-numeric-value"></a>Per calcolare un valore numerico  
  
-   Combinare uno o più valori letterali numerici, costanti e variabili in un'espressione numerica. L'esempio seguente mostra alcune espressioni numeriche valide.  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     Le prime tre righe mostrano un valore letterale, una costante e una variabile. Ognuno forma un'espressione numerica valida da sola. La riga finale Mostra una combinazione di una variabile con due valori letterali.  
  
     Si noti che un'espressione numerica non forma completa [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] istruzione da sola. È necessario utilizzare l'espressione come parte di un'istruzione completa.  
  
#### <a name="to-store-a-numeric-value"></a>Per archiviare un valore numerico  
  
-   È possibile utilizzare un'istruzione di assegnazione per assegnare il valore rappresentato da un'espressione numerica a una variabile, come illustrato nell'esempio seguente.  
  
     [!code-vb[VbVbalrOperators&#82;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_1.vb)]  
  
     Nell'esempio precedente, il valore dell'espressione sul lato destro dell'operatore uguale (`=`) viene assegnato alla variabile `j` sul lato sinistro dell'operatore, in modo `j` restituisce 276.  
  
     Per ulteriori informazioni, vedere [istruzioni](../../../../visual-basic/language-reference/statements/index.md).  
  
## <a name="multiple-operators"></a>Operatori multipli  
 Se l'espressione numerica contiene più di un operatore, l'ordine in cui vengono valutati è determinato dalle regole di precedenza degli operatori. Per ignorare le regole di precedenza degli operatori, racchiudere le espressioni tra parentesi, come illustrato nell'esempio precedente; le espressioni racchiuse tra parentesi vengono valutate per primi.  
  
#### <a name="to-override-normal-operator-precedence"></a>Per eseguire l'override di precedenza normale degli operatori  
  
-   Utilizzare le parentesi per racchiudere le operazioni che si desidera venga eseguita per prima. L'esempio seguente mostra due risultati diversi con lo stesso operandi e operatori.  
  
     [!code-vb[VbVbalrOperators&83;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_2.vb)]  
  
     Nell'esempio precedente, il calcolo per `j` esegue l'operatore di addizione (`+`) prima in quanto le parentesi che racchiudono `(67 + i)` eseguire l'override della precedenza normale e il valore assegnato a `j` corrisponde a 276 (4 volte 69). Il calcolo per `k` esegue gli operatori nella loro precedenza normale (`*` prima `+`) e il valore assegnato a `k` corrisponde a 270 (268 più 2).  
  
     Per ulteriori informazioni, vedere [precedenza tra operatori in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori ed espressioni](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Confronto di valori](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Istruzioni](../../../../visual-basic/language-reference/statements/index.md)   
 [Precedenza tra operatori in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Aritmetici (operatori)](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Combinazione efficace di operatori](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)
