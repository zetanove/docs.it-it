---
title: "Type Relationships in LINQ Query Operations (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "inferring type information [LINQ in C#]"
  - "data sources [LINQ in C#], type relationships"
  - "queries [LINQ in C#], type relationships"
  - "relationships [LINQ in C#]"
  - "type relationships [LINQ in C#]"
  - "variable relationships [LINQ in C#]"
  - "type information inferred [LINQ in C#]"
  - "data transformations [LINQ in C#]"
  - "LINQ [C#], type relationships"
ms.assetid: 99118938-d47c-4d7e-bb22-2657a9f95268
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 23
---
# Type Relationships in LINQ Query Operations (C#)
Per scrivere le query in modo corretto, è necessario comprendere il modo in cui i tipi delle variabili in un'operazione di query interagiscono tra loro.  Se si comprendono queste relazioni si comprenderanno più facilmente gli esempi [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] e gli esempi di codice presenti nella documentazione.  Si comprenderanno inoltre le operazioni eseguite automaticamente quando le variabili vengono tipizzate in modo implicito utilizzando `var`.  
  
 Le operazioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] sono fortemente tipizzate nell'origine dati, nella query stessa e nell'esecuzione della query.  Il tipo delle variabili nella query deve essere compatibile con il tipo degli elementi nell'origine dati e con il tipo della variabile di iterazione nell'istruzione `foreach`.  Questa tipizzazione forte consente di rilevare gli errori di tipo in fase di compilazione quando possono essere corretti prima che vengano riscontrati dagli utenti.  
  
 Per illustrare queste relazioni tra i tipi, nella maggior parte degli esempi riportati di seguito viene utilizzata la tipizzazione esplicita per tutte le variabili.  Nell'ultimo esempio viene illustrato come valgono gli stessi principi anche quando viene utilizzata la tipizzazione implicita mediante [var](../../../../csharp/language-reference/keywords/var.md).  
  
## Query che non trasformano i dati di origine  
 Nella figura seguente viene illustrata un'operazione di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] to Objects che non esegue alcuna trasformazione sui dati.  L'origine contiene una sequenza di stringhe e anche l'output della query è una sequenza di stringhe.  
  
 ![Relazione dei tipi di dati in una query LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq-flow1.png "LINQ\_flow1")  
  
1.  L'argomento del tipo dell'origine dati determina il tipo della variabile di intervallo.  
  
2.  Il tipo dell'oggetto selezionato determina il tipo della variabile di query.  In questo caso `name` è una stringa.  Pertanto, la variabile di query è una `IEnumerable`\<stringa\>.  
  
3.  La variabile di query viene scorsa nell'istruzione `foreach`.  Poiché la variabile di query è una sequenza di stringhe, anche la variabile di iterazione è una stringa.  
  
## Query che trasformano i dati di origine  
 Nella figura seguente viene illustrata un'operazione di query [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)] che esegue una trasformazione semplice sui dati.  La query utilizza una sequenza di oggetti `Customer` come input e seleziona solo la proprietà `Name` nel risultato.  Poiché `Name` è una stringa, la query genera una sequenza di stringhe come output.  
  
 ![Query che trasforma il tipo di dati](../../../../csharp/programming-guide/concepts/linq/media/linq-flow2.png "LINQ\_flow2")  
  
1.  L'argomento del tipo dell'origine dati determina il tipo della variabile di intervallo.  
  
2.  L'istruzione `select` restituisce la proprietà `Name` invece dell'intero oggetto `Customer`.  Poiché `Name` è una stringa, l'argomento del tipo di `custNameQuery` è `string`, non `Customer`.  
  
3.  Poiché `custNameQuery` è una sequenza di stringhe, anche la variabile di iterazione del ciclo `foreach` deve essere `string`.  
  
 Nella figura seguente viene illustrata una trasformazione leggermente più complessa.  L'istruzione `select` restituisce un tipo anonimo che acquisisce solo due membri dell'oggetto `Customer` originale.  
  
 ![Query che trasforma il tipo di dati](../../../../csharp/programming-guide/concepts/linq/media/linq-flow3.png "LINQ\_flow3")  
  
1.  L'argomento del tipo dell'origine dati è sempre il tipo della variabile di intervallo nella query.  
  
2.  Poiché l'istruzione `select` genera un tipo anonimo, la variabile di query deve essere tipizzata in modo implicito utilizzando `var`.  
  
3.  Poiché il tipo della variabile di query è implicito, anche la variabile di iterazione nel ciclo `foreach` deve essere implicita.  
  
## Deduzione delle informazioni sul tipo tramite il compilatore  
 Sebbene sia necessario comprendere le relazioni tra i tipi in un'operazione di query, è possibile consentire al compilatore di svolgere tutte le operazioni autonomamente.  La parola chiave [var](../../../../csharp/language-reference/keywords/var.md) può essere utilizzata per qualsiasi variabile locale in un'operazione di query.  La figura seguente è simile a quella riportata nel secondo esempio illustrato precedentemente.  Tuttavia, il compilatore fornisce il tipo forte per ogni variabile nell'operazione di query.  
  
 ![Flusso di tipo con tipizzazione implicita](../../../../csharp/programming-guide/concepts/linq/media/linq-flow4.png "LINQ\_flow4")  
  
 Per ulteriori informazioni su `var`, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## Vedere anche  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Type Relationships in Query Operations \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)