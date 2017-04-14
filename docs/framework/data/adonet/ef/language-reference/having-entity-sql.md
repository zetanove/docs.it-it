---
title: "HAVING (Entity SQL) | Microsoft Docs"
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
ms.assetid: b5d52d97-8372-4335-beac-2d0b79dc3707
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# HAVING (Entity SQL)
Specifica una condizione di ricerca per un gruppo o un'aggregazione.  
  
## Sintassi  
  
```  
  
[ HAVING search_condition ]  
```  
  
## Argomenti  
 `search_condition`  
 Specifica la condizione di ricerca che il gruppo o l'aggregazione deve soddisfare. Se viene usata assieme alla clausola GROUP BY ALL, la clausola HAVING è prioritaria rispetto a ALL.  
  
## Note  
 La clausola HAVING viene usata per specificare una condizione di filtro aggiuntiva sul risultato di un raggruppamento. Se non viene specificata alcuna clausola GROUP BY nell'espressione di query, viene presupposto un gruppo con singolo set implicito.  
  
> [!NOTE]
>  La clausola HAVING può essere usata solo con l'istruzione [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md). Se la clausola [GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md) non viene usata, la funzionalità della clausola HAVING corrisponde a quella di una clausola WHERE.  
  
 La clausola HAVING funziona come la clausola WHERE eccetto per il fatto che viene applicata dopo l'operazione GROUP BY. Questo significa che la clausola HAVING può fare riferimento solo alle aggregazioni e agli alias di raggruppamento, come illustrato nell'esempio seguente.  
  
```  
SELECT Name, SUM(o.Price * o.Quantity) AS Total FROM orderLines AS o GROUP BY o.Product AS Name  
HAVING SUM(o.Quantity) > 1  
```  
  
 L'esempio precedente consente di limitare i gruppi esclusivamente a quelli che includono più di un prodotto.  
  
## Esempio  
 Nella query Entity SQL seguente vengono usati gli operatori HAVING e GROUP BY per specificare una condizione di ricerca per un gruppo o un'aggregazione. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecutePrimitiveTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#HAVING](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#having)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Espressioni di query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)