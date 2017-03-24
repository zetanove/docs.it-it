---
title: "Operatore - (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "-_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "- (operatore) [C#]"
  - "sottrazione (operatore) (-) [C#]"
ms.assetid: 4de7a4fa-c69d-48e6-aff1-3130af970b2d
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Operatore - (Riferimenti per C#)
L'operatore `-` può essere utilizzato come operatore unario o binario.  
  
## Note  
 Gli operatori `-` unari sono predefiniti per tutti i tipi numerici.  Il risultato di un'operazione `-` unaria su un tipo numerico corrisponde alla negazione numerica dell'operando.  
  
 Gli operatori `-` binari sono predefiniti per tutti i tipi numerici e di enumerazione per la sottrazione del secondo operando dal primo.  
  
 Anche i tipi delegati forniscono un operatore `-` binario, che esegue la rimozione dei delegati.  
  
 I tipi definiti dall'utente possono sottoporre a overload gli operatori `-` unari e gli operatori `-` binari.  Per ulteriori informazioni, vedere [operatore](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#40](../../../csharp/language-reference/operators/codesnippet/CSharp/subtraction-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)