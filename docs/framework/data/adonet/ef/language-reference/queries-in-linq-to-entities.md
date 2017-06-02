---
title: "Query in LINQ to Entities | Microsoft Docs"
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
ms.assetid: c015a609-29eb-4e95-abb1-2ca721c6e2ad
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Query in LINQ to Entities
Una query è un'espressione che recupera dati da un'origine dati.  Le query sono in genere espresse in un linguaggio di query specializzato, ad esempio SQL per i database relazionali e XQuery per XML.  Gli sviluppatori hanno dovuto pertanto imparare un nuovo linguaggio di query per ogni tipo di origine dati o formato dati usato per le query.  LINQ \(Language\-Integrated Query\) offre un modello più semplice e coerente per l'uso di dati in diversi tipi di origini dati e formati di dati.  In una query LINQ vengono sempre usati oggetti di programmazione.  
  
 Un'operazione di query LINQ comporta tre azioni: il recupero di una o più origini dati, la creazione della query e l'esecuzione della query.  
  
 È possibile usare LINQ per eseguire query su origini dati che implementano l'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>.  Le istanze della classe generica <xref:System.Data.Objects.ObjectQuery%601>, che implementa l'interfaccia generica <xref:System.Linq.IQueryable%601>, fungono da origine dati per le query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  La classe generica <xref:System.Data.Objects.ObjectQuery%601> rappresenta una query che restituisce una raccolta di zero o più oggetti tipizzati.  È anche possibile consentire al compilatore di dedurre il tipo di un'entità tramite la parola chiave `var` di C\# \(Dim in Visual Basic\).  
  
 Nella query è necessario specificare esattamente le informazioni che si desidera recuperare dall'origine dati.  Una query può inoltre specificare in che modo ordinare, raggruppare e formattare le informazioni prima che vengano restituite.  In LINQ una query viene archiviata in una variabile.  Se la query restituisce una sequenza di valori, la variabile di query deve essere un tipo queryable.  La variabile di query non esegue azioni né restituisce dati. Viene solo usata per archiviare le informazioni sulla query.  Dopo aver creato una query è necessario eseguirla per recuperare eventuali dati.  
  
## Sintassi della query  
 Per la composizione di query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] è possibile usare due diverse sintassi: la sintassi delle espressioni di query e la sintassi delle query basate su metodo.  La sintassi delle espressioni di query è una novità di C\# 3.0 e Visual Basic 9.0 e consiste in un set di clausole scritte in una sintassi dichiarativa simile a Transact\-SQL o a XQuery.  Tuttavia, [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] Common Language Runtime \(CLR\) non è in grado di leggere da solo la sintassi delle espressioni di query.  Pertanto, in fase di compilazione, le espressioni di query vengono convertite in chiamate al metodo in modo da poter essere usate da CLR.  Questi metodi sono noti come *operatori di query standard*.  Gli sviluppatori possono scegliere di chiamare direttamente questi metodi usando la relativa sintassi, anziché usare la sintassi di query. Per altre informazioni, vedere [Query Syntax and Method Syntax in LINQ](../Topic/Query%20Syntax%20and%20Method%20Syntax%20in%20LINQ%20\(C%23\).md).  
  
### Sintassi delle espressioni di query  
 Le espressioni di query vengono scritte in una sintassi di query dichiarativa.  Questa sintassi consente a uno sviluppatore di scrivere query in un linguaggio di alto livello formattato in modo simile a Transact\-SQL.  Tramite la sintassi delle espressioni di query è possibile eseguire anche complesse operazioni di filtro, ordinamento e raggruppamento sulle origini dati usando una quantità minima di codice.  Per altre informazioni, vedere [Operazioni di query di base \(Visual Basic\)](../Topic/Basic%20Query%20Operations%20\(Visual%20Basic\).md).  Per esempi che illustrano come usare la sintassi delle espressioni di query, vedere gli argomenti seguenti:  
  
-   [Esempi di sintassi delle espressione di query: proiezione](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-projection.md)  
  
-   [Esempi di sintassi delle espressione di query: filtro](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-filtering.md)  
  
-   [Esempi di sintassi delle espressione di query: ordinamento](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-ordering.md)  
  
-   [Esempi di sintassi delle espressioni di query: operatori di aggregazione](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-aggregate-operators.md)  
  
-   [Esempi di sintassi delle espressione di query: partizionamento](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-partitioning.md)  
  
-   [Esempi di sintassi delle espressioni di query: operatori di join](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-join-operators.md)  
  
-   [Esempi di sintassi delle espressioni di query: operatori sugli elementi](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-element-operators.md)  
  
-   [Esempi di sintassi delle espressione di query: raggruppamento](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-grouping.md)  
  
-   [Esempi di sintassi delle espressioni di query: navigazione tra relazioni](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expression-syntax-examples-navigating-relationships.md)  
  
### Sintassi delle query basate su metodo  
 Per comporre query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)], è inoltre possibile usare query basate su metodo.  La sintassi delle query basate su metodo è costituita da una sequenza di chiamate dirette ai metodi dell'operatore LINQ, in cui come parametri vengono passate espressioni lambda.  Per altre informazioni, vedere [Espressioni lambda](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md).  Per esempi che illustrano come usare la sintassi delle query basate su metodo, consultare gli argomenti seguenti:  
  
-   [Esempi di sintassi delle query basate su metodo: proiezione](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-projection.md)  
  
-   [Esempi di sintassi delle query basate su metodo: filtro](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-filtering.md)  
  
-   [Esempi di sintassi delle query basate su metodo: ordinamento](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-ordering.md)  
  
-   [Esempi di sintassi delle query basate su metodo: operatori di aggregazione](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-aggregate-operators.md)  
  
-   [Esempi di sintassi delle query basate su metodo: partizionamento](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-partitioning.md)  
  
-   [Esempi di sintassi delle query basate su metodo: conversione](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-conversion.md)  
  
-   [Esempi di sintassi delle query basate su metodo: operatori di join](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-join-operators.md)  
  
-   [Esempi di sintassi delle query basate su metodo: operatori sugli elementi](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-element-operators.md)  
  
-   [Esempi di sintassi delle query basate su metodo: raggruppamento](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-grouping.md)  
  
-   [Esempi di sintassi delle query basate su metodo: navigazione tra relazioni](../../../../../../docs/framework/data/adonet/ef/language-reference/method-based-query-syntax-examples-navigating-relationships.md)  
  
## Vedere anche  
 [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)   
 [Getting Started with LINQ in C\#](../Topic/Getting%20Started%20with%20LINQ%20in%20C%23.md)   
 [Getting Started with LINQ in Visual Basic](../Topic/Getting%20Started%20with%20LINQ%20in%20Visual%20Basic.md)   
 [Opzioni di unione di Entity Framework e query compilate](http://go.microsoft.com/fwlink/?LinkId=199591)