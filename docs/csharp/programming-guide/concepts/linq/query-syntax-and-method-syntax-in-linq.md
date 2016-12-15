---
title: "Query Syntax and Method Syntax in LINQ (C#) | Microsoft Docs"
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
  - "LINQ [C#], query syntax vs. method syntax"
  - "queries [LINQ in C#], syntax comparisons"
ms.assetid: eedd6dd9-fec2-428c-9581-5b8783810ded
caps.latest.revision: 30
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Query Syntax and Method Syntax in LINQ (C#)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

La maggior parte delle query nella documentazione di query integrata linguaggio introduttivo \([!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]\) vengono scritti mediante la sintassi dichiarativa di query LINQ.  Tuttavia, la sintassi della query deve essere convertita in chiamate al metodo per Common Language Runtime \(CLR\) .NET quando il codice viene compilato.  Le chiamate al metodo include gli operatori di query standard, con nomi quali `Where`, `Select`, `GroupBy`, `Join`, `Max`e `Average`.  È possibile chiamarli direttamente utilizzando la sintassi del metodo anziché la sintassi della query.  
  
 La sintassi e la sintassi del metodo sono semanticamente sintassi persone con molta, ma identica di ricerca di query più semplice e più semplice da leggere.  Alcune query devono essere espressi come chiamate al metodo.  Ad esempio, è necessario utilizzare una chiamata al metodo per esprimere una query che recupera il numero di elementi che corrispondono a una condizione specificata.  È inoltre necessario utilizzare una chiamata al metodo per una query che recupera l'elemento con il valore massimo in una sequenza di origine.  Nella documentazione di riferimento per gli operatori di query standard dello spazio dei nomi <xref:System.Linq> viene utilizzata generalmente la sintassi del metodo.  Pertanto, anche quando si comincia a scrivere le query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], è utile acquisire dimestichezza con l'utilizzo della sintassi del metodo nelle query e nelle espressioni di query.  
  
## Metodi di estensione degli operatori di query standard  
 Nell'esempio seguente viene illustrata un'*espressione di query* semplice e la query equivalente a livello semantico scritta come *query basata sul metodo*.  
  
 [!code-cs[csLINQGettingStarted#22](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/query-syntax-and-method-syntax-in-linq_1.cs)]  
  
 L'output dei due esempi è identico.  Il tipo della variabile di query è uguale in entrambi i formati: <xref:System.Collections.Generic.IEnumerable%601>.  
  
 Per comprendere la query basata sul metodo, è utile esaminarla più dettagliatamente.  Sul lato destro dell'espressione la clausola `where` viene ora espressa come un metodo di istanza sull'oggetto `numbers` che, come descritto in precedenza, ha un tipo di `IEnumerable<int>`.  Se si ha dimestichezza con l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> generica, è noto che non dispone di un metodo `Where`.  Tuttavia, se si richiama l'elenco di completamento IntelliSense nell'IDE di Visual Studio, non solo sarà disponibile un metodo `Where`, ma molti altri metodi quali `Select`, `SelectMany`, `Join` e `Orderby`.  Questi sono tutti operatori di query standard.  
  
 ![Operatori query standard in Intellisense](../../../../csharp/programming-guide/concepts/linq/media/standardqueryops.png "StandardQueryOps")  
  
 Sebbene possa sembrare che <xref:System.Collections.Generic.IEnumerable%601> sia stato ridefinito per includere questi metodi aggiuntivi, di fatto non è così.  Gli operatori di query standard vengono implementati come un nuovo tipo di metodo denominato *metodo di estensione*.  I metodi di estensione "estendono" un tipo esistente e possono essere chiamati come se fossero metodi di istanza sul tipo.  Gli operatori di query standard estendono <xref:System.Collections.Generic.IEnumerable%601> ed è per questo motivo che è possibile scrivere  `numbers.Where(...)`.  
  
 Per iniziare a utilizzare [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], è importante comprendere come inserire i metodi di estensione nell'ambito dell'applicazione mediante le direttive `using` corrette.  Tale procedura viene illustrata anche in [How to: Create a LINQ Project](../Topic/How%20to:%20Create%20a%20LINQ%20Project.md).  Dal punto di vista dell'applicazione, un metodo di estensione e un metodo di istanza regolare sono uguali.  
  
 Per ulteriori informazioni sui metodi di estensione, vedere [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md).  Per ulteriori informazioni sugli operatori di query standard, vedere [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).  Alcuni provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], ad esempio [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], implementano operatori di query standard personalizzati e metodi di estensione aggiuntivi per altri tipi oltre a <xref:System.Collections.Generic.IEnumerable%601>.  
  
## Espressioni lambda  
 Nell'esempio precedente, si noti che l'espressione condizionale \(`num % 2 == 0`\) viene passata come argomento al metodo inline di `Where` : `Where(num => num % 2 == 0).`questa espressione in linea viene chiamato un'espressione lambda.  È il modo più semplice per scrivere il codice che altrimenti dovrebbe essere scritto in modo molto più complesso come metodo anonimo o delegato generico o come struttura ad albero dell'espressione.  In C\# `=>` è l'operatore lambda, che viene letto come "fino a".  `num` sulla sinistra dell'operatore è la variabile di input che corrisponde a `num` nell'espressione di query.  Il compilatore può dedurre il tipo di `num` poiché `numbers` è un tipo <xref:System.Collections.Generic.IEnumerable%601> generico.  Il corpo della lambda è identico all'espressione nella sintassi della query o in un'altra espressione o istruzione C\# e può includere chiamate al metodo e altra logica complessa.  Il "valore restituito" è il risultato dell'espressione.  
  
 Per iniziare a utilizzare [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], non è necessario utilizzare le espressioni lambda.  Tuttavia, alcune query possono essere espresse solo nella sintassi del metodo e possono richiedere le espressioni lambda.  Dopo aver acquisito dimestichezza con le espressioni lambda, si scoprirà che sono uno strumento potente e flessibile nella casella degli strumenti [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Per ulteriori informazioni, vedere [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
## Componibilità delle query  
 Nell'esempio di codice precedente si noti che il metodo `OrderBy` viene richiamato utilizzando l'operatore punto nella chiamata a `Where`.  `Where` produce una sequenza filtrata, quindi `Orderby` agisce su tale sequenza ordinandola.  Poiché le query restituiscono un oggetto `IEnumerable`, è necessario comporle nella sintassi del metodo concatenando le chiamate al metodo.  Questa operazione viene eseguita automaticamente dal compilatore quando si scrivono le query utilizzando la sintassi della query.  E poiché una variabile di query non archivia i risultati della query, è possibile modificarla o utilizzarla come base per una nuova query in qualsiasi momento, anche dopo l'esecuzione.  
  
## Vedere anche  
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)