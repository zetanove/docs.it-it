---
title: "/ (divisione) (Entity SQL) | Microsoft Docs"
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
ms.assetid: ef48c368-f3ed-4275-8ada-4e9649781262
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# / (divisione) (Entity SQL)
Divide un numero per un altro.  
  
## Sintassi  
  
```  
  
dividend  
/  
divisor  
  
```  
  
## Argomenti  
 `dividend`  
 Espressione numerica da dividere.`dividend` è qualsiasi espressione valida con qualsiasi tipo di dati numerici.  
  
 `divisor`  
 Espressione numerica per la quale dividere il dividendo.`divisor` è qualsiasi espressione valida con qualsiasi tipo di dati numerici.  
  
## Tipi di risultati  
 Tipo di dati ottenuto della promozione implicita del tipo dei due argomenti. Per altre informazioni sulla promozione implicita del tipo, vedere [Sistema di tipi](../../../../../../docs/framework/data/adonet/ef/language-reference/type-system-entity-sql.md).  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore aritmetico \/ per dividere un numero per un altro. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#DIVIDE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#divide)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)