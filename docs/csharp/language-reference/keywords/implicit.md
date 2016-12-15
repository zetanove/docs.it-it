---
title: "implicit (Riferimenti per C#) | Microsoft Docs"
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
  - "implicit"
  - "implicit_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "implicit (parola chiave) [C#]"
ms.assetid: 34db590e-eb3a-4f11-88d0-ffb3cd753dab
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# implicit (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `implicit` viene utilizzata per dichiarare un operatore di conversione implicita di tipi definita dall'utente.  È possibile utilizzarla per attivare le conversioni implicite tra un tipo definito dall'utente e un altro tipo, se è garantito che tale conversione non provochi una perdita di dati.  
  
## Esempio  
 [!code-cs[csrefKeywordsConversion#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/implicit_1.cs)]  
  
 Grazie all'eliminazione dei cast non necessari, le conversioni implicite contribuiscono a migliorare la leggibilità del codice sorgente.  Tuttavia, poiché per le conversioni implicite non è necessario eseguire il cast in modo esplicito da un tipo all'altro, è importante assicurarsi di non ottenere risultati imprevisti.  In generale, per poter essere utilizzati in modo sicuro senza il controllo del programmatore, gli operatori di conversione implicita non devono generare eccezioni né determinare perdite di dati.  Se un operatore di conversione non soddisfa questi requisiti, è opportuno contrassegnarlo come `explicit`.  Per ulteriori informazioni, vedere [Utilizzo degli operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [esplicita](../../../csharp/language-reference/keywords/explicit.md)   
 [operatore](../../../csharp/language-reference/keywords/operator.md)   
 [Procedura: implementare conversioni tra struct definite dall'utente](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)