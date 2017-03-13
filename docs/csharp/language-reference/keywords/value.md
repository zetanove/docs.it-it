---
title: "value (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "value_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "value (parola chiave) [C#]"
ms.assetid: c99d6468-687f-4a46-89b4-a95e1b00bf6d
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# value (Riferimenti per C#)
La parola chiave contestuale `value` viene utilizzata nella funzione di accesso set nelle dichiarazioni di proprietà ordinarie.  È simile a un parametro di input in un metodo.  La parola `value` fa riferimento al valore che il codice client sta tentando di assegnare alla proprietà.  Nell'esempio seguente `MyDerivedClass` dispone di una proprietà chiamata `Name` che utilizza il parametro `value` per assegnare una nuova stringa al campo sottostante `name`.  Dal punto di vista del codice client, l'operazione è scritta come una semplice assegnazione.  
  
 [!code-cs[csrefKeywordsModifiers#26](../../../csharp/language-reference/keywords/codesnippet/CSharp/value_1.cs)]  
  
 Per ulteriori informazioni sull'utilizzo di `value`, vedere [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)