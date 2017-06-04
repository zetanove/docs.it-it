---
title: "Funzioni definite dall&#39;utente (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f9e6bbd-8e5a-43e1-809f-f8a61338e522
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Funzioni definite dall&#39;utente (Entity SQL)
Nelle query Entity SQL sono supportate le chiamate a funzioni definite dall'utente.  È possibile definire queste funzioni inline con la query \(vedere [How to: Call a User\-Defined Function](http://msdn.microsoft.com/it-it/ad131b86-8b4e-4747-8605-d4fc64fb9d02)\) o come parte del modello concettuale \(vedere [How to: Define Custom Functions in the Conceptual Model](http://msdn.microsoft.com/it-it/0dad7b8b-58f6-4271-b238-f34810d68e5f)\).  Le funzioni del modello concettuale sono definite come un comando Entity SQL nell'elemento [DefiningExpression](http://msdn.microsoft.com/it-it/d3da8d8b-a048-47ee-8d81-0c2ea3acdd3e) di un elemento [Function](http://msdn.microsoft.com/it-it/dc3beca7-55cf-4977-8db0-5064cdbab134) nel modello concettuale.  
  
 Entity SQL consente di definire delle funzioni nel comando di query stesso.  L'operatore [FUNCTION](../../../../../../docs/framework/data/adonet/ef/language-reference/function-entity-sql.md) definisce funzioni inline.  È possibile definire più funzioni in un singolo comando e queste funzioni possono avere lo stesso nome purché le rispettive firme siano univoche.  Per altre informazioni, vedere [Risoluzione dell'overload di funzioni](../../../../../../docs/framework/data/adonet/ef/language-reference/function-overload-resolution-entity-sql.md).  
  
## Vedere anche  
 [Funzioni](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)