---
title: "Operatore ~ (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "~_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "~ [C#], operatore di complemento bit per bit"
  - "~ (operatore) [C#]"
  - "operatore di complemento bit per bit [C#]"
  - "tilde (~) (operatore di complemento di uno) [C#]"
ms.assetid: 11bc078a-50e2-4d7e-9896-67ef669dc602
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Operatore ~ (Riferimenti per C#)
L'operatore `~` esegue un'operazione di complemento bit per bit sull'operando, con l'effetto di invertire ogni bit.  Gli operatori di complemento bit per bit sono predefiniti per [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md) e [ulong](../../../csharp/language-reference/keywords/ulong.md).  
  
> [!NOTE]
>  Il simbolo `~` viene anche utilizzato per dichiarare i distruttori.  Per ulteriori informazioni, vedere [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md).  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `~` .  Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#25](../../../csharp/language-reference/operators/codesnippet/CSharp/bitwise-complement-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)