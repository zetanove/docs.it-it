---
title: LINQ (Language-Integrated Query) (C#) | Microsoft Docs
ms.custom: 
ms.date: 02-02-2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 19dd1782-905b-4a9d-a3e9-618453037fa2
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a97cdc61caf2cd9d1f71a6763e4903bb5a5fdc54
ms.lasthandoff: 03/13/2017

---

# <a name="language-integrated-query-linq"></a>LINQ (Language-Integrated Query)

LINQ (Language-Integrated Query) è il nome di un set di tecnologie basate sull'integrazione delle funzionalità di query direttamente nel linguaggio C#. In genere, le query sui dati vengono espresse come stringhe semplici senza il controllo dei tipi in fase di compilazione o il supporto di IntelliSense. È anche necessario imparare un linguaggio di query diverso per ogni tipo di origine dati: database SQL, documenti XML, svariati servizi Web e così via. Con LINQ, una query è un costrutto del linguaggio di prima classe, come le classi, i metodi e gli eventi.

Per uno sviluppatore che scrive query, la parte integrata nel linguaggio più visibile di LINQ è l'espressione di query. Le espressioni di query vengono scritte con una *sintassi di query* dichiarativa. Tramite la sintassi di query è possibile eseguire operazioni di filtro, ordinamento e raggruppamento sulle origini dati usando una quantità minima di codice. Vengono usati gli stessi modelli di espressioni di query di base per eseguire una query e trasformare i dati in database SQL, set di dati ADO .NET, documenti e flussi XML e raccolte .NET.

L'esempio seguente mostra l'operazione di query completa. L'operazione completa include la creazione di un'origine dati, la definizione dell'espressione di query e l'esecuzione della query in un'istruzione `foreach`.

[!code-cs[csProgGuideLINQ#11](../../../../../samples/snippets/csharp/concepts/linq/index_1.cs)]

## <a name="query-expression-overview"></a>Panoramica sulle espressioni di query

-   Le espressioni di query possono essere usate per eseguire una query e trasformare dati da qualsiasi origine dati abilitata per LINQ. Una sola query, ad esempio, è in grado di recuperare dati da un database SQL e di produrre un flusso XML come output.  
  
-   Le espressioni di query sono facili da gestire perché usano molti costrutti di linguaggio C# di uso comune.  
  
-   Le variabili presenti in un'espressione di query sono tutte fortemente tipizzate, anche se in molti casi non è necessario specificare il tipo in modo esplicito perché il compilatore è in grado di dedurlo. Per altre informazioni, vedere [Relazioni tra i tipi nelle operazioni di query LINQ](type-relationships-in-linq-query-operations.md).  
  
-   Una query non viene eseguita finché non si esegue l'iterazione della variabile di query, ad esempio in un'istruzione `foreach`. Per altre informazioni, vedere [Introduzione alle query LINQ](introduction-to-linq-queries.md).  
  
-   In fase di compilazione, le espressioni di query vengono convertite in chiamate al metodo dell'operatore query standard secondo le regole definite nella specifica C#. Le query che possono essere espresse usando la sintassi di query possono essere espresse anche usando la sintassi dei metodi. Nella maggior parte dei casi, tuttavia, la sintassi di query è più leggibile e concisa. Per altre informazioni, vedere [Specifiche del linguaggio C#](../../../language-reference/language-specification.md) e [Panoramica degli operatori di query standard](standard-query-operators-overview.md).  
  
-   Come regola di scrittura delle query LINQ, è consigliabile usare la sintassi di query quando possibile e la sintassi dei metodi quando necessario. Tra le due diverse forme non esiste differenza semantica o a livello di prestazioni. Le espressioni di query sono spesso più leggibili delle espressioni equivalenti scritte nella sintassi dei metodi.  
  
-   Per alcune espressioni di query, ad esempio <xref:System.Linq.Enumerable.Count%2A> o <xref:System.Linq.Enumerable.Max%2A>, non è presente una clausola dell'espressione di query equivalente. Tali espressioni devono quindi essere espresse come chiamata di metodo. La sintassi dei metodi può essere combinata con la sintassi di query in diversi modi. Per altre informazioni, vedere [Sintassi di query e sintassi di metodi in LINQ](query-syntax-and-method-syntax-in-linq.md).  
  
-   Le espressioni di query possono essere compilate in alberi delle espressioni o in delegati, a seconda del tipo al quale viene applicata la query. Le query <xref:System.Collections.Generic.IEnumerable%601> vengono compilate in delegati. Le query <xref:System.Linq.IQueryable> e <xref:System.Linq.IQueryable%601> vengono compilate in alberi delle espressioni. Per altre informazioni, vedere [Alberi delle espressioni](../../../expression-trees.md).  

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni dettagliate su LINQ, iniziare ad acquisire dimestichezza con alcuni concetti di base nella sezione introduttiva [Nozioni fondamentali sulle espressioni di query](../../../linq/query-expression-basics.md) e quindi leggere la documentazione per la tecnologia LINQ a cui si è interessati:   
-   Documenti XML: [LINQ to XML](linq-to-xml.md)  
  
-   ADO.NET Entity Framework: [LINQ to Entities](http://msdn.microsoft.com/library/641f9b68-9046-47a1-abb0-1c8eaeda0e2d)  
  
-   Raccolte .NET, file, stringhe e così via: [LINQ to Objects](linq-to-objects.md)

Per approfondire LINQ in generale, vedere [LINQ in C#](../../../linq/linq-in-csharp.md).

Per iniziare a lavorare con LINQ in C#, vedere l'esercitazione [Uso di LINQ](../../../tutorials/working-with-linq.md).




