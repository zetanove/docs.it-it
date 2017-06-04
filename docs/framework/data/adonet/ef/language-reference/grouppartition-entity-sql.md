---
title: "GROUPPARTITION (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0482e9b-086c-451c-9dfa-ccb024a9efb6
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# GROUPPARTITION (Entity SQL)
Restituisce una raccolta di valori di argomento che sono estratti dalla partizione di gruppo corrente alla quale è correlata l'aggregazione. L'aggregazione `GroupPartition` è un'aggregazione basata sul gruppo e non ha un formato basato sulla raccolta.  
  
## Sintassi  
  
```  
  
GROUPPARTITION( [ALL|DISTINCT] expression )  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## Note  
 Nella query seguente viene prodotto un elenco di prodotti e una raccolta di quantità nelle righe degli ordini per ogni prodotto:  
  
```  
select p, GroupPartition(ol.Quantity) from LOB.OrderLines as ol  
  group by ol.Product as p  
```  
  
 Le due query seguenti sono semanticamente uguali:  
  
```  
select p, Sum(GroupPartition(ol.Quantity)) from LOB.OrderLines as ol  
  group by ol.Product as p  
select p, Sum(ol.Quantity) from LOB.OrderLines as ol  
  group by ol.Product as p  
```  
  
 L'operatore `GROUPPARTITION` può essere usato insieme a funzioni di aggregazione definite dall'utente.  
  
 `GROUPPARTITION` è un operatore di aggregazione speciale che mantiene un riferimento al set di input raggruppato. Questo riferimento può essere usato ovunque nella query laddove GROUP BY è nell'ambito. Di seguito è riportato un esempio:  
  
```  
select p, GroupPartition(ol.Quantity) from LOB.OrderLines as ol group by ol.Product as p  
```  
  
 Se si usa un GROUP BY normale, i risultati del raggruppamento sono nascosti. È possibile usare solo i risultati in una funzione di aggregazione. Per vedere i risultati del raggruppamento, è necessario correlarli al set di input tramite una sottoquery. Le due query seguenti sono equivalenti:  
  
```  
select p, (select q from GroupPartition(ol.Quantity) as q) from LOB.OrderLines as ol group by ol.Product as p  
select p, (select ol.Quantity as q from LOB.OrderLines as ol2 where ol2.Product = p) from LOB.OrderLines as ol group by ol.Product as p  
```  
  
 Come illustrato nell'esempio, grazie all'operatore di aggregazione GROUPPARTITION diventa più semplice ottenere un riferimento al set di input dopo il raggruppamento.  
  
 L'operatore GROUPPARTITION può specificare qualsiasi espressione [!INCLUDE[esql](../../../../../../includes/esql-md.md)] nell'operatore di input quando si usa il parametro `expression`.  
  
 Tutte le espressioni di input seguenti alla partizione di gruppo sono valide:  
  
```  
select groupkey, GroupPartition(b) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(1) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(a + b) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition({a + b}) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition({42}) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(b > a) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
```  
  
## Esempio  
 Nell'esempio seguente viene mostrato come usare la clausola GROUPPARTITION con la clausola GROUP BY. La clausola GROUP BY raggruppa entità `SalesOrderHeader` in base a `Contact`. La clausola GROUPPARTITION proietta quindi la proprietà `TotalDue` per ogni gruppo, creando così una raccolta di numeri decimali.  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]