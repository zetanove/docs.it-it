---
title: Clausola group (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- group
- group_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- group keyword [C#]
- group clause [C#]
ms.assetid: c817242e-b12c-4baa-a57e-73ee138f34d1
caps.latest.revision: 24
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
ms.sourcegitcommit: 17edc1598b806f073ad93e470dc8764cfeb1e4eb
ms.openlocfilehash: d054a0824e9f072d38c01c2894606c5c492a2481
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="group-clause-c-reference"></a>Clausola group (Riferimento C#)
La clausola `group` restituisce una sequenza di oggetti <xref:System.Linq.IGrouping%602> che contengono zero o più elementi corrispondenti al valore chiave per il gruppo. Ad esempio, è possibile raggruppare una sequenza di stringhe in base alla prima lettera di ogni stringa. In questo caso, la prima lettera è la chiave con tipo [char](../../../csharp/language-reference/keywords/char.md) e viene archiviata nella proprietà `Key` di ogni oggetto <xref:System.Linq.IGrouping%602>. Il compilatore deduce automaticamente il tipo della chiave.  
  
 È possibile terminare un'espressione di query con una clausola `group`, come illustrato nell'esempio seguente:  
  
 [!code-cs[cscsrefQueryKeywords#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_1.cs)]  
  
 Per eseguire operazioni di query aggiuntive per ogni gruppo, è possibile specificare un identificatore temporaneo usando la parola chiave contestuale [into](../../../csharp/language-reference/keywords/into.md). Quando si usa `into`, è necessario continuare a eseguire la query ed eventualmente terminarla con un'istruzione `select` o un'altra clausola `group`, come illustrato nel seguente estratto di codice:  
  
 [!code-cs[cscsrefQueryKeywords#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_2.cs)]  
  
 Esempi di utilizzo di più completi di `group` con e senza `into` sono disponibili nella sezione Esempio di questo argomento.  
  
## <a name="enumerating-the-results-of-a-group-query"></a>Enumerazione dei risultati di una query con raggruppamento  
 Poiché gli oggetti <xref:System.Linq.IGrouping%602> prodotti da una query `group` sono essenzialmente un elenco di elenchi, è necessario usare un ciclo [foreach](../../../csharp/language-reference/keywords/foreach-in.md) nidificato per accedere agli elementi di ogni gruppo. Il ciclo esterno esegue l'iterazione delle chiavi del gruppo e il ciclo interno esegue l'iterazione di ogni voce nel gruppo. Un gruppo può avere una chiave ma non elementi. Di seguito è riportato il ciclo `foreach` che esegue la query negli esempi di codice precedenti:  
  
 [!code-cs[cscsrefQueryKeywords#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_3.cs)]  
  
## <a name="key-types"></a>Tipi di chiave  
 Le chiavi di raggruppamento possono essere di qualsiasi tipo, ad esempio una stringa, un tipo numerico incorporato, un tipo con nome definito dall'utente o un tipo anonimo.  
  
### <a name="grouping-by-string"></a>Raggruppamento per stringa  
 Negli esempi di codice precedenti è stato usato un oggetto `char`. Si potrebbe specificare in alternativa una chiave di stringa, ad esempio il cognome completo:  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_4.cs)]  
  
### <a name="grouping-by-bool"></a>Raggruppamento per valore booleano  
 L'esempio seguente illustra l'uso di un valore booleano per una chiave in modo da dividere i risultati in due gruppi. Si noti che il valore è generato da una sottoespressione nella clausola `group`.  
  
 [!code-cs[cscsrefQueryKeywords#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_5.cs)]  
  
### <a name="grouping-by-numeric-range"></a>Raggruppamento per intervallo numerico  
 Nell'esempio seguente viene usata un'espressione per creare le chiavi di raggruppamento numeriche che rappresentano un intervallo percentile. Si noti l'uso di [let](../../../csharp/language-reference/keywords/let-clause.md) come comoda posizione di archiviazione del risultato della chiamata a un metodo, in modo da non dover chiamare il metodo due volte nella clausola `group`. Si può notare inoltre che nella clausola `group`, per evitare un'eccezione "divisione per zero", il codice verifica se lo studente non ha una media pari a zero. Per altre informazioni su come usare in modo sicuro i metodi nelle espressioni di query, vedere [Procedura: Gestire le eccezioni nelle espressioni di query](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md).  
  
 [!code-cs[cscsrefQueryKeywords#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_6.cs)]  
  
### <a name="grouping-by-composite-keys"></a>Raggruppamento per chiavi composte  
 Usare una chiave composta se si vuole raggruppare gli elementi in base a più di una chiave. Per creare una chiave composta, usare un tipo anonimo o un tipo denominato per contenere l'elemento key. Nell'esempio seguente si suppone che una classe `Person` sia stata dichiarata con i membri denominati `surname` e `city`. La clausola `group` determina la creazione di un gruppo separato per ogni insieme di persone con lo stesso cognome e la stessa città.  
  
```csharp  
group person by new {name = person.surname, city = person.city};  
```  
  
 Usare un tipo denominato se è necessario passare la variabile di query a un altro metodo. Creare una classe speciale usando proprietà implementate automaticamente per le chiavi e quindi eseguire l'override dei metodi <xref:System.Object.Equals%2A> e <xref:System.Object.GetHashCode%2A>. È anche possibile usare uno struct e in questo caso non è strettamente necessario eseguire l'override dei metodi. Per altre informazioni, vedere [Procedura: Implementare una classe leggera con proprietà implementate automaticamente](../../../csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md) e [Procedura: Eseguire una query per trovare i file duplicati in un albero di directory](../../programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md). Il secondo argomento contiene un esempio di codice che illustra come usare una chiave composta con un tipo denominato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato il modello standard per l'ordinamento dei dati di origine nei gruppi quando non viene applicata una logica di query aggiuntiva ai gruppi. L'operazione è definita raggruppamento senza continuazione. Gli elementi in una matrice di stringhe vengono raggruppati in base alla prima lettera. Il risultato della query è un tipo <xref:System.Linq.IGrouping%602> che contiene una proprietà pubblica `Key` di tipo `char` e una raccolta <xref:System.Collections.Generic.IEnumerable%601> che contiene ogni elemento nel raggruppamento.  
  
 Il risultato di una clausola `group` è una sequenza di sequenze. Di conseguenza, per accedere ai singoli elementi all'interno di ogni gruppo restituito, usare un ciclo `foreach` nidificato all'interno del ciclo che esegue l'iterazione delle chiavi di raggruppamento, come illustrato nell'esempio seguente.  
  
 [!code-cs[cscsrefQueryKeywords#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_7.cs)]  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrato come eseguire la logica aggiuntiva per i gruppi dopo che sono stati creati, usando una *continuazione* con `into`. Per altre informazioni, vedere [into](../../../csharp/language-reference/keywords/into.md). Nell'esempio seguente viene eseguita una query di ogni gruppo per selezionare solo quelli il cui valore della chiave è una vocale.  
  
 [!code-cs[cscsrefQueryKeywords#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_8.cs)]  
  
## <a name="remarks"></a>Note  
 In fase di compilazione le clausole `group` vengono convertite in chiamate al metodo <xref:System.Linq.Enumerable.GroupBy%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.IGrouping%602>   
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.Enumerable.ThenBy%2A>   
 <xref:System.Linq.Enumerable.ThenByDescending%2A>   
 [Parole chiave di query (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Procedura: Creare un gruppo annidato](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)   
 [Procedura: Raggruppare i risultati di una query](../../../csharp/programming-guide/linq-query-expressions/how-to-group-query-results.md)   
 [Procedura: Eseguire una sottoquery su un'operazione di raggruppamento](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)

