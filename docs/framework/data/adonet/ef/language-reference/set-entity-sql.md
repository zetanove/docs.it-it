---
title: "SET (Entity SQL) | Microsoft Docs"
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
ms.assetid: 28b4deac-c7e4-4f09-b428-4d352ef2dc94
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# SET (Entity SQL)
L'espressione SET viene usata per convertire una raccolta di oggetti in un set restituendo una nuova raccolta da cui sono stati rimossi tutti i duplicati.  
  
## Sintassi  
  
```  
  
SET (expression)  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione di query valida che restituisce una raccolta.  
  
## Note  
 L'espressione set `SET(c)` equivale, dal punto di vista logico,  all'istruzione Select seguente:  
  
```  
SELECT VALUE DISTINCT c FROM c  
```  
  
 `SET` è uno degli operatori sui set di [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Tutti gli operatori sui set di [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono valutati da sinistra a destra. Per informazioni sulla priorità degli operatori sui set di [EXCEPT](../../../../../../docs/framework/data/adonet/ef/language-reference/except-entity-sql.md), vedere [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## Esempio  
 Nella query Entity SQL seguente viene usata l'espressione SET per convertire una raccolta di oggetti in un set. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#SET](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#set)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)