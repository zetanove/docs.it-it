---
title: Filtro di dati (C#) | Microsoft Docs
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
ms.assetid: fbaece0d-0f23-47f7-89c5-f3ea8db692b6
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1d0efd313a670348a65870c348dd2ef5e079e5d0
ms.lasthandoff: 03/13/2017

---
# <a name="filtering-data-c"></a>Filtro di dati (C#)
Il filtro si riferisce all'operazione in base alla quale il set di risultati viene limitato in modo da contenere solo gli elementi che corrispondono a una condizione specificata. È anche noto come selezione.  
  
 Nella figura seguente vengono illustrati i risultati del filtro di una sequenza di caratteri. Il predicato per l'operazione di filtro specifica che il carattere deve essere 'A'.  
  
 ![Operazione di filtro LINQ](../../../../csharp/programming-guide/concepts/linq/media/linq_filter.png "LINQ_Filter")  
  
 La sezione seguente elenca i metodi dell'operatore query standard che esegue la selezione.  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi di espressione della query C#|Altre informazioni|  
|-----------------|-----------------|---------------------------------|----------------------|  
|OfType|Seleziona i valori, a seconda della loro capacità di eseguire il cast a un tipo specificato.|Non applicabile.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName>|  
|Dove|Seleziona i valori che si basano su una funzione di predicato.|`where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-example"></a>Esempi di sintassi delle espressioni di query  
 Nell'esempio seguente viene usata la clausola `where` per filtrare da una matrice le stringhe con una lunghezza specifica.  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            where word.Length == 3  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
*/  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq>   
 [Panoramica degli operatori query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Clausola Where](../../../../csharp/language-reference/keywords/where-clause.md)   
 [Procedura: Specificare dinamicamente i filtri dei predicati in fase di esecuzione](../../../../csharp/programming-guide/linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)   
 [Procedura: Eseguire una query sui metadati di un assembly tramite reflection (LINQ)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-assembly-s-metadata-with-reflection-linq.md)   
 [Procedura: Eseguire una query per trovare i file con un attributo o un nome specifico (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-for-files-with-a-specified-attribute-or-name.md)   
 [Procedura: Ordinare o filtrare i dati di testo in base a qualsiasi parola o campo (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
