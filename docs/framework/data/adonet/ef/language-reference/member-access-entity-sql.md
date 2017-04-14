---
title: ". (Accesso ai membri) (Entity SQL) | Microsoft Docs"
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
ms.assetid: 4733e3b2-3efa-4b96-b591-ac31350e96ad
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# . (Accesso ai membri) (Entity SQL)
L'operatore punto \(.\) è l'operatore di accesso ai membri [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  L'operatore di accesso ai membri viene usato per produrre il valore di una proprietà o di un campo di un'istanza del tipo di modello concettuale strutturale.  
  
## Sintassi  
  
```  
expression.identifier  
```  
  
## Argomenti  
 `expression`  
 Istanza di un tipo di modello concettuale strutturale.  
  
 `identifier`  
 Proprietà o campo che appartiene a un'istanza dell'oggetto.  
  
## Note  
 L'operatore punto \(.\) può essere usato per estrarre campi da un record, analogamente all'estrazione di proprietà di un tipo di entità o complesso.  Se, ad esempio, un oggetto n di tipo Name è un membro del tipo Person e p è un'istanza del tipo Person, p.  n è un'espressione di accesso ai membri valida che restituisce un valore di tipo Name.  
  
 `select p.Name.FirstName from LOB.Person as p`  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)