---
title: "Espressioni di query LINQ (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Linguaggio C#, espressioni di query LINQ"
  - "espressioni [C#], espressioni di query LINQ"
  - "LINQ [C#], espressioni nelle query"
  - "query [LINQ in C#], espressioni nelle query"
  - "query (espressioni) [LINQ in C#]"
ms.assetid: 40638f19-fb46-4d26-a2d9-a383b48f5ed4
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Espressioni di query LINQ (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

[!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext_md.md)] è il nome di un set di tecnologie basate sull'integrazione di funzionalità di query direttamente nel linguaggio C\# \(anche in Visual Basic e potenzialmente in qualsiasi altro linguaggio .NET\).  Con [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], una query è un costrutto di linguaggio di prima categoria, esattamente come le classi, i metodi, gli eventi e così via.  
  
 Per uno sviluppatore che scrive query, la parte "integrata nel linguaggio" più visibile di [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] è l'espressione di query.  Le espressioni di query sono scritte in una *sintassi di query* dichiarativa introdotta in C\# 3.0.  Tramite la sintassi di query, è persino possibile eseguire operazioni di filtro, ordinamento e raggruppamento complesse su origini dati con una quantità minima di codice.  Si utilizzano gli stessi modelli di espressioni di query di base per eseguire query e trasformare dati in database SQL, set di dati [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado_md.md)], documenti e flussi XML e raccolte .NET.  
  
 Nell'esempio seguente viene illustrata l'operazione di query completa.  L'operazione completa include la creazione di un'origine dati, la definizione dell'espressione di query e l'esecuzione della query in un 'istruzione `foreach`.  
  
 [!code-cs[csProgGuideLINQ#11](../../../csharp/programming-guide/arrays/codesnippet/CSharp/index_1.cs)]  
  
 Per ulteriori informazioni sulle nozioni di base di [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] in C\#, vedere [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md).  
  
## Cenni preliminari sulle espressioni di query  
  
-   Le espressioni di query possono essere utilizzate per eseguire una query e trasformare dati da qualsiasi origine dati abilitata per [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].  Una sola query, ad esempio, è in grado di recuperare dati da un database SQL e di produrre un flusso XML come output.  
  
-   Le espressioni di query sono facili da gestire perché utilizzano molti costrutti di linguaggio C\# comuni.  Per ulteriori informazioni, vedere [Getting Started with LINQ in C\#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md).  
  
-   Le variabili in un'espressione di query sono tutte fortemente tipizzate, anche se in molti casi non è necessario specificare il tipo in modo esplicito perché il compilatore è in grado di dedurlo.  Per ulteriori informazioni, vedere [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
-   Una query non viene eseguita finché non viene eseguita un'iterazione sulla variabile di query in un'istruzione `foreach`.  Per ulteriori informazioni, vedere la classe [Introduction to LINQ Queries \(C\#\)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
-   In fase di compilazione, le espressioni di query vengono convertite in chiamate al metodo dell'operatore query standard secondo le regole definite nella specifica C\#.  Le query che possono essere espresse utilizzando la sintassi della query possono essere espresse anche utilizzando la sintassi del metodo.  Tuttavia, nella maggior parte dei casi la sintassi della query è più leggibile e concisa.  Per ulteriori informazioni, vedere [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md) e [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
-   Come regola di scrittura delle query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)], si consiglia di utilizzare la sintassi della query ogni qualvolta è possibile e la sintassi del metodo ogni qualvolta è necessario.  Tra le due diverse forme non esiste differenza semantica o a livello di prestazioni.  Le espressioni di query sono spesso più leggibili delle espressioni equivalenti scritte nella sintassi del metodo.  
  
-   Poiché per alcune operazioni di query, ad esempio <xref:System.Linq.Enumerable.Count%2A> o <xref:System.Linq.Enumerable.Max%2A>, non esiste una clausola dell'espressione di query equivalente, è necessario esprimerle come chiamata al metodo.  La sintassi del metodo può essere combinata con la sintassi della query in svariati modi.  Per ulteriori informazioni, vedere [Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
-   Le espressioni di query possono essere compilate in strutture ad albero dell'espressione o in delegati, a seconda del tipo al quale viene applicata la query.  Le query <xref:System.Collections.Generic.IEnumerable%601> vengono compilate in delegati.  Le query <xref:System.Linq.IQueryable> e <xref:System.Linq.IQueryable%601> vengono compilate in strutture ad albero dell'espressione.  Per ulteriori informazioni, vedere [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Nella tabella seguente sono elencati gli argomenti in cui sono disponibili informazioni aggiuntive sulle query ed esempi di codice per le attività comuni.  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|[Nozioni fondamentali sulle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/query-expression-basics.md)|Sono introdotti i concetti fondamentali sulle query e vengono forniti esempi di sintassi della query C\#.|  
|[Procedura: scrivere query LINQ in C\#](../../../csharp/programming-guide/linq-query-expressions/how-to-write-linq-queries.md)|Sono forniti esempi di diversi tipi di base di espressioni di query.|  
|[Procedura: gestire le eccezioni nelle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)|Come e quando spostare codice che genera potenziali eccezioni al di fuori di un'espressione di query.|  
|[How to: Populate Object Collections from Multiple Sources \(LINQ\)](../Topic/How%20to:%20Populate%20Object%20Collections%20from%20Multiple%20Sources%20\(LINQ\).md)|Come utilizzare l'istruzione `select` per unire dati da origini diverse in un nuovo tipo.|  
|[Procedura: raggruppare i risultati di una query](../../../csharp/programming-guide/linq-query-expressions/how-to-group-query-results.md)|Vengono illustrati diversi modi per utilizzare la clausola `group`.|  
|[Procedura: creare un gruppo annidato](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)|Viene illustrato come creare gruppi annidati.|  
|[Procedura: eseguire una sottoquery su un'operazione di raggruppamento](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)|Viene illustrato come utilizzare una sottoespressione in una query come origine dati per una query nuova.|  
|[Procedura: raggruppare i risultati per chiavi contigue](../../../csharp/programming-guide/linq-query-expressions/how-to-group-results-by-contiguous-keys.md)|Viene illustrato come implementare un operatore di query standard thread\-safe in grado di eseguire operazioni di raggruppamento in origini dati di flusso.|  
|[Procedura: specificare dinamicamente i filtri dei predicati in fase di esecuzione](../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)|Viene illustrato come specificare un numero arbitrario di valori da utilizzare nei confronti di uguaglianza in una clausola `where`.|  
|[Procedura: Archiviare i risultati di una query in memoria](../../../csharp/programming-guide/linq-query-expressions/how-to-store-the-results-of-a-query-in-memory.md)|Viene illustrato come materializzare e archiviare i risultati della query senza utilizzare necessariamente un ciclo `foreach`.|  
|[Procedura: ottenere una query da un metodo](../../../csharp/programming-guide/linq-query-expressions/how-to-return-a-query-from-a-method.md)|Viene illustrato come restituire variabili di query dai metodi e come passarle ai metodi come parametri di input.|  
|[Procedura: eseguire operazioni di join personalizzate](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)|Viene illustrato come eseguire operazioni di join basate su qualsiasi tipo di funzione predicativa.|  
|[Procedura: eseguire un join utilizzando una chiave composta](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)|Viene illustrato come unire due origini basate su più di una chiave corrispondente.|  
|[Procedura: ordinare i risultati di una clausola join](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)|Viene illustrato come ordinare una sequenza prodotta da un'operazione di join.|  
|[Procedura: eseguire degli inner join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)|Viene illustrato come eseguire un inner join in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].|  
|[Procedura: eseguire dei join raggruppati](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)|Viene illustrato come produrre un join raggruppato in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].|  
|[Procedura: Eseguire i left outer join](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)|Viene illustrato come produrre un left outer join in [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].|  
|[Procedura: gestire valori null nelle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-null-values-in-query-expressions.md)|Viene illustrato come gestire valori null nelle query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)].|  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Walkthrough: Writing Queries in C\#](../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [Basic LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)   
 [Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)   
 [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Funzionamento delle query LINQ to Objects](http://go.microsoft.com/fwlink/?LinkId=112389)   
 [Lettura e scrittura di query](http://go.microsoft.com/fwlink/?LinkId=112391)   
 [Informazioni sulle raccolte](http://go.microsoft.com/fwlink/?LinkId=112394)   
 [Semplicità di collegamento: un elenco di provider LINQ](http://go.microsoft.com/fwlink/?LinkId=112411)