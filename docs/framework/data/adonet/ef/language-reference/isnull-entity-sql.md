---
title: "ISNULL (Entity SQL) | Microsoft Docs"
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
ms.assetid: dc7a0173-3664-4c90-a57b-5cbb0a8ed7ee
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ISNULL (Entity SQL)
Consente di determinare se un'espressione di query è null.  
  
## Sintassi  
  
```  
  
expression IS [ NOT ] NULL  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione di query valida. Non può trattarsi di una raccolta, includere membri di una raccolta o essere un tipo di record con proprietà di un tipo di raccolta.  
  
 NOT  
 Nega il risultato EDM.Boolean di IS NULL.  
  
## Valore restituito  
 `true` se `expression` restituisce null; in caso contrario, `false`.  
  
## Note  
 Usare `IS NULL` per determinare se l'elemento di un outer join è null:  
  
```  
select c   
      from LOB.Customers as c left outer join LOB.Orders as o   
                              on c.ID = o.CustomerID    
      where o is not null and o.OrderQuantity = @x  
```  
  
 Usare `IS NULL` per determinare se un membro ha un valore effettivo:  
  
```  
select c from LOB.Customer as c where c.DOB is not null  
```  
  
 Nella tabella seguente viene illustrato il comportamento di `IS NULL` con alcuni modelli. Tutte le eccezioni vengono generate sul lato client prima che il provider venga richiamato:  
  
|Criterio|Comportamento|  
|--------------|-------------------|  
|null IS NULL|Restituisce `true`.|  
|TREAT \(null AS EntityType\) IS NULL|Restituisce `true`.|  
|TREAT \(null AS ComplexType\) IS NULL|Genera un errore.|  
|TREAT \(null AS RowType\) IS NULL|Genera un errore.|  
|EntityType IS NULL|Restituisce `true` o `false`.|  
|ComplexType IS NULL|Genera un errore.|  
|RowType IS NULL|Genera un errore.|  
  
## Esempio  
 Nella query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] seguente viene usato l'operatore IS NOT NULL per determinare se un'espressione di query non è null. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#ISNULL](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#isnull)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)