---
title: "parziale (Tipo) (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "partialtype"
  - "partialtype_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "tipi parziali [C#]"
ms.assetid: 27320743-a22e-4c7b-b0b3-53afe3607334
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# parziale (Tipo) (Riferimenti per C#)
Le definizioni di tipi parziali consentono la suddivisione in più file della definizione di una classe, una struttura o un'interfaccia.  
  
 In File1.cs:  
  
 [!code-cs[csrefKeywordsContextual#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/partial-type_1.cs)]  
  
 In File2.cs la dichiarazione:  
  
 [!code-cs[csrefKeywordsContextual#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/partial-type_2.cs)]  
  
## Note  
 La suddivisione di un tipo di classe, struttura o interfaccia in più file può essere utile per progetti di grandi dimensioni o quando si utilizza codice generato automaticamente come quello fornito da [Windows Forms Designer](http://msdn.microsoft.com/it-it/3c3d61f8-f36c-4d41-b9c3-398376fabb15).  Un tipo parziale può contenere un [metodo parziale](../../../csharp/language-reference/keywords/partial-method.md).  Per ulteriori informazioni, vedere [Classi e metodi parziali](../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)