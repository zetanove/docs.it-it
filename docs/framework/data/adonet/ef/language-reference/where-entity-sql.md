---
title: "WHERE (Entity SQL) | Microsoft Docs"
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
ms.assetid: a8e1061e-0028-4a6f-8f19-b9f48e96c4b8
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# WHERE (Entity SQL)
La clausola WHERE viene applicata direttamente dopo la clausola [FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md).  
  
## Sintassi  
  
```  
[ WHERE expression ]  
```  
  
## Argomenti  
 `expression`  
 Tipo Boolean.  
  
## Note  
 La clausola WHERE dispone della stessa semantica descritta per [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)].  Questa clausola consente di ridurre gli oggetti prodotti dall'espressione di query limitando gli elementi delle raccolte di origine a quelli che soddisfano la condizione.  
  
```  
select c from cs as c where e  
```  
  
 L'espressione `e` deve essere di tipo Boolean.  
  
 La clausola WHERE viene applicata direttamente dopo la clausola FROM e prima che avvenga qualsiasi operazione di  raggruppamento, ordinamento o proiezione.  Tutti i nomi degli elementi definiti nella clausola FROM sono visibili all'espressione della clausola WHERE.  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Espressioni di query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)