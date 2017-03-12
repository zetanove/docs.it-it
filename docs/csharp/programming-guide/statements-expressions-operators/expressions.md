---
title: "Espressioni (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, espressioni"
  - "espressioni [C#]"
ms.assetid: c7d8feb0-0e58-4f94-8bf6-4d070550a832
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# Espressioni (Guida per programmatori C#)
Una *espressione* è una sequenza di uno o più operandi e di zero o più operatori che possono restituire un singolo valore, oggetto, metodo o spazio dei nomi.  Le espressioni possono contenere un valore letterale, una chiamata di metodo, un operatore e i relativi operandi oppure un *nome semplice*,  ad esempio il nome di una variabile, un membro di tipo, un parametro di metodo, uno spazio dei nomi o un tipo.  
  
 Le espressioni possono presentare diversi gradi di complessità, da semplici a molto complesse, in quanto possono utilizzare operatori che a loro volta utilizzano altre espressioni come parametri oppure chiamate a metodi i cui parametri sono a loro volta altre chiamate a metodi.  Di seguito sono elencati esempi di espressioni.  
  
```  
((x < 10) && ( x > 5)) || ((x > 20) && (x < 25))   
System.Convert.ToInt32("35")  
```  
  
## Valori dell'espressione  
 Nella maggior parte dei contesti nella quale le espressioni vengono utilizzate, ad esempio in istruzioni o parametri di un metodo, è previsto che l'espressione restituisca un valore.  Se x e y sono di tipo integer, l'espressione `x + y` restituisce un valore numerico.  L'espressione `new MyClass()` restituisce un riferimento a una nuova istanza di un oggetto `MyClass`.  L’espressione `myClass.ToString()` restituisce una stringa perché questo è il tipo restituito dal method.  Tuttavia, sebbene il nome di uno spazio dei nomi sia classificato come un'espressione, non restituisce un valore e pertanto non può mai essere il risultato finale di un’espressione.  Non è possibile passare il nome di uno spazio dei nomi come parametro di un metodo, utilizzarlo in una nuova espressione o assegnarlo a una variabile.  È possibile utilizzarlo solo come una sottoespressione in un’espressione più grande.  Lo stesso vale per i tipi \(distinti dagli oggetti <xref:System.Type?displayProperty=fullName> \), i nomi di gruppi di metodi \(distinti dai metodi specifici\) e le funzioni di accesso degli eventi [aggiungi](../../../csharp/language-reference/keywords/add.md) e [rimuovi](../../../csharp/language-reference/keywords/remove.md).  
  
 Ad ogni valore è associato un tipo.  Ad esempio, se x e y sono entrambi variabili di tipo `int`, il valore dell'espressione `x + y` è anch’esso di tipo `int`.  Se il valore è assegnato ad una variabile di un tipo diverso, o se x e y sono tipi diversi fra loro, vengono applicate le regole di conversione del tipo.  Per ulteriori informazioni sul funzionamento di tali conversioni, vedere [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md).  
  
## Overflow  
 Le espressioni numeriche possono causare overflow se il valore è più grande del massimo valore accettabile per il tipo.  Per ulteriori informazioni, vedere [Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md) e [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
## Precedenza e associazione tra gli operatori  
 Il modo in cui viene valutata un'espressione è governato dalle regole di associazione e precedenza degli operatori.  Per ulteriori informazioni, vedere [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md).  
  
 La maggior parte delle espressioni, tranne le espressioni di assegnazione e le espressioni di chiamata di un metodo, deve essere incorporata in un'istruzione.  Per ulteriori informazioni, vedere [Istruzioni](../../../csharp/programming-guide/statements-expressions-operators/statements.md).  
  
## Valori letterali e nomi semplici  
 I due tipi più semplici di espressioni sono i valori letterali e i nomi semplici.  Il valore letterale è un valore costante privo di nome.  Nell'esempio di codice riportato di seguito `5` e `"Hello World"` sono valori letterali:  
  
 [!code-cs[csProgGuideStatements#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/expressions_1.cs)]  
  
 Per ulteriori informazioni sui valori letterali, vedere [Tipi](../../../csharp/language-reference/keywords/types.md).  
  
 Nell'esempio precedente `i` e `s` sono nomi semplici che identificano variabili locali.  Quando tali variabili vengono utilizzate in un'espressione, il nome della variabile restituisce il valore attualmente archiviato nella posizione di memoria corrispondente alla variabile,  come illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideStatements#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/expressions_2.cs)]  
  
## Espressioni di chiamata  
 Nell'esempio di codice seguente la chiamata a `DoWork` è un'espressione di chiamata.  
  
```  
DoWork();  
```  
  
 Tramite la chiamata viene richiesto il nome del metodo, che può essere un nome semplice, come nell'esempio precedente, oppure il risultato di un'altra espressione, seguito dalla parentesi e da eventuali parametri di metodo.  Per ulteriori informazioni, vedere [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md).  Una chiamata a un delegato comprende il nome di un delegato e i parametri di metodo tra parentesi.  Per ulteriori informazioni, vedere [Delegati](../../../csharp/programming-guide/delegates/index.md).  Le chiamate a metodi e delegati restituiscono il valore restituito del metodo, se quest'ultimo restituisce un valore.  Non è possibile utilizzare i metodi che restituiscono void in sostituzione di un valore in un'espressione.  
  
## Espressioni di query  
 Le stesse regole relative alle espressioni si applicano in genere alle espressioni di query.  Per ulteriori informazioni, vedere [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md).  
  
## Espressioni lambda  
 Le espressioni lambda rappresentano "metodi inline" che non hanno nome, ma che possono avere parametri di input e più istruzioni.  Sono ampiamente utilizzate in LINQ per passare argomenti ai metodi.  Le espressioni lambda vengono compilate per delegati o strutture ad albero dell'espressione a seconda del contesto nel quale vengono utilizzate.  Per ulteriori informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
## Strutture ad albero dell'espressione  
 Le strutture ad albero dell'espressione consentono alle espressioni di essere rappresentate come strutture di dati.  Sono ampiamente utilizzate dai provider LINQ per convertire espressioni di query in codice significativo in altri contesti, ad esempio un database SQL.  Per ulteriori informazioni, vedere [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Note  
 Ogni volta che da un'espressione viene identificato l'accesso a una variabile, a una proprietà di oggetto o a un indicizzatore di oggetto, il valore di tale elemento viene utilizzato come valore dell'espressione.  In C\# è possibile inserire un'espressione ovunque sia richiesto un valore o un oggetto, purché alla fine restituisca il tipo richiesto.  
  
## Capitoli del libro rappresentati  
 [Variabili ed espressioni](http://go.microsoft.com/fwlink/?LinkId=221228) in [Visual c\# 2010 iniziale](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)