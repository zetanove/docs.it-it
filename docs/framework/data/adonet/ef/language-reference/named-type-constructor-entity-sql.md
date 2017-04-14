---
title: "Costruttore di tipo denominato (Entity SQL) | Microsoft Docs"
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
ms.assetid: 549dea04-d93d-4c87-a292-f81b1598dbfd
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Costruttore di tipo denominato (Entity SQL)
Utilizzato per creare istanze di tipi nominali del modello concettuale, ad esempio i tipi di entità o i tipi complessi.  
  
## Sintassi  
  
```  
  
[{identifier. }] identifier( [expression [{, expression }]] )  
```  
  
## Argomenti  
 `identifier`  
 Valore che rappresenta un identificatore semplice o delimitato. Per altre informazioni, vedere [Identificatori](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)  
  
 `expression`  
 Attributi del tipo che si presuppone essere nello stesso ordine in cui appaiono nella dichiarazione del tipo.  
  
## Valore restituito  
 Istanze di tipi di entità e di tipi complessi denominati.  
  
## Note  
 Negli esempi seguenti viene illustrato come costruire i tipi nominali e complessi:  
  
 L'espressione seguente consente di creare un'istanza di un tipo `Person`:  
  
 `Person("abc", 12)`  
  
 L'espressione seguente consente di creare un'istanza di un tipo complesso:  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 L'espressione seguente consente di creare un'istanza di un tipo complesso annidato:  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 L'espressione seguente consente di creare un'istanza di un'entità con un tipo complesso annidato:  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 Nell'esempio seguente viene illustrato come inizializzare una proprietà di un tipo complesso impostandola su Null:`MyModel.ZipCode(‘98118’, null)`.  
  
## Esempio  
 Nella query Entity SQL seguente viene usato il costruttore di tipi denominati per creare un'istanza di un tipo di modello concettuale. La query è basata sul modello Sales di AdventureWorks. Per compilare ed eseguire questa query, effettuare le operazioni seguenti:  
  
1.  Seguire la procedura indicata in [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Passare la query seguente come argomento al metodo `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#NAMED_TYPE_CONSTRUCTOR](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#named_type_constructor)]  
  
## Vedere anche  
 [Costruzione di tipi](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)   
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)