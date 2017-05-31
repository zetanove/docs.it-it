---
title: Espressioni (Guida per programmatori C#) | Microsoft Docs
ms.date: 2017-05-11
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- expressions [C#]
- C# language, expressions
ms.assetid: c7d8feb0-0e58-4f94-8bf6-4d070550a832
caps.latest.revision: 22
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: 79efbca3d8d0b32c83dc3909e0a33839ecc0ef3e
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="expressions-c-programming-guide"></a>Espressioni (Guida per programmatori C#)
Un'*espressione* è una sequenza di uno o più operandi e zero o più operatori che può restituire un singolo valore, oggetto, metodo o spazio dei nomi. Le espressioni possono contenere un valore letterale, una chiamata al metodo, un operatore e i relativi operandi oppure un *nome semplice*, ad esempio il nome di una variabile, un membro di un tipo, un parametro di un metodo, uno spazio dei nomi o un tipo.  
  
 Le espressioni possono usare operatori che a loro volta usano altre espressioni come parametri oppure chiamate a metodi i cui parametri sono a loro volta altre chiamate a metodi, quindi le espressioni possono variare da semplici a molto complesse. Di seguito sono riportati due esempi di espressioni:  
  
```csharp  
((x < 10) && ( x > 5)) || ((x > 20) && (x < 25));
   
System.Convert.ToInt32("35");  
```  
  
## <a name="expression-values"></a>Valori dell'espressione  
 Nella maggior parte dei contesti in cui si usano le espressioni, ad esempio in istruzioni o parametri di metodo, l'espressione deve restituire un valore. Se x e y sono numeri interi, l'espressione `x + y` restituisce un valore numerico. L'espressione `new MyClass()` restituisce un riferimento a una nuova istanza di un oggetto `MyClass`. L'espressione `myClass.ToString()` restituisce una stringa poiché questo è il tipo restituito del metodo. Tuttavia, sebbene il nome di uno spazio dei nomi sia classificato come espressione, non restituisce un valore e quindi non può mai essere il risultato finale di un'espressione. Non è possibile passare il nome di uno spazio dei nomi a un parametro di metodo né usarlo in una nuova espressione o assegnarlo a una variabile. È possibile usarlo solo in un'espressione più ampia come sottoespressione. Lo stesso vale per i tipi (distinti dagli oggetti <xref:System.Type?displayProperty=fullName>), i nomi dei gruppi di metodi (distinti dai metodi specifici) e le funzioni di accesso agli eventi [add](../../../csharp/language-reference/keywords/add.md) e [remove](../../../csharp/language-reference/keywords/remove.md).  
  
 Ad ogni valore è associato un tipo. Ad esempio, se x e y sono entrambi variabili di tipo `int`, anche il valore dell'espressione `x + y` è di tipo `int`. Se il valore viene assegnato a una variabile di tipo diverso o se x e y sono tipi diversi, vengono applicate le regole di conversione del tipo. Per altre informazioni sul funzionamento di tali conversioni, vedere [Cast e conversioni di tipi](../../../csharp/programming-guide/types/casting-and-type-conversions.md).  
  
## <a name="overflows"></a>Overflow  
 Le espressioni numeriche possono causare overflow se il valore è maggiore del valore massimo del tipo del valore. Per altre informazioni, vedere [Checked e Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md) e la [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
## <a name="operator-precedence-and-associativity"></a>Precedenza e associatività degli operatori  
 Il modo in cui viene valutata un'espressione è disciplinato dalle regole di associatività e dalla precedenza degli operatori. Per altre informazioni, vedere [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md).  
  
 La maggior parte delle espressioni, ad eccezione delle espressioni di assegnazione e delle espressioni di chiamata di metodo, devono essere incorporate in un'istruzione. Per altre informazioni, vedere [Istruzioni](../../../csharp/programming-guide/statements-expressions-operators/statements.md).  
  
## <a name="literals-and-simple-names"></a>Valori letterali e nomi semplici  
 I due tipi più semplici di espressione sono i valori letterali e i nomi semplici. Un valore letterale è un valore costante che non ha un nome. Ad esempio, nel codice seguente sia `5` che `"Hello World"` sono valori letterali:  
  
 [!code-cs[csProgGuideStatements#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/expressions_1.cs)]  
  
 Per altre informazioni sui valori letterali, vedere [Tipi](../../../csharp/language-reference/keywords/types.md).  
  
 Nell'esempio precedente, sia `i` che `s` sono nomi semplici che identificano le variabili locali. Quando tali variabili vengono usate in un'espressione, il nome della variabile restituisce il valore attualmente archiviato nel percorso della variabile in memoria. Questa operazione è illustrata nell'esempio seguente:  
  
 [!code-cs[csProgGuideStatements#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/expressions_2.cs)]  
## <a name="invocation-expressions"></a>Espressioni di chiamata  
 Nell'esempio di codice seguente, la chiamata a `DoWork` è un'espressione di chiamata.  
  
```csharp
DoWork();  
```  
  
 Una chiamata al metodo richiede il nome del metodo, che può essere un nome come nell'esempio precedente o il risultato di un'altra espressione, seguito da parentesi ed eventuali parametri di metodo. Per altre informazioni, vedere [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md). Una chiamata al delegato usa il nome di un delegato e i parametri di metodo tra parentesi. Per altre informazioni, vedere [Delegati](../../../csharp/programming-guide/delegates/index.md). Le chiamate ai metodi e le chiamate ai delegati restituiscono il valore restituito del metodo, se il metodo restituisce un valore. I metodi che restituiscono void non possono essere usati al posto di un valore in un'espressione.  

## <a name="query-expressions"></a>Espressioni di query  
 Per le espressioni di query sono valide le stesse regole applicate in generale per le espressioni. Per altre informazioni, vedere [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md).  
  
## <a name="lambda-expressions"></a>Espressioni lambda  
 Le espressioni lambda rappresentano "metodi inline" che non hanno nome ma possono avere parametri di input e più istruzioni. Vengono ampiamente usate in LINQ per passare gli argomenti ai metodi. Le espressioni lambda vengono compilate in delegati o alberi delle espressioni a seconda del contesto in cui vengono usate. Per altre informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
## <a name="expression-trees"></a>Alberi delle espressioni  
 Gli alberi delle espressioni consentono di rappresentare le espressioni come strutture dei dati. Vengono ampiamente usati dai provider LINQ per convertire le espressioni di query in un codice che sia significativo in un altro contesto, ad esempio un database SQL. Per altre informazioni, vedere [Alberi delle espressioni](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b).  
  
## <a name="expression-body-definitions"></a>Definizioni del corpo dell'espressione

C# supporta i *membri con corpo di espressione*, che consentono di specificare una definizione concisa del corpo dell'espressione per metodi, costruttori, finalizzatori, proprietà e indicizzatori. Per altre informazioni, vedere [Membri con corpo di espressione](expression-bodied-members.md).

## <a name="remarks"></a>Note  
 Ogni volta che un'espressione identifica una variabile, una proprietà dell'oggetto o l'accesso a un indicizzatore di oggetti, il valore di tale elemento viene usato come valore dell'espressione. Un'espressione può essere inserita ovunque sia richiesto un valore o un oggetto in C#, purché l'espressione alla fine restituisca il tipo richiesto.  

## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Operatori](../../../csharp/programming-guide/statements-expressions-operators/operators.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)
