---
title: Relazioni tra i tipi nelle operazioni di query LINQ (C#) | Documentazione Microsoft
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
- inferring type information [LINQ in C#]
- data sources [LINQ in C#], type relationships
- queries [LINQ in C#], type relationships
- relationships [LINQ in C#]
- type relationships [LINQ in C#]
- variable relationships [LINQ in C#]
- type information inferred [LINQ in C#]
- data transformations [LINQ in C#]
- LINQ [C#], type relationships
ms.assetid: 99118938-d47c-4d7e-bb22-2657a9f95268
caps.latest.revision: 25
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
ms.openlocfilehash: ad52663fb54ee1adc06a084d26abb3e6ce46e2af
ms.lasthandoff: 03/13/2017

---
# <a name="type-relationships-in-linq-query-operations-c"></a>Relazioni tra i tipi nelle operazioni di query LINQ (C#)
Per scrivere le query in modo efficace, è necessario comprendere in che modo i tipi di variabili in un'operazione di query completa interagiscono tra loro. Conoscendo queste relazioni, si comprenderanno più facilmente gli esempi di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] e di codice nella documentazione. In aggiunta, è possibile comprendere che cosa accade dietro le quinte quando le variabili vengono tipizzate in modo implicito tramite `var`.  
  
 Le operazioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]sono fortemente tipizzate nell'origine dati, nella query stessa e nell'esecuzione della query. Il tipo delle variabili nella query deve essere compatibile con il tipo degli elementi nell'origine dati e con il tipo della variabile di iterazione nell'istruzione `foreach`. Questa forte tipizzazione garantisce che gli errori di tipo vengono rilevati in fase di compilazione quando possono essere corretti prima di essere riscontrati dagli utenti.  
  
 Per illustrare tali relazioni del tipo, la maggior parte degli esempi che seguono usa la tipizzazione esplicita per tutte le variabili. Nell'ultimo esempio viene illustrato come si applichino gli stessi principi anche quando si usa la tipizzazione implicita tramite [var](../../../../csharp/language-reference/keywords/var.md).  
  
## <a name="queries-that-do-not-transform-the-source-data"></a>Query che non trasformano i dati di origine  
 La figura seguente mostra un'operazione di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] to Objects che non esegue alcuna trasformazione sui dati. L'origine contiene una sequenza di stringhe e anche l'output della query è una sequenza di stringhe.  
  
 ![Relazione dei tipi di dati in una query LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_flow1.png "LINQ_flow1")  
  
1.  L'argomento del tipo dell'origine dati determina il tipo della variabile di intervallo.  
  
2.  Il tipo di oggetto selezionato determina il tipo della variabile di query. Qui `name` è una stringa. La variabile di query è pertanto una `IEnumerable`\<string>.  
  
3.  La variabile di query viene iterata nell'istruzione `foreach`. Poiché la variabile di query è una sequenza di stringhe, anche la variabile di iterazione è una stringa.  
  
## <a name="queries-that-transform-the-source-data"></a>Query che trasformano i dati di origine  
 La figura seguente mostra un'operazione di query [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] che esegue una trasformazione sui dati di lieve entità. La query usa una sequenza di oggetti `Customer` come input e seleziona solo la proprietà `Name` nel risultato. Poiché `Name` è una stringa, la query genera una sequenza di stringhe come output.  
  
 ![Query che trasforma il tipo di dati](../../../../csharp/programming-guide/concepts/linq/media/linq_flow2.png "LINQ_flow2")  
  
1.  L'argomento del tipo dell'origine dati determina il tipo della variabile di intervallo.  
  
2.  L'istruzione `select` restituisce la proprietà `Name` invece dell'oggetto `Customer` completo. Poiché `Name` è una stringa, l'argomento del tipo `custNameQuery` è `string` e non `Customer`.  
  
3.  Poiché `custNameQuery` è una sequenza di stringhe, anche la variabile di iterazione del ciclo `foreach` del ciclo deve essere una `string`.  
  
 La figura seguente mostra una trasformazione leggermente più complessa. L'istruzione `select` restituisce un tipo anonimo che acquisisce solo due membri dell'oggetto di origine `Customer`.  
  
 ![Query che trasforma il tipo di dati](../../../../csharp/programming-guide/concepts/linq/media/linq_flow3.png "LINQ_flow3")  
  
1.  L'argomento del tipo dell'origine dati è sempre il tipo della variabile di intervallo nella query.  
  
2.  Poiché l'istruzione `select` produce un tipo anonimo, la variabile di query deve essere tipizzata in modo implicito tramite `var`.  
  
3.  Poiché il tipo della variabile di query è implicito, anche la variabile di iterazione nel ciclo `foreach` deve essere implicita.  
  
## <a name="letting-the-compiler-infer-type-information"></a>Deduzione delle informazioni sul tipo tramite il compilatore  
 Sebbene sia necessario comprendere le relazioni di tipo in un'operazione di query, è possibile scegliere di far eseguire al compilatore tutto il lavoro al posto dell'utente. La parola chiave [var](../../../../csharp/language-reference/keywords/var.md) può essere usata per qualsiasi variabile locale in un'operazione di query. La figura seguente è simile all'esempio 2 illustrato in precedenza. Il compilatore fornisce, tuttavia, il tipo forte per ogni variabile nell'operazione di query.  
  
 ![Flusso di tipo con tipizzazione implicita](../../../../csharp/programming-guide/concepts/linq/media/linq_flow4.png "LINQ_flow4")  
  
 Per altre informazioni su `var`, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni di base su LINQ in C#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)
