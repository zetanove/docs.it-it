---
title: "IsFalse Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.isfalse"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "AndAlso operator"
  - "IsFalse operator"
ms.assetid: 37fc9dbf-e5cc-4570-b93f-7213447974df
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# IsFalse Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Determina se un'espressione è `False`.  
  
 Non è possibile chiamare `IsFalse` in modo esplicito nel codice, ma il compilatore Visual Basic può utilizzare tale operatore per generare codice dalle clausole `AndAlso`.  Se si definisce una classe o una struttura, quindi si utilizza una variabile di questo tipo in una clausola `AndAlso`, è necessario definire `IsFalse` su tale classe o struttura.  
  
 Il compilatore considera gli operatori `IsFalse` e `IsTrue` come *coppia associata*.  Questo significa che, se si definisce uno degli operatori, è necessario definire anche l'altro.  
  
> [!NOTE]
>  L'operatore `IsFalse` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando presenta il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono definite le caratteristiche di una struttura che include le definizioni per gli operatori `IsFalse` e `IsTrue`.  
  
 [!code-vb[VbVbalrOperators#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/isfalse-operator_1.vb)]  
  
## Vedere anche  
 [IsTrue Operator](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [How to: Define an Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [AndAlso Operator](../../../visual-basic/language-reference/operators/andalso-operator.md)