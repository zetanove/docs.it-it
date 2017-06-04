---
title: "BETWEEN (Entity SQL) | Microsoft Docs"
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
ms.assetid: 4dcdd754-ae01-4e78-bf28-8a117fb2b73e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# BETWEEN (Entity SQL)
Determina se un'espressione restituisce un valore incluso in un intervallo specificato. L'espressione BETWEEN [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ha la stessa funzione dell'espressione BETWEEN Transact\-SQL.  
  
## Sintassi  
  
```  
  
expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione valida da testare nell'intervallo definito da `begin_expression` e `end_expression`.`expression` deve essere dello stesso tipo sia di `begin_expression` che di `end_expression`.  
  
 `begin_expression`  
 Qualsiasi espressione valida.`begin_expression` deve essere dello stesso tipo sia di `expression` che di `end_expression`.`begin_expression` deve essere minore di `end_expression`; in caso contrario, il valore restituito sarà negativo.  
  
 `end_expression`  
 Qualsiasi espressione valida.`end_expression` deve essere dello stesso tipo sia di `expression` che di `begin_expression`.  
  
 NOT  
 Specifica la negazione del risultato di BETWEEN.  
  
 AND  
 Segnaposto che indica che l'oggetto `expression` deve essere incluso nell'intervallo specificato da `begin_expression` e `end_expression`.  
  
## Valore restituito  
 `true` se `expression` si trova tra l'intervallo indicato da `begin_expression` e `end_expression`; in caso contrario, `false`. Verrà restituito `null` se `expression` è `null` o se `begin_expression` o `end_expression` è `null`.  
  
## Note  
 Per specificare un intervallo esclusivo, usare gli operatori "maggiore di" \(\>\) e "minore di" \(\<\), anziché BETWEEN.  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore BETWEEN per determinare se un'espressione restituisce un valore incluso in un intervallo specificato. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#BETWEEN](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#between)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)