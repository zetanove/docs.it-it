---
title: "Operatore + (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "+_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "+ (operatore) [C#]"
  - "operatore di addizione [C#]"
  - "operatore di concatenazione [C#]"
ms.assetid: 93e56486-bb42-43c1-bd43-60af11e64e67
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Operatore + (Riferimenti per C#)
L'operatore `+` può essere utilizzato come operatore unario o binario.  
  
## Note  
 Gli operatori `+` unari sono predefiniti per tutti i tipi numerici.  Il risultato di un'operazione `+` unaria su un tipo numerico corrisponde al valore dell'operando.  
  
 Gli operatori `+` binari sono predefiniti per i tipi numerici e tipi stringa.  Per i tipi numerici, l'operatore \+ calcola la somma dei due operandi.  Quando entrambi gli operandi sono di tipo stringa, l'operatore \+ concatena le rappresentazioni in formato stringa degli operandi.  
  
 Anche i tipi delegati forniscono un operatore `+` binario, che esegue la concatenazione dei delegati.  
  
 I tipi definiti dall'utente possono sottoporre a overload gli operatori `+` unari e gli operatori `+` binari.  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  Per ulteriori informazioni, vedere [operatore](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#28](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#28)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [operatore](../../../csharp/language-reference/keywords/operator.md)