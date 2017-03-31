---
title: Operazioni di query LINQ di base (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- orderby clause [LINQ in C#]
- ordering data [LINQ in C#]
- selecting data [LINQ in C#]
- queries [LINQ in C#], basic operations
- grouping data [LINQ in C#]
- data sources [LINQ in C#]
- sorting data [LINQ in C#]
- projections [LINQ in C#]
- filtering data [LINQ in C#]
- joining data [LINQ in C#]
- select clause [LINQ in C#]
- LINQ [C#], basic query operations
- join clause [LINQ in C#]
- group clause [LINQ in C#]
ms.assetid: a7ea3421-1cf4-4df7-832a-aa22fe6379e9
caps.latest.revision: 39
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 48624d608c3eb8d1118a2492454595d46025cb3e
ms.lasthandoff: 03/13/2017

---
# <a name="basic-linq-query-operations-c"></a>Operazioni di query LINQ di base (C#)
Questo argomento offre una breve introduzione alle espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] e ad alcuni tipi di operazioni specifiche eseguite in una query. Informazioni più specifiche sono disponibili negli argomenti seguenti:  
  
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)  
  
 [Panoramica degli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
  
 [Procedura dettagliata: scrittura di query in C#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)  
  
> [!NOTE]
>  Se si ha già familiarità con un linguaggio di query, ad esempio SQL o XQuery, è possibile ignorare la maggior parte di questo argomento. Leggere la sezione sulla "clausola `from`" più avanti per informazioni sull'ordine delle clausole nelle espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  
  
## <a name="obtaining-a-data-source"></a>Ottenere un'origine dei dati  
 In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], il primo passaggio consiste nella specifica dell'origine dei dati. In C#, come nella maggior parte dei linguaggi di programmazione, una variabile deve essere dichiarata prima di essere usata. In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], la clausola `from` viene dichiarata per prima per introdurre l'origine dei dati (`customers`) e la *variabile di intervallo* (`cust`).  
  
 [!code-cs[csLINQGettingStarted#23](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_1.cs)]  
  
 La variabile di intervallo è come la variabile di iterazione in un ciclo `foreach` ad eccezione del fatto che non si verifica alcuna iterazione in un'espressione di query. Quando viene eseguita la query, la variabile di intervallo verrà usata come riferimento a ogni elemento successivo in `customers`. Poiché il compilatore può dedurre il tipo di `cust`, non è necessario specificarlo in modo esplicito. Altre variabili di intervallo possono essere introdotte da una clausola `let`. Per altre informazioni, vedere [Clausola let](../../../../csharp/language-reference/keywords/let-clause.md).  
  
> [!NOTE]
>  Per origini di dati non generici, ad esempio <xref:System.Collections.ArrayList>, la variabile di intervallo deve essere digitata in modo esplicito. Per altre informazioni, vedere [Procedura: Eseguire una query su un ArrayList con LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md) e [Clausola from](../../../../csharp/language-reference/keywords/from-clause.md).  
  
## <a name="filtering"></a>Filtro  
 Probabilmente l'operazione di query più comune consiste nell'applicazione di un filtro sotto forma di espressione booleana. Il filtro fa in modo che la query restituisca solo gli elementi per i quali l'espressione è vera. Il risultato viene generato utilizzando la clausola `where`. Il filtro in realtà specifica gli elementi da escludere dalla sequenza di origine. Nell'esempio seguente vengono restituiti solo i `customers` che hanno un indirizzo in Londra.  
  
 [!code-cs[csLINQGettingStarted#24](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_2.cs)]  
  
 È possibile usare gli operatori logici `AND` e `OR` di C# per applicare tutte le espressioni necessarie nella clausola `where`. Ad esempio, per restituire solo i clienti in "Londra" `AND` che si chiamano "Devon", si scrive il codice seguente:  
  
 [!code-cs[csLINQGettingStarted#25](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_3.cs)]  
  
 Per restituire i clienti di Londra o Parigi, si scrive il codice seguente:  
  
 [!code-cs[csLINQGettingStarted#26](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_4.cs)]  
  
 Per altre informazioni, vedere [Clausola where](../../../../csharp/language-reference/keywords/where-clause.md).  
  
## <a name="ordering"></a>Ordering  
 È spesso utile ordinare i dati restituiti. La clausola `orderby` ordinerà gli elementi della sequenza restituita in base all'operatore di confronto per il tipo che si sta ordinando. Ad esempio, la query seguente può essere estesa per ordinare i risultati basati sulla proprietà `Name`. Poiché `Name` è una stringa, l'operatore di confronto esegue un ordinamento alfabetico da A a Z.  
  
 [!code-cs[csLINQGettingStarted#27](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_5.cs)]  
  
 Per ordinare i risultati in ordine inverso, da Z ad A, usare la clausola `orderby…descending`.  
  
 Per altre informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).  
  
## <a name="grouping"></a>Raggruppamento  
 La clausola `group` consente di raggruppare i risultati in base a una chiave specificata. Ad esempio, è possibile specificare che i risultati devono essere raggruppati in base a `City` in modo che tutti i clienti di Londra o Parigi siano elencati in gruppi individuali. In questo caso, `cust.City` è la soluzione.  
  
 [!code-cs[csLINQGettingStarted#28](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_6.cs)]  
  
 Quando si termina una query con una clausola `group`, i risultati vengono rappresentati come un elenco di elenchi. Ogni elemento nell'elenco è un oggetto che ha un membro `Key` e un elenco di elementi che sono raggruppati sotto tale chiave. Quando si esegue l'iterazione di una query che produce una sequenza di gruppi, è necessario usare un ciclo `foreach` annidato. Il ciclo esterno esegue l'iterazione di ogni gruppo e il ciclo interno esegue l'iterazione dei membri di ogni gruppo.  
  
 Se è necessario fare riferimento ai risultati di un'operazione di gruppo, è possibile usare la parola chiave `into` per creare un identificatore sul quale eseguire query addizionali. La query seguente restituisce solo i gruppi che contengono più di due clienti:  
  
 [!code-cs[csLINQGettingStarted#29](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_7.cs)]  
  
 Per altre informazioni, vedere [Clausola group](../../../../csharp/language-reference/keywords/group-clause.md).  
  
## <a name="joining"></a>Uso di join  
 Le operazioni di join creano associazioni tra le sequenze che non sono modellate in modo esplicito nelle origini dei dati. Ad esempio, è possibile eseguire un join per trovare tutti i clienti e i distributori che hanno la stessa ubicazione. In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], la clausola `join` usa sempre raccolte di oggetti anziché direttamente le tabelle di database.  
  
 [!code-cs[csLINQGettingStarted#36](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_8.cs)]  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] non è necessario usare `join` così spesso come in SQL poiché le chiavi esterne in [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sono rappresentate nel modello a oggetti come proprietà che contengono una raccolta di elementi. Ad esempio, un oggetto `Customer` contiene una raccolta di oggetti `Order`. Anziché eseguire un join, si accede agli ordini usando la notazione "Dot":  
  
```  
from order in Customer.Orders...  
```  
  
 Per altre informazioni, vedere [Clausola join](../../../../csharp/language-reference/keywords/join-clause.md).  
  
## <a name="selecting-projections"></a>Selezione (proiezioni)  
 La clausola `select` produce i risultati della query e specifica la "forma" o un tipo di ogni elemento restituito. Ad esempio, è possibile specificare se i risultati saranno costituiti di oggetti `Customer` completi, di un solo membro, di un subset di membri, oppure un tipo di risultato completamente diverso basato su un calcolo o su una creazione nuova di oggetti. Quando la clausola `select` produce un valore diverso da una copia dell'elemento d'origine, l'operazione viene chiamata *proiezione*. L'uso di proiezioni per trasformare i dati è una funzionalità efficace delle espressioni delle query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]. Per altre informazioni, vedere [Trasformazioni dati con LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md) e [Clausola select](../../../../csharp/language-reference/keywords/select-clause.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione all'uso di LINQ in C#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Procedura dettagliata: scrittura di query in C#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [Parole chiave di query (LINQ)](../../../../csharp/language-reference/keywords/query-keywords.md)   
 [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
