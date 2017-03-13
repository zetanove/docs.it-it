---
title: "Operatore false (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "false (parola chiave di operatore) [C#]"
ms.assetid: 81a888fd-011e-4589-b242-6c261fea505e
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Operatore false (Riferimenti per C#)
Restituisce il valore [bool](../../../csharp/language-reference/keywords/bool.md) `true` per indicare che un operando è `false` e restituisce `false` in caso contrario.  
  
 Prima di C\# 2.0, gli operatori `true` e `false` erano utilizzati per creare tipi di valore nullable definiti dall'utente, compatibile con tipi quali `SqlBool`.  Ora tuttavia Il linguaggio fornisce il supporto incorporato per i tipi di valore nullable e, ove possibile, è preferibile utilizzare tali tipi in sostituzione dell'overload degli operatori `true` e `false`.  Per ulteriori informazioni, vedere [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md).  
  
 Con valori booleani nullable, l'espressione `a != b` non è necessariamente uguale a `!(a == b)` poiché uno o entrambi i valori potrebbero essere null.  È necessario eseguire l'overload di entrambi gli operatori `true` e `false` separatamente per gestire correttamente i valori null nell'espressione.  Nell'esempio riportato di seguito viene illustrato come eseguire l'overload e utilizzare gli operatori `true` e `false`.  
  
 [!code-cs[csrefKeywordsOperator#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/false-operator_1.cs)]  
  
 È possibile utilizzare un tipo che esegue l'overload degli operatori `true` e `false`per l'espressione di controllo nelle istruzioni [if](../../../csharp/language-reference/keywords/if-else.md), [do](../../../csharp/language-reference/keywords/do.md), [while](../../../csharp/language-reference/keywords/while.md) e [for](../../../csharp/language-reference/keywords/for.md) nonché nelle [espressioni condizionali](../../../csharp/language-reference/operators/conditional-operator.md).  
  
 Se un tipo definisce l'operatore `false`, deve anche definire l'operatore [true](../../../csharp/language-reference/keywords/true.md).  
  
 Un tipo non può eseguire direttamente l'overload degli operatori logici condizionali [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) e [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md), ma è possibile ottenere un effetto equivalente eseguendo l'overload dei normali operatori logici e degli operatori `true` e `false`.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [true](../../../csharp/language-reference/keywords/true.md)