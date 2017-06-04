---
title: "Espressioni di query (Entity SQL) | Microsoft Docs"
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
ms.assetid: c36f327b-e230-48d4-bbd5-78dc6478c447
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Espressioni di query (Entity SQL)
Un'espressione di query combina numerosi operatori di query diversi in un'unica sintassi.  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce i vari tipi di espressioni, inclusi i seguenti: [valori letterali](../../../../../../docs/framework/data/adonet/ef/language-reference/literals-entity-sql.md), [parametri](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md), [variabili](../../../../../../docs/framework/data/adonet/ef/language-reference/variables-entity-sql.md), operatori, [funzioni](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md), operatori di impostazione e così via.  Per altre informazioni, vedere [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md).  
  
## Clausole  
 Un'espressione di query è composta da una serie di clausole che consentono di applicare operazioni successive a una raccolta di oggetti.  Queste sono basate sulle stesse clausole presenti in un'istruzione SQL SELECT standard: [SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md), [FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md), [WHERE](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md), [GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md), [HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md) e [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md).  
  
## Ambito  
 I nomi definiti nella clausola FROM vengono introdotti nell'ambito FROM in base all'ordine con cui appaiono, da sinistra verso destra.  Nell'elenco JOIN le espressioni possono fare riferimento ai nomi definiti precedentemente nell'elenco.  Le proprietà pubbliche degli elementi identificate nella clausola FROM non vengono aggiunte all'ambito FROM, ma è sempre necessario fare riferimento a queste proprietà tramite il nome completo dell'alias.  In genere, tutte le parti dell'espressione SELECT vengono considerate all'interno dell'ambito FROM.  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)