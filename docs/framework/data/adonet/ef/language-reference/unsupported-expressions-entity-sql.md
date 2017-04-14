---
title: "Espressioni non supportate (Entity SQL) | Microsoft Docs"
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
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Espressioni non supportate (Entity SQL)
In questo argomento vengono descritte le espressioni [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] non supportate in [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Per altre informazioni, vedere [Differenze tra Entity SQL e Transact\-SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md).  
  
## Predicati quantificati  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] consente i costrutti con il formato seguente:  
  
```  
sal > all (select salary from employees)  
sal > any (select salary from employees)  
```  
  
 In [!INCLUDE[esql](../../../../../../includes/esql-md.md)], tuttavia, tali costrutti non sono supportati.  È possibile scrivere espressioni equivalenti in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] come indicato di seguito:  
  
```  
not exists(select 0 from employees as e where sal > e.salary)  
exists(select 0 from employees as e where sal > e.salary)  
```  
  
## Operatore \*  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] supporta l'uso dell'operatore \* nella clausola SELECT per indicare che tutte le colonne devono essere proiettate.  Questa opzione non è supportata in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Differenze tra Entity SQL e Transact\-SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)