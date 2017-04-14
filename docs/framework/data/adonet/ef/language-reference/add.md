---
title: "+ (addizione) | Microsoft Docs"
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
ms.assetid: 51769b02-a8f7-4177-9e99-bbd10e77092c
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# + (addizione)
Esegue l'addizione di due numeri.  
  
## Sintassi  
  
```  
  
expression  
+  
expression  
  
```  
  
## Argomenti  
 `expression`  
 Qualsiasi espressione valida con qualsiasi tipo di dati numerici.  
  
## Tipi di risultati  
 Tipo di dati ottenuto della promozione implicita del tipo dei due argomenti. Per altre informazioni sulla promozione implicita del tipo, vedere [Sistema di tipi](../../../../../../docs/framework/data/adonet/ef/language-reference/type-system-entity-sql.md).  
  
## Note  
 Per i tipi EDM.String, l'aggiunta è la concatenazione.  
  
## Esempio  
 Nella query Entity SQL seguente viene usato l'operatore aritmetico \+ per sommare due numeri. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#ADD](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#add)]  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Tipi del modello concettuale \(CSDL\)](http://msdn.microsoft.com/it-it/987b995f-e429-4569-9559-b4146744def4)