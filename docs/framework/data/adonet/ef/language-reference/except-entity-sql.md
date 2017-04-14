---
title: "EXCEPT (Entity SQL) | Microsoft Docs"
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
ms.assetid: 69cc23e5-3f8f-4b49-b20e-2f84ff11c80d
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# EXCEPT (Entity SQL)
Restituisce una raccolta di tutti i valori distinti dell'espressione di query a sinistra dell'operando EXCEPT che non vengono restituiti anche dall'espressione di query a destra dell'operando EXCEPT. Tutte le espressioni devono essere dello stesso tipo o di un tipo di base o derivato comune di `expression`.  
  
## Sintassi  
  
```  
  
expression EXCEPT expression  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione di query valida che restituisce una raccolta da confrontare con la raccolta restituita da un'altra espressione di query.  
  
## Valore restituito  
 Raccolta dello stesso tipo o di un tipo di base o derivato comune di `expression`.  
  
## Note  
 EXCEPT è uno degli operatori sui set di [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Tutti gli operatori sui set di [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono valutati da sinistra a destra. Nella tabella seguente viene indicata la precedenza tra gli operatori dei set [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
|Precedenza|Operatori|  
|----------------|---------------|  
|Più alta|INTERSECT|  
||UNION<br /><br /> UNION ALL|  
||EXCEPT|  
|Più bassa|EXISTS<br /><br /> OVERLAPS<br /><br /> FLATTEN<br /><br /> SET|  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore EXCEPT per restituire una raccolta di tutti i valori distinti da due espressioni di query. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#EXCEPT](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#except)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)