---
title: "is (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "is_CSharpKeyword"
  - "is"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "is (parola chiave) [C#]"
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# is (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Controlla se un oggetto è compatibile con un determinato tipo.  Ad esempio, il codice seguente può determinare se un oggetto è un'istanza del tipo `MyObject` o un tipo che deriva da `MyObject`:  
  
```  
if (obj is MyObject)  
{  
}  
```  
  
 Un'espressione `is` restituisce `true` se l'espressione fornita non è null e l'oggetto fornito può essere sottoposto a cast sul tipo fornito senza generare un'eccezione.  
  
 La parola chiave `is` causa un avviso in fase di compilazione se l'espressione è sempre `true` oppure `false`, ma in genere valuta la compatibilità dei tipi in fase di esecuzione.  
  
 Non è possibile sottoporre l'operatore `is` a overload.  
  
 È possibile utilizzare l'operatore `is` soltanto con le conversioni dei riferimenti, le conversioni boxing e le conversioni unboxing.  Altre conversioni, ad esempio quelle definite dall'utente, non sono considerate.  
  
 Non è possibile utilizzare metodi anonimi sul lato sinistro dell'operatore `is`.  Questa eccezione include le espressioni lambda.  
  
## Esempio  
 [!code-cs[csrefKeywordsOperator#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/is_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)