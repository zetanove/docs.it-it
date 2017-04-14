---
title: "THEN (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
ms.assetid: 54222642-23c6-4f61-9861-67caca53ac5f
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# THEN (Entity SQL)
Risultato di una clausola WHEN quando restituisce `true`.  
  
## Sintassi  
  
```  
  
WHEN when_expression THEN then_expression  
```  
  
## Argomenti  
 `when_expression`  
 Qualsiasi espressione booleana valida.  
  
 `then_expression`  
 Qualsiasi espressione di query valida che restituisce una raccolta.  
  
## Note  
 Se `when_expression` restituisce il valore `true`, il risultato è l'oggetto `then-expression` corrispondente. Se nessuna delle condizioni WHEN è soddisfatta, viene restituito `else-expression`. Se, tuttavia, non sono presenti `else-expression`, il risultato è null.  
  
 Per un esempio, vedere [CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md).  
  
## Esempio  
 Nella query Entity SQL seguente viene usata l'espressione CASE per valutare un set di espressioni `Boolean`. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#CASE_WHEN_THEN_ELSE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#case_when_then_else)]  
  
## Vedere anche  
 [CASE](../../../../../../docs/framework/data/adonet/ef/language-reference/case-entity-sql.md)   
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)