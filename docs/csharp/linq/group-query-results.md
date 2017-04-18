---
title: Raggruppare i risultati di una query
description: Come raggruppare i risultati.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2e4ec27f-06fb-4de7-8973-0189906d4520
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ee1ad2d65fda8a524b42f44f893e0b6f5f81eea5
ms.lasthandoff: 03/13/2017

---
# <a name="group-query-results"></a>Raggruppare i risultati di una query

Il raggruppamento è una delle funzionalità più efficace di LINQ. Negli esempi seguenti viene illustrato come raggruppare i dati in vari modi:  
  
-   In base a una singola proprietà.  
  
-   In base alla prima lettera di una proprietà stringa.  
  
-   In base a un intervallo numerico calcolato.  
  
-   In base a un predicato booleano o un'altra espressione.  
  
-   In base a una chiave composta.  
  
 Le ultime due query proiettano i risultati in un tipo anonimo nuovo che contiene solo il nome e il cognome dello studente. Per altre informazioni, vedere [Clausola group](../language-reference/keywords/group-clause.md).  
  
## <a name="example"></a>Esempio  
 In tutti gli esempi di questo argomento vengono usate le classi di supporto e le origini dati seguenti.  
  
 [!code-cs[csProgGuideLINQ#15](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come raggruppare gli elementi di origine usando una sola proprietà dell'elemento come chiave di gruppo. In questo caso la chiave è un oggetto `string`, il cognome dello studente. È anche possibile usare una sottostringa per la chiave. L'operazione di raggruppamento usa l'operatore di confronto di uguaglianza predefinito per il tipo.  
  
 Incollare il metodo seguente nella classe `StudentClass`. Modificare l'istruzione di chiamata nel metodo `Main` in `sc.GroupBySingleProperty()`.  
  
 [!code-cs[csProgGuideLINQ#17](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_2.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come raggruppare gli elementi di origine usando un elemento diverso da una proprietà dell'oggetto per la chiave di gruppo. In questo esempio la chiave è la prima lettera del cognome dello studente.  
  
 Incollare il metodo seguente nella classe `StudentClass`. Modificare l'istruzione di chiamata nel metodo `Main` in `sc.GroupBySubstring()`.  
  
 [!code-cs[csProgGuideLINQ#18](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_3.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come raggruppare gli elementi di origine usando un intervallo numerico come chiave di gruppo. La query proietta i risultati in un tipo anonimo che contiene solo il nome e il cognome e l'intervallo percentile al quale appartiene lo studente. Viene usato un tipo anonimo perché non è necessario usare l'oggetto `Student` completo per visualizzare i risultati. `GetPercentile` è una funzione di supporto che consente di calcolare un percentile in base al voto medio dello studente. Il metodo restituisce un numero intero compreso tra 0 e 10.  
  
 [!code-cs[csProgGuideLINQ#50](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_4.cs)]  
  
 Incollare il metodo seguente nella classe `StudentClass`. Modificare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByRange()`.  
  
 [!code-cs[csProgGuideLINQ#19](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_5.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come raggruppare elementi di origine usando un'espressione di confronto booleana. In questo esempio l'espressione booleana consente di verificare se il voto medio degli esami di uno studente è maggiore di 75. Come negli esempi precedenti, i risultati vengono proiettati in un tipo anonimo perché l'elemento di origine completo non è necessario. Si noti che le proprietà nel tipo anonimo diventano proprietà sul membro `Key` e sono accessibili tramite il nome quando la query viene eseguita.  
  
 Incollare il metodo seguente nella classe `StudentClass`. Modificare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByBoolean()`.  
  
 [!code-cs[csProgGuideLINQ#20](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_6.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare un tipo anonimo per incapsulare una chiave che contiene più valori. In questo esempio il primo valore della chiave è la prima lettera del cognome dello studente. Il secondo valore della chiave è un valore booleano che specifica se lo studente ha ottenuto un voto superiore a 85 nel primo esame. È possibile ordinare i gruppi in base a qualsiasi proprietà nella chiave.  
  
 Incollare il metodo seguente nella classe `StudentClass`. Modificare l'istruzione di chiamata nel metodo `Main` in `sc.GroupByCompositeKey()`.  
  
 [!code-cs[csProgGuideLINQ#21](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_7.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.IGrouping%602>   
 [Espressioni di query LINQ](index.md)   
 [Clausola group](../language-reference/keywords/group-clause.md)   
 [Tipi anonimi](../programming-guide/classes-and-structs/anonymous-types.md)   
 [Eseguire una sottoquery su un'operazione di raggruppamento](perform-a-subquery-on-a-grouping-operation.md)   
 [Creare un gruppo annidato](create-a-nested-group.md)   
 [Raggruppamento dei dati](../programming-guide/concepts/linq/grouping-data.md)
