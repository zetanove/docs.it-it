---
title: "Provider EntityClient per Entity Framework | Microsoft Docs"
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
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Provider EntityClient per Entity Framework
EntityClient è un provider di dati usato dalle applicazioni Entity Framework per accedere a dati descritti in un  modello concettuale.  Per informazioni sui modelli concettuali, vedere [Modellazione e mapping](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md).  EntityClient usa altri provider di dati .NET Framework per accedere all'origine dati,  ad esempio il provider di dati .NET Framework per SQL Server \(SqlClient\) in caso di accesso a un database SQL Server.  Per informazioni sul provider SqlClient, vedere [SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md).  Il provider EntityClient viene implementato nello spazio dei nomi <xref:System.Data.EntityClient>.  
  
## Gestione di connessioni  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] è compilato in base a provider di dati [!INCLUDE[vstecado](../../../../../includes/vstecado-md.md)] specifici dell'archiviazione fornendo un oggetto <xref:System.Data.EntityClient.EntityConnection> a un provider di dati e a un database relazionale sottostanti.  Per costruire un oggetto <xref:System.Data.EntityClient.EntityConnection>, è necessario fare riferimento a un set di metadati che contiene i mapping e i modelli necessari, nonché a una stringa di connessione e a un nome di provider di dati specifici dell'archiviazione.  Dopo avere stabilito una connessione \(oggetto <xref:System.Data.EntityClient.EntityConnection>\), è possibile accedere alle entità tramite le classi generate dal modello concettuale.  
  
 È possibile specificare una stringa di connessione nel file app.config.  
  
 <xref:System.Data.EntityClient> include anche la classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder>.  Questa classe consente agli sviluppatori di creare a livello di codice stringhe di connessione sintatticamente corrette, nonché di analizzare e ricompilare le stringhe di connessione esistenti, usando le proprietà e i metodi della classe.  Per altre informazioni, vedere [Procedura: compilare una stringa di connessione EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md).  
  
## Creazione di query  
 [!INCLUDE[esql](../../../../../includes/esql-md.md)] è un linguaggio SQL indipendente dall'archiviazione che interagisce direttamente con gli schemi di entità concettuali e supporta i concetti EDM, quali l'ereditarietà e le relazioni.  La classe <xref:System.Data.EntityClient.EntityCommand> viene usata per eseguire un comando [!INCLUDE[esql](../../../../../includes/esql-md.md)] su un modello di entità.  Quando si costruiscono oggetti <xref:System.Data.EntityClient.EntityCommand>, è possibile specificare un nome di stored procedure o un testo della query.  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] funziona con provider di dati specifici dell'archiviazione per convertire il linguaggio [!INCLUDE[esql](../../../../../includes/esql-md.md)] generico in query specifiche dell'archiviazione.  Per altre informazioni sulla scrittura di query [!INCLUDE[esql](../../../../../includes/esql-md.md)], vedere [Linguaggio Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md).  
  
 Nell'esempio seguente viene creato un oggetto <xref:System.Data.EntityClient.EntityCommand> e viene assegnato un testo della query [!INCLUDE[esql](../../../../../includes/esql-md.md)] alla proprietà <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=fullName>.  Questa query [!INCLUDE[esql](../../../../../includes/esql-md.md)] consente di richiedere i prodotti ordinati in base al prezzo di listino nel modello concettuale.  Il codice seguente non comporta alcuna conoscenza del modello di archiviazione.  
  
 `EntityCommand cmd = conn.CreateCommand();`  
  
 `cmd.CommandText = @"` `SELECT VALUE p`  
  
 `FROM AdventureWorksEntities.Product AS p`  
  
 `ORDER BY p.ListPrice ";`  
  
## Esecuzione di query  
 Quando una query viene eseguita, viene analizzata e convertita in una struttura ad albero dei comandi canonici.  Tutte le elaborazioni successive vengono eseguite nell'albero dei comandi.  L'albero dei comandi costituisce il mezzo di comunicazione tra <xref:System.Data.EntityClient> e il provider di dati [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] sottostante, ad esempio <xref:System.Data.SqlClient>.  
  
 <xref:System.Data.EntityClient.EntityDataReader> espone i risultati dell'esecuzione di un oggetto <xref:System.Data.EntityClient.EntityCommand> su un modello concettuale.  Per eseguire il comando che restituisce <xref:System.Data.EntityClient.EntityDataReader>, chiamare <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>.  <xref:System.Data.EntityClient.EntityDataReader> implementa <xref:System.Data.IExtendedDataRecord> per descrivere risultati completamente strutturati.  
  
## Gestione di transazioni  
 In Entity Framework è possibile usare le transazioni in modo esplicito e in modo automatico.  Le transazioni automatiche usano lo spazio dei nomi <xref:System.Transactions> e le transazioni esplicite usano la classe <xref:System.Data.EntityClient.EntityTransaction>.  
  
 Per aggiornare i dati esposti tramite un modello concettuale. Vedere [How to: Manage Transactions in the Entity Framework](http://msdn.microsoft.com/it-it/4a55eb7f-f826-4a48-9df1-aebe2352ebef).  
  
## Contenuto della sezione  
 [Procedura: compilare una stringa di connessione EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)  
  
 [Procedura: eseguire una query che restituisce risultati PrimitiveType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Procedura: eseguire una query che restituisce risultati StructuralType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Procedura: eseguire una query che restituisce risultati RefType](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Procedura: eseguire una query che restituisce tipi complessi](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Procedura: eseguire una query che restituisce raccolte annidate](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Procedura: eseguire una query Entity SQL con parametri utilizzando EntityCommand](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Procedura: eseguire una stored procedure con parametri utilizzando EntityCommand](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Procedura: eseguire una query polimorfica](../../../../../docs/framework/data/adonet/ef/how-to-execute-a-polymorphic-query.md)  
  
 [Procedura: navigare nelle relazioni con l'operatore Navigate](../../../../../docs/framework/data/adonet/ef/how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## Vedere anche  
 [Managing Connections and Transactions](http://msdn.microsoft.com/it-it/b6659d2a-9a45-4e98-acaa-d7a8029e5b99)   
 [ADO.NET Entity Framework](../../../../../docs/framework/data/adonet/ef/index.md)   
 [Riferimenti per il linguaggio](../../../../../docs/framework/data/adonet/ef/language-reference/index.md)