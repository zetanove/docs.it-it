---
title: "as (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "as_CSharpKeyword"
  - "as"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "as (parola chiave) [C#]"
  - "conversione di tipi [C#], as (parola chiave)"
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# as (Riferimenti per C#)
È possibile utilizzare l'operatore di `as` per eseguire determinati tipi di conversioni tra tipi compatibili riferimenti o [tipi nullable](../../../csharp/programming-guide/nullable-types/index.md).  Il codice che segue fornisce un esempio in proposito.  
  
 [!code-cs[csrefKeywordsOperator#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_1.cs)]  
  
## Note  
 L'operatore `as` è simile a un'operazione cast.  Tuttavia, se la conversione non è possibile, `as` restituisce `null` anziché generare un'eccezione.  Si consideri l'esempio seguente:  
  
```  
expression as type  
```  
  
 Il codice è equivalente alla seguente espressione con la differenza che la variabile di `expression` viene valutata solo una volta.  
  
```  
expression is type ? (type)expression : (type)null  
```  
  
 Si noti che l'operatore di `as` esegue solo le conversioni dei riferimenti, le conversioni nullable e le conversioni boxing.  L'operatore di `as` non può eseguire altre conversioni, come conversioni definite dall'utente, che devono invece essere eseguite utilizzando espressioni cast.  
  
## Esempio  
 [!code-cs[csrefKeywordsOperator#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Operatore ?:](../../../csharp/language-reference/operators/conditional-operator.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)