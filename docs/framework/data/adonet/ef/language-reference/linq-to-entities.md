---
title: "LINQ to Entities | Microsoft Docs"
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
ms.assetid: 641f9b68-9046-47a1-abb0-1c8eaeda0e2d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# LINQ to Entities
LINQ to Entities fornisce il supporto LINQ \(Language Integrated Query\) che consente agli sviluppatori di scrivere query sul modello concettuale di Entity Framework usando Visual Basic o Visual C\#.  Le query su Entity Framework sono rappresentate da query a struttura ad albero dei comandi, eseguite sul contesto dell'oggetto.  LINQ to Entities consente di convertire query LINQ \(Language Integrated Query\) in query ad albero dei comandi, eseguire le query su Entity Framework e restituire oggetti che possono essere usati sia da Entity Framework sia da LINQ.  Di seguito viene descritto il processo di creazione ed esecuzione di una query LINQ to Entities:  
  
1.  Costruire un'istanza di <xref:System.Data.Objects.ObjectQuery%601> da <xref:System.Data.Objects.ObjectContext>.  
  
2.  Comporre una query LINQ to Entities in C\# o Visual Basic usando l'istanza di <xref:System.Data.Objects.ObjectQuery%601>.  
  
3.  Convertire gli operatori e le espressioni di query standard LINQ in alberi dei comandi.  
  
4.  Eseguire la query, nella rappresentazione ad albero dei comandi, sull'origine dati.  Tutte le eccezioni generate nell'origine dati durante l'esecuzione vengono passate direttamente al client.  
  
5.  Restituire i risultati della query al client.  
  
## Costruzione di un'istanza di ObjectQuery  
 La classe generica <xref:System.Data.Objects.ObjectQuery%601> rappresenta una query che restituisce una raccolta di zero o più entità tipizzate.  Una query di oggetto viene in genere costruita da un contesto dell'oggetto esistente anziché manualmente e appartiene sempre a tale contesto dell'oggetto.  Il contesto fornisce le informazioni relative a connessione e metadati necessarie per comporre ed eseguire la query.  La classe generica <xref:System.Data.Objects.ObjectQuery%601> implementa l'interfaccia generica <xref:System.Linq.IQueryable%601>, i cui metodi del generatore consentono la compilazione incrementale delle query LINQ.  È inoltre possibile consentire al compilatore di dedurre il tipo di entità tramite la parola chiave `var` di C\# \(`Dim` in Visual Basic, con inferenza di tipi locale abilitata\).  
  
## Composizione di query  
 Le istanze della classe generica <xref:System.Data.Objects.ObjectQuery%601>, che implementa l'interfaccia generica <xref:System.Linq.IQueryable%601>, fungono da origine dati per le query LINQ to Entities.  In una query è necessario specificare con esattezza le informazioni che si desidera recuperare dall'origine dati.  Una query può inoltre specificare in che modo ordinare, raggruppare e formattare le informazioni prima che vengano restituite.  In LINQ una query viene archiviata in una variabile.  La variabile di query non esegue azioni né restituisce dati. Viene solo usata per archiviare le informazioni sulla query.  Dopo aver creato una query è necessario eseguirla per recuperare eventuali dati.  
  
 Le query LINQ to Entities possono essere composte in due sintassi diverse, ovvero la sintassi delle espressioni di query e la sintassi delle query basate su metodo.  La sintassi delle espressioni di query e la sintassi delle query basate su metodo rappresentano una novità in C\# 3.0 e Visual Basic 9.0.  
  
 Per altre informazioni, vedere [Query in LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md).  
  
## Conversione della query  
 Per eseguire una query LINQ to Entities su Entity Framework, è necessario convertire la query LINQ in una rappresentazione a struttura ad albero dei comandi che possa essere eseguita su Entity Framework.  
  
 Le query LINQ to Entities includono operatori di query standard LINQ, ad esempio <xref:System.Linq.Queryable.Select%2A>, <xref:System.Linq.Queryable.Where%2A> e <xref:System.Linq.Queryable.GroupBy%2A>, ed espressioni \(x \> 10, Contact.LastName e così via\).  Gli operatori LINQ non sono definiti da una classe, ma sono piuttosto metodi in una classe.  In LINQ le espressioni possono contenere tutto ciò che è consentito dai tipi all'interno dello spazio dei nomi <xref:System.Linq.Expressions> e, per estensione, tutto ciò che può essere rappresentato in una funzione lambda.  Si tratta di un superset delle espressioni consentite da Entity Framework, per definizione limitate alle operazioni consentite sul database, e supportate da <xref:System.Data.Objects.ObjectQuery%601>.  
  
 In Entity Framework sia gli operatori sia le espressioni sono rappresentati da una singola gerarchia dei tipi e vengono quindi inclusi in un albero dei comandi.  L'albero dei comandi viene usato da Entity Framework per eseguire la query.  Se la query LINQ non può essere espressa come albero dei comandi, viene generata un'eccezione durante la conversione della query.  La conversione di query LINQ to Entities comporta due conversioni secondarie: la conversione degli operatori di query standard e la conversione delle espressioni.  
  
 Per un certo numero di operatori di query standard LINQ non è disponibile una conversione valida in LINQ to Entities.  Qualsiasi tentativo di usare tali operatori restituirà un'eccezione in fase di conversione della query.  Per un elenco degli operatori LINQ to Entities supportati, vedere [Metodi LINQ supportati e non supportati \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md).  
  
 Per altre informazioni sull'utilizzo di operatori di query standard in LINQ to Entities, vedere [Operatori di query standard nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md).  
  
 Poiché in generale le espressioni in LINQ to Entities vengono valutate nel server, non è previsto che il comportamento dell'espressione sia conforme alla semantica CLR.  Per altre informazioni, vedere [Espressioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md).  
  
 Per informazioni su come le chiamate ai metodi CLR vengono mappate alle funzioni canoniche nell'origine dati, vedere [Mapping dei metodi CLR alle funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md).  
  
 Per informazioni su come chiamare le funzioni canoniche, di database e personalizzate dall'interno delle query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)], vedere [Chiamata di funzioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md).  
  
## Esecuzione di query  
 Al termine della creazione della query LINQ da parte dell'utente, la query viene convertita in una rappresentazione compatibile con Entity Framework, sotto forma di strutture ad albero dei comandi, e viene quindi eseguita sull'origine dati.  In fase di esecuzione della query tutte le espressioni di query, o i componenti della query, vengono valutate nel client o nel server,  incluse le espressioni usate nella materializzazione dei risultati o nelle proiezioni di entità.  Per altre informazioni, vedere [Esecuzione di query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md).  Per informazioni su come migliorare le prestazioni compilando una query una volta, quindi eseguendola molte volte con parametri diversi, vedere [Query compilate \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md).  
  
## Materializzazione  
 La materializzazione è il processo di restituzione dei risultati della query al client come tipi CLR.  In LINQ to Entities i record di dati dei risultati della query non vengono mai restituiti, ma è sempre disponibile un tipo CLR di supporto definito dall'utente o da Entity Framework oppure generato dal compilatore \(tipi anonimi\).  Tutta la materializzazione degli oggetti viene eseguita da Entity Framework.  Qualsiasi errore correlato all'impossibilità di eseguire il mapping tra Entity Framework e CLR comporterà la generazione di eccezioni durante la materializzazione degli oggetti.  
  
 I risultati della query vengono in genere restituiti come uno degli elementi seguenti:  
  
-   Raccolta di zero o più oggetti entità tipizzate o proiezione di tipi complessi definiti nel modello concettuale.  
  
-   Tipi CLR supportati da [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)].  
  
-   Raccolte inline.  
  
-   Tipi anonimi.  
  
 Per altre informazioni, vedere [Risultati delle query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md).  
  
## Contenuto della sezione  
 [Query in LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/queries-in-linq-to-entities.md)  
  
 [Espressioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/expressions-in-linq-to-entities-queries.md)  
  
 [Chiamata di funzioni nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/calling-functions-in-linq-to-entities-queries.md)  
  
 [Query compilate \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/compiled-queries-linq-to-entities.md)  
  
 [Esecuzione di query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-execution.md)  
  
 [Risultati delle query](../../../../../../docs/framework/data/adonet/ef/language-reference/query-results.md)  
  
 [Operatori di query standard nelle query LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/standard-query-operators-in-linq-to-entities-queries.md)  
  
 [Mapping dei metodi CLR alle funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/clr-method-to-canonical-function-mapping.md)  
  
 [Metodi LINQ supportati e non supportati \(LINQ to Entities\)](../../../../../../docs/framework/data/adonet/ef/language-reference/supported-and-unsupported-linq-methods-linq-to-entities.md)  
  
 [Problemi noti e considerazioni relativi a LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)  
  
## Vedere anche  
 [Problemi noti e considerazioni relativi a LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ e ADO.NET](../../../../../../docs/framework/data/adonet/linq-and-ado-net.md)   
 [ADO.NET Entity Framework](../../../../../../docs/framework/data/adonet/ef/index.md)