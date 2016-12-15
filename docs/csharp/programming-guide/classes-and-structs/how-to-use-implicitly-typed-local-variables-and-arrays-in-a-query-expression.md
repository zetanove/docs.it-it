---
title: "Procedura: utilizzare variabili e matrici locali tipizzate in modo implicito in un&#39;espressione di query (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "variabili locali tipizzate in modo implicito [C#], modalità di utilizzo"
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: utilizzare variabili e matrici locali tipizzate in modo implicito in un&#39;espressione di query (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare le variabili locali tipizzate in modo implicito ogni volta che si desidera determinare il tipo di una variabile locale tramite il compilatore.  È necessario utilizzare variabili locali tipizzate in modo implicito per archiviare i tipi anonimi, che vengono spesso utilizzati nelle espressioni di query.  Negli esempi seguenti vengono illustrati sia l'utilizzo facoltativo che quello obbligatorio delle variabili locali tipizzate in modo implicito nelle query.  
  
 Le variabili locali tipizzate in modo implicito vengono dichiarate utilizzando la parola chiave contestuale [var](../../../csharp/language-reference/keywords/var.md).  Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md) e [Matrici tipizzate in modo implicito](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato uno scenario comune in cui la parola chiave `var` è obbligatoria: un'espressione di query che produce una sequenza di tipi anonimi.  In questo scenario, sia la variabile di query che la variabile di iterazione nell'istruzione `foreach` devono essere tipizzate in modo implicito utilizzando `var`, poiché non si dispone dell'accesso a un nome di tipo per il tipo anonimo.  Per ulteriori informazioni sui tipi anonimi, vedere [Tipi anonimi](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
 [!code-cs[csProgGuideLINQ#32](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la parola chiave `var` in una situazione simile, ma in cui l'utilizzo di `var` è facoltativo.  Poiché `student.LastName` è una stringa, l'esecuzione della query restituisce una sequenza di stringhe.  Il tipo di `queryID` potrebbe pertanto essere dichiarato come `System.Collections.Generic.IEnumerable<string>` invece di `var`.  La parola chiave `var` viene utilizzata per praticità.  Nell'esempio la variabile di iterazione nell'istruzione `foreach` è tipizzata in modo esplicito come stringa, ma potrebbe invece essere dichiarata utilizzando `var`.  Poiché il tipo della variabile di iterazione non è un tipo anonimo, l'utilizzo di `var` è facoltativo e non obbligatorio.  Tenere presente che `var` non è un tipo, ma un'istruzione per il compilatore affinché vengano eseguite l'inferenza e l'assegnazione del tipo.  
  
 [!code-cs[csProgGuideLINQ#33](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi di estensione](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [var](../../../csharp/language-reference/keywords/var.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)