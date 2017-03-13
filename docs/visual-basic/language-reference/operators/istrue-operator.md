---
title: "IsTrue Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.istrue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IsTrue operator"
  - "OrElse operator [Visual Basic]"
ms.assetid: b6cec0f2-61b1-4331-a7f0-4d07ee3179d6
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# IsTrue Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Determina se un'espressione è `True`.  
  
 Non è possibile chiamare `IsTrue` in modo esplicito nel codice, ma il compilatore Visual Basic può utilizzare tale operatore per generare codice dalle clausole `OrElse`.  Se si definisce una classe o una struttura, quindi si utilizza una variabile di questo tipo in una clausola `OrElse`, è necessario definire `IsTrue` su tale classe o struttura.  
  
 Il compilatore considera gli operatori `IsTrue` e `IsFalse` come *coppia associata*.  Questo significa che, se si definisce uno degli operatori, è necessario definire anche l'altro.  
  
## Utilizzo di IsTrue da parte del compilatore  
 Dopo aver definito una classe o una struttura, è possibile utilizzare una variabile del tipo specificato in un'istruzione `For`, `If`, `Else` `If` o `While` o in una clausola `When`.  Se si esegue questa operazione, è necessario per il compilatore un operatore che converta il tipo in un valore `Boolean`, in modo da consentire il test di una condizione.  La ricerca di un operatore appropriato viene svolta nel seguente ordine:  
  
1.  Un operatore di conversione verso un tipo di dati più grande dalla classe o dalla struttura in `Boolean`.  
  
2.  Un operatore di conversione verso un tipo di dati più grande dalla classe o dalla struttura in `Boolean?`.  
  
3.  L'operatore `IsTrue` sulla classe o sulla struttura.  
  
4.  Una conversione verso un tipo di dati più piccolo a `Boolean?` che non comprende una conversione da `Boolean` a `Boolean?`.  
  
5.  Un operatore di conversione verso un tipo di dati più piccolo dalla classe o dalla struttura in `Boolean`.  
  
 Se non sono stati definiti né una conversione in `Boolean` né un operatore `IsTrue`, verrà segnalato un errore.  
  
> [!NOTE]
>  L'operatore `IsTrue` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando presenta il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono definite le caratteristiche di una struttura che include le definizioni per gli operatori `IsFalse` e `IsTrue`.  
  
 [!code-vb[VbVbalrOperators#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/istrue-operator_1.vb)]  
  
## Vedere anche  
 [IsFalse Operator](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [OrElse Operator](../../../visual-basic/language-reference/operators/orelse-operator.md)