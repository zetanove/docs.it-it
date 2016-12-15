---
title: "Operatore ?: (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "?:_CSharpKeyword"
  - "?_CSharpKeyword"
  - ":_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "?: (operatore) [C#]"
  - "condizionale (operatore) (?:) [C#]"
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
caps.latest.revision: 23
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore ?: (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'operatore condizionale \(`?:`\) restituisce uno tra due valori in base al valore di un'espressione booleana.  Di seguito è riportata la sintassi per l'operatore condizionale.  
  
```  
condition ? first_expression : second_expression;  
```  
  
## Note  
 L' oggetto `condition` deve restituire `true` o `false`.  Se `condition` è `true`, `first_expression` viene valutato e diventa il risultato.  Se `condition` è `false`, `second_expression` viene valutato e diventa il risultato.  Viene valutata soltanto una delle due espressioni.  
  
 Il tipo di `first_expression` e di `second_expression` deve essere lo stesso o deve esistere una conversione implicita da un tipo a un altro.  
  
 I calcoli che richiedono una costruzione `if-else` possono essere espressi più concisamente mediante l'operatore condizionale.  Ad esempio, il codice seguente viene utilizzato prima un'istruzione `if`, quindi un operatore condizionale per classificare un integer come positivo o negativo.  
  
```  
  
int input = Convert.ToInt32(Console.ReadLine());  
string classify;  
  
// if-else construction.  
if (input > 0)  
    classify = "positive";  
else  
    classify = "negative";  
  
// ?: conditional operator.  
classify = (input > 0) ? "positive" : "negative";  
  
```  
  
 L'operatore condizionale si associa all'operando a destra.  L'espressione `a ? b : c ? d : e` viene valutata come `a ? b : (c ? d : e)`, non come `(a ? b : c) ? d : e`.  
  
 Non è possibile eseguire l'overload dell'operatore condizionale.  
  
## Esempio  
 [!code-cs[csRefOperators#41](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [if\-else](../../../csharp/language-reference/keywords/if-else.md)