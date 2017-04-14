---
title: "IN (Entity SQL) | Microsoft Docs"
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
ms.assetid: 51662950-ee01-4857-b7b9-311dd8515966
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# IN (Entity SQL)
Determina se un valore corrisponde a qualsiasi valore in una raccolta.  
  
## Sintassi  
  
```  
  
value [ NOT ] IN expression  
```  
  
## Argomenti  
 `value`  
 Qualsiasi espressione valida che restituisce il valore di cui trovare la corrispondenza.  
  
 \[ NOT \]  
 Specifica la negazione del risultato `Boolean` di IN.  
  
 `expression`  
 Qualsiasi espressione valida che restituisce la raccolta da testare per trovare una corrispondenza. Tutte le espressioni devono essere dello stesso tipo o di un tipo di base o derivato comune di `value`.  
  
## Valore restituito  
 `true` se il valore viene trovato nella raccolta; null se il valore è null o se la raccolta è null; in caso contrario `false`. L'utilizzo di NOT IN consente di negare i risultati di IN.  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore IN per determinare se un valore corrisponde a qualsiasi valore in una raccolta. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#IN](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#in)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)