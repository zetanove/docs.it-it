---
title: "Paging (Entity SQL) | Microsoft Docs"
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
ms.assetid: ba4f334d-03e5-4a7b-9d42-628f4639b9a2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Paging (Entity SQL)
Il paging fisico può essere eseguito usando le sottoclausole [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md) e [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) nella clausola [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md).  Per eseguire il paging fisico in modo deterministico, è consigliabile usare SKIP e LIMIT.  Se si desidera solo limitare il numero di righe nel risultato in modo non deterministico, è consigliabile usare [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md).  TOP e SKIP\/LIMIT si escludono a vicenda.  
  
## Panoramica su TOP  
 La clausola SELECT può includere una sottoclausola TOP facoltativa dopo il modificatore ALL\/DISTINCT facoltativo.  La sottoclausola TOP specifica che verrà restituito solo il primo rowset del risultato della query.  Per altre informazioni, vedere [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md).  
  
## Panoramica su SKIP e LIMIT  
 SKIP e LIMIT fanno parte della clausola ORDER BY.  Se una sottoclausola dell'espressione SKIP è presente in una clausola ORDER BY, i risultati verranno ordinati in base alla specifica di ordinamento e il set di risultati includerà le righe a partire dalla riga immediatamente successiva all'espressione SKIP.  SKIP 5, ad esempio, consente di ignorare le prime cinque righe e restituisce le righe a partire dalla sesta in avanti.  Se una sottoclausola dell'espressione LIMIT è presente in una clausola ORDER BY, la query verrà ordinata in base alla specifica di ordinamento e il numero risultante di righe sarà limitato dall'espressione LIMIT.  LIMIT 5, ad esempio, limiterà il set di risultati a cinque istanze o righe.  SKIP e LIMIT non devono essere usate insieme. Con la clausola ORDER BY è possibile usare solo SKIP o LIMIT.  Per altre informazioni, vedere i seguenti argomenti:  
  
-   [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)  
  
-   [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)  
  
-   [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [How to: Page Through Query Results](http://msdn.microsoft.com/it-it/ffc0f920-e7de-42e0-9b12-ef356421d030)