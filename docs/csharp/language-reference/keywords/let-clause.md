---
title: "Clausola let (Riferimento C#) | Microsoft Docs"
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
  - "let_CSharpKeyword"
  - "let"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "let (clausola) [C#]"
  - "parola chiave let [C#]"
ms.assetid: 13c9c1a4-ce57-48ef-8e1b-4c2a59b99fb4
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Clausola let (Riferimento C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In un'espressione di query, è talvolta utile archiviare il risultato di una sottoespressione al fine di utilizzarlo nelle clausole successive.  È possibile eseguire questa operazione con la parola chiave `let` che crea una nuova variabile di intervallo e la inizializza con il risultato dell'espressione fornita.  Dopo l'inizializzazione con un valore, la variabile di intervallo non può essere utilizzata per archiviare un altro valore.  Tuttavia la variabile di intervallo può essere sottoposta a query, se contiene un tipo che può essere sottoposto a query.  
  
## Esempio  
 Nell'esempio riportato di seguito `let` viene utilizzato in due modi:  
  
1.  Per creare un tipo enumerabile che può essere sottoposto a query.  
  
2.  Per consentire alla query di chiamare `ToLower` solo una volta sulla variabile di intervallo `word`.  Senza utilizzare `let`, si dovrebbe chiamare `ToLower` in ogni predicato nella clausola `where`.  
  
 [!code-cs[cscsrefQueryKeywords#28](../../../csharp/language-reference/keywords/codesnippet/CSharp/let-clause_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Procedura: gestire le eccezioni nelle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)