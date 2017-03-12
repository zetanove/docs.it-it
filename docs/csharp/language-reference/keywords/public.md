---
title: "public (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "public"
  - "public_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "public (parola chiave) [C#]"
ms.assetid: 0ae45d16-a551-4b74-9845-57208de1328e
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# public (Riferimenti per C#)
La parola chiave `public` è un modificatore di accesso per i tipi e i membri dei tipi.  L'accesso pubblico è il livello di accesso più permissivo.  Non vi è alcuna restrizione relativa all'accesso di membri pubblici, come illustrato nell'esempio riportato di seguito:  
  
```  
class SampleClass  
{  
    public int x; // No access restrictions.  
}  
```  
  
 Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md) e [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md).  
  
## Esempio  
 Nell'esempio riportato di seguito vengono dichiarate due classi: `PointTest` e `MainClass`.  È possibile accedere ai membri pubblici `x` e `y` di `PointTest` direttamente da `MainClass`.  
  
 [!code-cs[csrefKeywordsModifiers#13](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#13)]  
  
 Se si modifica il livello di accesso `public` in [private](../../../csharp/language-reference/keywords/private.md) o [protected](../../../csharp/language-reference/keywords/protected.md), verrà visualizzato il seguente messaggio di errore:  
  
 'PointTest.y' è inaccessibile a causa del livello di protezione.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [private](../../../csharp/language-reference/keywords/private.md)   
 [Protected](../../../csharp/language-reference/keywords/protected.md)   
 [interne](../../../csharp/language-reference/keywords/internal.md)