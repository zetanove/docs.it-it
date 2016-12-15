---
title: "Basic LINQ Query Operations (C#) | Microsoft Docs"
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
  - "orderby clause [LINQ in C#]"
  - "ordering data [LINQ in C#]"
  - "selecting data [LINQ in C#]"
  - "queries [LINQ in C#], basic operations"
  - "grouping data [LINQ in C#]"
  - "data sources [LINQ in C#]"
  - "sorting data [LINQ in C#]"
  - "projections [LINQ in C#]"
  - "filtering data [LINQ in C#]"
  - "joining data [LINQ in C#]"
  - "select clause [LINQ in C#]"
  - "LINQ [C#], basic query operations"
  - "join clause [LINQ in C#]"
  - "group clause [LINQ in C#]"
ms.assetid: a7ea3421-1cf4-4df7-832a-aa22fe6379e9
caps.latest.revision: 39
caps.handback.revision: 37
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Basic LINQ Query Operations (C#)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene fornita una breve introduzione alle espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] e ad alcune operazioni comuni eseguite in una query.  Informazioni più dettagliate vengono fornite negli argomenti seguenti:  
  
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)  
  
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)  
  
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)  
  
> [!NOTE]
>  Se si ha già dimestichezza con un linguaggio di query, ad esempio SQL o XQuery, è possibile saltare la maggior parte di questo argomento.  Per informazioni sull'ordine delle clausole nelle espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], consultare la "clausola `from`" nella sezione successiva.  
  
## Come ottenere l'origine dati  
 In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] il primo passaggio consiste nello specificare l'origine dati.  In C\#, come nella maggior parte dei linguaggi di programmazione, per poter utilizzare una variabile è necessario prima dichiararla.  In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] la clausola `from` deve essere specificata per prima per poter introdurre l'origine dati \(`customers`\) e la *variabile di intervallo* \(`cust`\).  
  
 [!code-cs[csLINQGettingStarted#23](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_1.cs)]  
  
 La variabile di intervallo è simile alla variabile di iterazione in un ciclo `foreach`, con la differenza che in un'espressione di query non si verifica un'effettiva iterazione.  Quando viene eseguita la query, la variabile di intervallo funge da riferimento per ogni elemento successivo in `customers`.  Poiché il compilatore è in grado di dedurre il tipo di `cust`, non è necessario specificarlo in modo esplicito.  È possibile introdurre ulteriori variabili di intervallo mediante la clausola `let`.  Per ulteriori informazioni, vedere [Clausola let](../../../../csharp/language-reference/keywords/let-clause.md).  
  
> [!NOTE]
>  Per le origini dati non generiche, ad esempio <xref:System.Collections.ArrayList>, la variabile di intervallo deve essere tipizzata in modo esplicito.  Per ulteriori informazioni, vedere [How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md) e [Clausola from](../../../../csharp/language-reference/keywords/from-clause.md).  
  
## Filtraggio  
 Probabilmente l'operazione di query più comune consiste nell'applicazione di un filtro sotto forma di espressione booleana.  Il filtro consente alla query di restituire solo gli elementi per i quali l'espressione sia true.  Il risultato viene generato utilizzando la clausola `where`.  Il filtro attivo specifica gli elementi da escludere dalla sequenza di origine.  Nell'esempio seguente vengono restituiti solo gli oggetti `customers` con un indirizzo di Londra.  
  
 [!code-cs[csLINQGettingStarted#24](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_2.cs)]  
  
 È possibile utilizzare i comuni operatori logici `AND` e `OR` in C\# per applicare tutte le espressioni di filtro necessarie nella clausola `where`.  Per restituire, ad esempio, solo i clienti di "Londra" di nome "Davon" mediante l'operatore `AND`, utilizzare il codice seguente:  
  
 [!code-cs[csLINQGettingStarted#25](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_3.cs)]  
  
 Per restituire i clienti di Londra o Parigi, utilizzare il codice seguente:  
  
 [!code-cs[csLINQGettingStarted#26](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_4.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola where](../../../../csharp/language-reference/keywords/where-clause.md).  
  
## Ordinamento  
 Spesso è utile ordinare i dati restituiti.  La clausola `orderby` consente di ordinare gli elementi presenti nella sequenza restituita in base all'operatore di confronto predefinito per il tipo da ordinare.  Ad esempio, la query seguente può essere estesa per ordinare i risultati in base alla proprietà `Name`.  Poiché `Name` è una stringa, l'operatore di confronto predefinito dispone i risultati in ordine alfabetico dalla A alla Z.  
  
 [!code-cs[csLINQGettingStarted#27](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_5.cs)]  
  
 Per disporre i risultati in ordine inverso, ovvero dalla Z alla A, utilizzare la clausola `orderby…descending`.  
  
 Per ulteriori informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).  
  
## Raggruppamento  
 La clausola `group` consente di raggruppare i risultati in base a una chiave specificata.  Ad esempio, è possibile specificare di raggruppare i risultati in base alla chiave `City` in modo che tutti i clienti di Londra o Parigi vengano suddivisi in singoli gruppi.  In tal caso, la chiave è `cust.City`.  
  
 [!code-cs[csLINQGettingStarted#28](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_6.cs)]  
  
 Quando si termina una query con la clausola `group`, i risultati vengono visualizzati sotto forma di elenco.  Ogni elemento nell'elenco è un oggetto che contiene un membro `Key` e un elenco di elementi raggruppati sotto quella chiave.  Quando si scorre una query che genera una sequenza di gruppi, è necessario utilizzare un ciclo `foreach` annidato.  Il ciclo esterno scorre ogni gruppo e il ciclo interno scorre i membri di ogni gruppo.  
  
 Se è necessario fare riferimento ai risultati di un'operazione di gruppo, è possibile utilizzare la parola chiave `into` per creare un identificatore su cui eseguire un'altra query.  Nella query seguente vengono restituiti solo i gruppi che contengono più di due clienti:  
  
 [!code-cs[csLINQGettingStarted#29](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_7.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola group](../../../../csharp/language-reference/keywords/group-clause.md).  
  
## Operazioni di join  
 Le operazioni di join creano associazioni tra sequenze che non vengono create in modo esplicito nelle origini dati.  È possibile ad esempio eseguire un join per cercare tutti i clienti e i concessionari che risiedono nella stessa località.  In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] la clausola `join` funziona sempre sulle raccolte di oggetti anziché direttamente sulle tabelle di database.  
  
 [!code-cs[csLINQGettingStarted#36](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_8.cs)]  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] non è necessario utilizzare `join` come in SQL poiché le chiavi esterne in [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sono rappresentate nel modello a oggetti come proprietà che contengono una raccolta di elementi.  Ad esempio, un oggetto `Customer` contiene una raccolta di oggetti `Order`.  Invece di eseguire un join, è possibile accedere agli ordini utilizzando la notazione del punto:  
  
```  
from order in Customer.Orders...  
```  
  
 Per ulteriori informazioni, vedere [Clausola join](../../../../csharp/language-reference/keywords/join-clause.md).  
  
## Selezione \(proiezioni\)  
 La clausola `select` genera i risultati della query e specifica la "forma" o il tipo di ogni elemento restituito.  Ad esempio, è possibile specificare se i risultati devono essere costituiti da oggetti `Customer` completi, solo da un membro, da un sottoinsieme di membri o da un tipo di risultati completamente diverso basato su un calcolo o sulla creazione di un nuovo oggetto.  Quando la clausola `select` genera un risultato diverso da una copia dell'elemento di origine, l'operazione viene denominata *proiezione*.  L'utilizzo delle proiezioni per la trasformazione dei dati è una funzionalità potente delle espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Per ulteriori informazioni, vedere [Trasformazioni dati con LINQ \(C\#\)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md) e [Clausola select](../../../../csharp/language-reference/keywords/select-clause.md).  
  
## Vedere anche  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [Parole chiave di query \(LINQ\)](../../../../csharp/language-reference/keywords/query-keywords.md)   
 [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)   
 [Operazioni di query di base \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)