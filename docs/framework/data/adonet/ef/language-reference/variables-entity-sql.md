---
title: "Variabili (Entity SQL) | Microsoft Docs"
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
ms.assetid: 3eed222a-f8f6-46b6-9cd5-220cc0e4e5d8
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Variabili (Entity SQL)
## Variabile  
 Un'espressione variabile è un riferimento a un'espressione denominata definita nell'ambito corrente.  Un riferimento a una variabile deve essere un identificatore [!INCLUDE[esql](../../../../../../includes/esql-md.md)] valido, come definito in [Identificatori](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md).  
  
 Nell'esempio seguente viene illustrato l'uso di una variabile nell'espressione.  Il valore `c` nella clausola FROM è la definizione della variabile.  L'utilizzo di `c` nella clausola SELECT rappresenta il riferimento alla variabile.  
  
```  
select c   
from LOB.customers as c  
```  
  
## Vedere anche  
 [Identificatori](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)   
 [Parametri](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)   
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)