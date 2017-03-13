---
title: "protected (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "protected"
  - "protected_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "protected (parola chiave) [C#]"
ms.assetid: 05ce3794-6675-4025-bddb-eaaa0ec22892
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# protected (Riferimenti per C#)
La parola chiave `protected` è un modificatore di accesso per membri.  Un membro protetto è accessibile all'interno della classe relativa e dalle istanze di classe derivate.  Per un confronto tra il modificatore d'accesso `protected` e gli altri modificatori di accesso, vedere [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md).  
  
## Esempio  
 Un membro protetto di una classe base è accessibile in una classe derivata solo se l'accesso viene eseguito attraverso il tipo della classe derivata.  Si consideri, ad esempio, il seguente segmento di codice:  
  
 [!code-cs[csrefKeywordsModifiers#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/protected_1.cs)]  
  
 L'istruzione `a.x = 10` genera un errore perché utilizzata all'interno del metodo Main statico e non in un'istanza della classe B.  
  
 I membri della struttura non possono essere protetti perché una struttura non può essere ereditata.  
  
## Esempio  
 In questo esempio, la classe `DerivedPoint` è derivata da `Point`.  Pertanto sarà possibile accedere ai membri protetti della classe base direttamente dalla classe derivata.  
  
 [!code-cs[csrefKeywordsModifiers#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/protected_2.cs)]  
  
 Se si modificano i livelli di accesso di `x` e `y` impostandoli su [private](../../../csharp/language-reference/keywords/private.md), in fase di compilazione verranno generati i seguenti messaggi di errore:  
  
 `'Point.y' is inaccessible due to its protection level.`  
  
 `'Point.x' is inaccessible due to its protection level.`  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)