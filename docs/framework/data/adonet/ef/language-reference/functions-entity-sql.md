---
title: "Funzioni (Entity SQL) | Microsoft Docs"
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
ms.assetid: 52b3d776-5acc-4f69-b614-5a43ce56ef9f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Funzioni (Entity SQL)
Entity SQL supporta funzioni definite dall'utente, funzioni canoniche e funzioni specifiche del provider.  Le funzioni definite dall'utente vengono specificate nel modello concettuale o inline nella query.  Per altre informazioni, vedere [Funzioni definite dall'utente](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md).  
  
 Le funzioni canoniche sono predefinite in Entity Framework e devono essere supportate dai provider di dati.  Se un utente chiama una funzione che non è supportata da un provider, i comandi Entity SQL hanno esito negativo.  Le funzioni canoniche vengono pertanto generalmente preferite alle funzioni specifiche dell'archivio, che sono incluse in uno spazio dei nomi specifico del provider.  Per altre informazioni, vedere [Funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md).  
  
 Il provider gestito del client Microsoft SQL fornisce un set di funzioni specifiche del provider.  Per altre informazioni, vedere [Funzioni di SqlClient per Entity Framework](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md).  
  
## Contenuto della sezione  
 [Funzioni definite dall'utente](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md)  
  
 [Risoluzione dell'overload di funzioni](../../../../../../docs/framework/data/adonet/ef/language-reference/function-overload-resolution-entity-sql.md)  
  
 [Funzioni di aggregazione](../../../../../../docs/framework/data/adonet/ef/aggregate-functions-sqlclient-for-entity-framework.md)  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)