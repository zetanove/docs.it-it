---
title: "Linguaggio Entity SQL | Microsoft Docs"
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
ms.assetid: 9e7d8837-28c5-429d-a824-7bafb59724cf
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Linguaggio Entity SQL
Entity SQL è un linguaggio di query indipendente da archiviazione che è simile a SQL.  Entity SQL consente di eseguire una query su dati di entità, come oggetti o in un form tabulare.  L'utilizzo di Entity SQL è indicato nei casi seguenti:  
  
-   Quando è necessario creare una query dinamicamente in fase di runtime.  In questo caso, si dovrebbero usare anche i metodi del generatore di query di <xref:System.Data.Objects.ObjectQuery%601> anziché costruire una stringa di query Entity SQL in fase di runtime.  
  
-   Quando si desidera definire una query come parte della definizione del modello.  Solo Entity SQL è supportato in un modello di dati.  Per altre informazioni, vedere [QueryView Element \(MSL\)](http://msdn.microsoft.com/it-it/f0426b34-45cb-4fd7-9777-e0570c5e0e80).  
  
-   Quando si usa EntityClient per restituire dati di entità di sola lettura come set di righe usando un oggetto <xref:System.Data.EntityClient.EntityDataReader>.  Per altre informazioni, vedere [Provider EntityClient per Entity Framework](../../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
-   Se si è già esperti nei linguaggi di query basati su SQL, Entity SQL potrebbe essere la soluzione più semplice.  
  
## Uso di Entity SQL con il provider EntityClient  
 Se si desidera usare Entity SQL con il provider EntityClient, vedere gli argomenti seguenti per ulteriori informazioni:  
  
 [Provider EntityClient per Entity Framework](../../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)  
  
 [Procedura: compilare una stringa di connessione EntityConnection](../../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)  
  
 [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Procedura: eseguire una query che restituisce risultati RefType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Procedura: eseguire una query che restituisce tipi complessi](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Procedura: eseguire una query che restituisce raccolte annidate](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Procedura: eseguire una query Entity SQL con parametri utilizzando EntityCommand](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Procedura: eseguire una stored procedure con parametri utilizzando EntityCommand](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Procedura: eseguire una query polimorfica](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-polymorphic-query.md)  
  
 [Procedura: navigare nelle relazioni con l'operatore Navigate](../../../../../../docs/framework/data/adonet/ef/how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## Uso di Entity SQL con le query di oggetto  
 Se si desidera usare Entity SQL con query di oggetto, vedere gli argomenti seguenti per ulteriori informazioni:  
  
 [How to: Execute a Query that Returns Entity Type Objects](http://msdn.microsoft.com/it-it/f73e137d-1534-42bb-9e31-99ca42c19b48)  
  
 [How to: Execute a Parameterized Query](http://msdn.microsoft.com/it-it/42048f03-c65c-4d98-b50a-3e7d537a63e8)  
  
 [How to: Navigate Relationships Using Navigation Properties](http://msdn.microsoft.com/it-it/b1d71c7d-16a7-4b46-96ac-690176bd5057)  
  
 [How to: Call a User\-Defined Function](http://msdn.microsoft.com/it-it/ad131b86-8b4e-4747-8605-d4fc64fb9d02)  
  
 [How to: Filter Data](http://msdn.microsoft.com/it-it/776f8556-3350-4572-804a-b1513515c1b2)  
  
 [How to: Sort Data](http://msdn.microsoft.com/it-it/c05f2506-cb9d-4ebc-822b-300042ad53e7)  
  
 [How to: Group Data](http://msdn.microsoft.com/it-it/df801d9d-9a8a-4157-97a6-5016b18998e1)  
  
 [How to: Aggregate Data](http://msdn.microsoft.com/it-it/4cf04ce8-3c0f-4f88-9d97-8fac8622598d)  
  
 [How to: Execute a Query that Returns Anonymous Type Objects](http://msdn.microsoft.com/it-it/3b264025-e911-4d73-90ce-992d2b9d189d)  
  
 [How to: Execute a Query that Returns a Collection of Primitive Types](http://msdn.microsoft.com/it-it/115b52c0-4f27-4253-8991-284b450000b5)  
  
 [How to: Query Related Objects in an EntityCollection](http://msdn.microsoft.com/it-it/11ce946f-16f8-4c1d-9d80-f740853807ba)  
  
 [How to: Order the Union of Two Queries](http://msdn.microsoft.com/it-it/853c583a-eaba-4400-830d-be974e735313)  
  
 [How to: Page Through Query Results](http://msdn.microsoft.com/it-it/ffc0f920-e7de-42e0-9b12-ef356421d030)  
  
## Contenuto della sezione  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)  
  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)  
  
## Vedere anche  
 [ADO.NET Entity Framework](../../../../../../docs/framework/data/adonet/ef/index.md)   
 [Riferimenti per il linguaggio](../../../../../../docs/framework/data/adonet/ef/language-reference/index.md)