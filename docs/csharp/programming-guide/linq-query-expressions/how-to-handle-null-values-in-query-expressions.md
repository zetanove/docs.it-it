---
title: "Procedura: gestire valori null nelle espressioni di query (Guida per programmatori C#) | Microsoft Docs"
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
  - "valori null [LINQ in C#]"
  - "query [LINQ in C#], valori null"
  - "query (espressioni) [LINQ in C#], valori null"
ms.assetid: cb34f7a1-7ef5-466a-90ba-91da30ab525d
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: gestire valori null nelle espressioni di query (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In questo esempio viene illustrato come gestire i possibili valori null nelle raccolte di origine.  Una raccolta di oggetti quale <xref:System.Collections.Generic.IEnumerable%601> può contenere elementi il cui valore è [null](../../../csharp/language-reference/keywords/null.md).  Se una raccolta di origine è null o contiene un elemento il cui valore è null e la query non gestisce valori null, verrà generata un'eccezione <xref:System.NullReferenceException> quando si esegue la query.  
  
## Esempio  
 È possibile codificare in modo sicuro per evitare un'eccezione di riferimento null come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideLINQ#82](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-null-values-in-query-expressions_1.cs)]  
  
 Nell'esempio precedente la clausola `where` esclude tutti gli elementi null nella sequenza di categorie.  Questa tecnica è indipendente dal controllo null nella clausola join.  In questo esempio è possibile utilizzare l'espressione condizionale con null poiché `Products.CategoryID` è di tipo `int?`, ovvero una forma abbreviata di `Nullable<int>`.  
  
## Esempio  
 Se in una clausola join solo una delle chiavi di confronto è un tipo valore che ammette valori null, è possibile eseguire il cast della altre chiavi a un tipo che ammette valori null nell'espressione di query.  Nell'esempio seguente si supponga che `EmployeeID` sia una colonna contenente valori di tipo `int?`:  
  
 [!code-cs[csProgGuideLINQ#83](../../../csharp/programming-guide/arrays/codesnippet/CSharp/how-to-handle-null-values-in-query-expressions_2.cs)]  
  
## Vedere anche  
 <xref:System.Nullable%601>   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)