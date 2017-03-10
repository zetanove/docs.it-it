---
title: "Operatore / (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/ (operatore) [C#]"
  - "operatore di divisione [C#]"
ms.assetid: d155e496-678f-4efa-bebe-2bd08da2c5af
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# Operatore / (Riferimenti per C#)
L'operatore di divisione \(`/`\) Divide il primo operando dal secondo operando.  Tutti i tipi numerici hanno operatori di divisione già definiti.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `/`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Un overload dell'operatore `/`esegue in modo implicito l'overload dell'[operatore \/\=](../../../csharp/language-reference/operators/subtraction-assignment-operator.md).  
  
 Quando si dividono due numeri interi, il risultato è sempre un numero intero.  Ad esempio, il risultato di 7 \/ 3 è 2.  Per determinare la parte restante del 7 \/ 3, utilizzare l'operatore di resto \([%](../../../csharp/language-reference/operators/modulus-operator.md)\).  Per ottenere un quoziente come numero razionale o frazione, assegnare al dividendo o al divisore il tipo `float` o `double`.  Se è necessario esprimere il dividendo o il divisore come numero decimale inserendo una cifra a destra del separatore decimale, come illustrato nell'esempio riportato di seguito, è possibile assegnare in modo implicito il tipo.  
  
## Esempio  
 [!code-cs[csRefOperators#42](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#42)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)