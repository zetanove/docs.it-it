---
title: "object (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "object_CSharpKeyword"
  - "object"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "object (parola chiave) [C#]"
ms.assetid: 93f60c0b-e17a-40a9-9362-cca5fb77b0e7
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# object (Riferimenti per C#)
Il tipo `object` è un alias dell'oggetto <xref:System.Object> in .NET Framework.  Nel sistema di tipi unificato di C\#, tutti i tipi, predefiniti e definiti dall'utente, tipi di riferimento e tipi di valore, ereditano direttamente o indirettamente da <xref:System.Object>.  Alle variabili di tipo `object` è possibile assegnare valori di qualsiasi tipo.  Una variabile di un tipo di valore convertita in oggetto viene definita *boxed*.  Una variabile di tipo object convertita in un tipo di valore viene definita *unboxed*.  Per ulteriori informazioni, vedere [Boxing e unboxing](../../../csharp/programming-guide/types/boxing-and-unboxing.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato che le variabili di tipo `object` possono accettare valori di qualsiasi tipo di dati e che le variabili di tipo `object` possono utilizzare i metodi su <xref:System.Object> di .NET Framework.  
  
 [!code-cs[csrefKeywordsTypes#16](../../../csharp/language-reference/keywords/codesnippet/csharp/object_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)