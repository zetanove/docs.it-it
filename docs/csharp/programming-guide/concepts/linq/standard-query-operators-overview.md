---
title: Cenni preliminari sugli operatori di query standard (C#) | Documentazione Microsoft
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
ms.assetid: 812fa119-5f65-4139-b4fa-55dccd8dc3ac
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5b03c85a298b3864a91a7052ca80cf3714ba98fe
ms.lasthandoff: 03/13/2017

---
# <a name="standard-query-operators-overview-c"></a>Cenni preliminari sugli operatori di query standard (C#)
Gli *operatori di query standard* sono metodi che costituiscono il modello LINQ. La maggior parte di questi metodi agisce sulle sequenze, dove una sequenza è un oggetto il cui tipo implementa l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>. Gli operatori di query standard forniscono le funzionalità di query che includono filtro, proiezione, aggregazione, ordinamento e altro ancora.  
  
 Sono disponibili due set di operatori di query standard LINQ, uno che agisce sugli oggetti di tipo <xref:System.Collections.Generic.IEnumerable%601> e l'altro che agisce sugli oggetti di tipo <xref:System.Linq.IQueryable%601>. I metodi che costituiscono ogni set sono membri statici rispettivamente delle classi <xref:System.Linq.Enumerable> e <xref:System.Linq.Queryable>. Vengono definiti come *metodi di estensione* del tipo su cui agiscono. Ciò significa che possono essere chiamati usando la sintassi del metodo statico o la sintassi del metodo di istanza.  
  
 Inoltre, molti metodi degli operatori di query standard agiscono su tipi diversi da quelli basati su <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>. Il tipo <xref:System.Linq.Enumerable> definisce questi due diversi metodi che agiscono entrambi su oggetti di tipo <xref:System.Collections.IEnumerable>. Questi metodi, <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> e <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29>, consentono l'esecuzione di query su una Collection senza parametri o non generico nel modello LINQ grazie alla creazione di una Collection di oggetti fortemente tipizzato. La classe <xref:System.Linq.Queryable> definisce due metodi simili, <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> e <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>, che agiscono su oggetti di tipo <xref:System.Linq.Queryable>.  
  
 Gli operatori di query standard presentano una durata di esecuzione diversa, a seconda che restituiscano un valore singleton o una sequenza di valori. Questi metodi che restituiscono un valore singleton, ad esempio <xref:System.Linq.Enumerable.Average%2A> e <xref:System.Linq.Enumerable.Sum%2A>, vengono eseguiti immediatamente. I metodi che restituiscono una sequenza rinviano l'esecuzione della query e restituiscono un oggetto enumerabile.  
  
 Nel caso dei metodi che agiscono sulle Collection in memoria, ovvero i metodi che estendono <xref:System.Collections.Generic.IEnumerable%601>, l'oggetto enumerabile restituito acquisisce gli argomenti passati al metodo. Quando l'oggetto viene enumerato, viene utilizzata la logica dell'operatore query e vengono restituiti i risultati della query.  
  
 I metodi che estendono <xref:System.Linq.IQueryable%601> non implementano invece il comportamento delle query, ma compilano un albero delle espressioni che rappresenta la query da eseguire. L'elaborazione delle query viene gestita dall'oggetto <xref:System.Linq.IQueryable%601> di origine.  
  
 Le chiamate ai metodi della query possono essere concatenate in una query, consentendo alle query di diventare arbitrariamente complesse.  
  
 Nell'esempio di codice seguente viene illustrato come usare gli operatori di query standard per ottenere informazioni su una sequenza.  
  
```csharp  
string sentence = "the quick brown fox jumps over the lazy dog";  
// Split the string into individual words to create a collection.  
string[] words = sentence.Split(' ');  
  
// Using query expression syntax.  
var query = from word in words  
            group word.ToUpper() by word.Length into gr  
            orderby gr.Key  
            select new { Length = gr.Key, Words = gr };  
  
// Using method-based query syntax.  
var query2 = words.  
    GroupBy(w => w.Length, w => w.ToUpper()).  
    Select(g => new { Length = g.Key, Words = g }).  
    OrderBy(o => o.Length);  
  
foreach (var obj in query)  
{  
    Console.WriteLine("Words of length {0}:", obj.Length);  
    foreach (string word in obj.Words)  
        Console.WriteLine(word);  
}  
  
// This code example produces the following output:  
//  
// Words of length 3:  
// THE  
// FOX  
// THE  
// DOG  
// Words of length 4:  
// OVER  
// LAZY  
// Words of length 5:  
// QUICK  
// BROWN  
// JUMPS   
```  
  
## <a name="query-expression-syntax"></a>Sintassi delle espressioni di query  
 Alcuni degli operatori di query standard usati più di frequente dispongono di sintassi dedicata delle parole chiave per i linguaggi C# e Visual Basic che consente di chiamare gli operatori come parte di un'*espressione* di *query*. Per altre informazioni sugli operatori di query standard con parole chiave dedicate e le relative sintassi, vedere [Sintassi di espressione della query per operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md).  
  
## <a name="extending-the-standard-query-operators"></a>Estensione degli operatori di query standard  
 È possibile estendere il set di operatori di query standard creando metodi specifici del dominio appropriati per la tecnologia o il dominio di destinazione. È possibile anche sostituire gli operatori di query standard con implementazioni personalizzate che forniscono servizi aggiuntivi, ad esempio la valutazione remota, la conversione delle query e l'ottimizzazione. Per un esempio vedere <xref:System.Linq.Enumerable.AsEnumerable%2A>.  
  
## <a name="related-sections"></a>Sezioni correlate  
 I collegamenti riportati di seguito consentono di passare ad argomenti che forniscono informazioni aggiuntive sui vari operatori di query standard in base alla funzionalità.  
  
 [Ordinamento dei dati (C#)](../../../../csharp/programming-guide/concepts/linq/sorting-data.md)  
  
 [Operazioni sui set (C#)](../../../../csharp/programming-guide/concepts/linq/set-operations.md)  
  
 [Filtro di dati (C#)](../../../../csharp/programming-guide/concepts/linq/filtering-data.md)  
  
 [Operazioni del quantificatore (C#)](../../../../csharp/programming-guide/concepts/linq/quantifier-operations.md)  
  
 [Operazioni di proiezione (C#)](../../../../csharp/programming-guide/concepts/linq/projection-operations.md)  
  
 [Partizionamento dei dati (C#)](../../../../csharp/programming-guide/concepts/linq/partitioning-data.md)  
  
 [Operazioni di join (C#)](../../../../csharp/programming-guide/concepts/linq/join-operations.md)  
  
 [Raggruppamento dei dati (C#)](../../../../csharp/programming-guide/concepts/linq/grouping-data.md)  
  
 [Operazioni di generazione (C#)](../../../../csharp/programming-guide/concepts/linq/generation-operations.md)  
  
 [Operazioni di uguaglianza (C#)](../../../../csharp/programming-guide/concepts/linq/equality-operations.md)  
  
 [Operazioni sugli elementi (C#)](../../../../csharp/programming-guide/concepts/linq/element-operations.md)  
  
 [Conversione del tipo di dati (C#)](../../../../csharp/programming-guide/concepts/linq/converting-data-types.md)  
  
 [Operazioni di concatenazione (C#)](../../../../csharp/programming-guide/concepts/linq/concatenation-operations.md)  
  
 [Operazioni di aggregazione (C#)](../../../../csharp/programming-guide/concepts/linq/aggregation-operations.md)  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable>   
 [Introduzione alle query LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)   
 [Sintassi di espressione di query per operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)   
 [Classificazione degli operatori di query standard in base alla modalità di esecuzione](../../../../csharp/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)   
 [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
