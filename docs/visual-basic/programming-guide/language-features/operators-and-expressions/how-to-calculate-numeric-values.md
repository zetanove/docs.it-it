---
title: "How to: Calculate Numeric Values (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operator precedence"
  - "operators [Visual Basic]"
  - "expressions [Visual Basic], numeric"
  - "calculations, numeric expressions"
  - "precedence, of operators"
  - "Visual Basic code, operators"
  - "Visual Basic code, expressions"
  - "numeric expressions"
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# How to: Calculate Numeric Values (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile calcolare i valori numeri tramite l'uso di espressioni numeriche.  Per *espressione numerica* è un'espressione contenente valori letterali, costanti e variabili che rappresentano valori numerici e operatori che agiscono su quei valori.  
  
## Calcolo di valori numerici  
  
#### Per calcolare un valore numerico  
  
-   Combinare uno o più valori letterali numerici, costanti e variabili in un'espressione numerica.  Nell'esempio riportato di seguito vengono illustrate alcune espressioni numeriche valide.  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     Nelle prime tre righe sono illustrati un valore letterale, una costante e una variabile.  Ognuno forma un'espressione numerica valida da sola.  Nella riga finale viene illustrata una combinazione di una variabile con due valori letterali.  
  
     Si noti che un'espressione numerica non forma un'istruzione di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]completa da sola.  È necessario utilizzare l'espressione come parte di un'istruzione completa.  
  
#### Per memorizzare un valore numerico  
  
-   È possibile utilizzare un'istruzione di assegnazione per assegnare il valore rappresentato da un'espressione numerica a una variabile, come dimostrato nell'esempio riportato di seguito.  
  
     [!code-vb[VbVbalrOperators#82](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_1.vb)]  
  
     Nell'esempio riportato in precedenza, il valore dell'espressione a destra dell'operatore uguale \(`=`\) viene assegnato a una variabile `j` a sinistra dell'operatore, quindi `j` restituisce 276.  
  
     Per ulteriori informazioni, vedere [Statements](../../../../visual-basic/language-reference/statements/index.md).  
  
## Operatori multipli  
 Se l'espressione numerica contiene più di un operatore, l'ordine con cui essi vengono valutati è determinato dalle regole di precedenza tra gli operatori.  Per eseguire l'override delle regole di precedenza degli operatori, racchiudere le espressioni tra parentesi, come nell'esempio illustrato di seguito; le espressioni racchiuse tra parentesi vengono valutate per prime.  
  
#### Per eseguire l'override della normale precedenza tra gli operatori  
  
-   Utilizzare le parentesi per racchiudere le operazioni che si desidera eseguire per prime.  Nell'esempio seguente vengono illustrati due risultati diversi con gli stessi operandi e operatori.  
  
     [!code-vb[VbVbalrOperators#83](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-calculate-numeric-values_2.vb)]  
  
     Nell'esempio riportato in precedenza, il calcolo di `j` esegue l'operazione di addizione \(`+`\) per prima in quanto le parentesi attorno a `(67 + i)` eseguono l'override della precedenza normale e il valore assegnato a `j` corrisponde a 276 \(4 volte 69\).  Il calcolo di `k` esegue gli operatori nella loro precedenza normale \(`*` prima di `+`\) e il valore assegnato a`k` corrisponde a 270 \(268 più 2\).  
  
     Per ulteriori informazioni, vedere [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md).  
  
## Vedere anche  
 [Operators and Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Statements](../../../../visual-basic/language-reference/statements/index.md)   
 [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Arithmetic Operators](../../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Efficient Combination of Operators](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)