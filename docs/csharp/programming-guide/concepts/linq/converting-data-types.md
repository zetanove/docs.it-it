---
title: Conversione di tipi di dati (C#) | Microsoft Docs
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
ms.assetid: 46e5682f-77a1-4302-8f93-a2b53c408808
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
ms.openlocfilehash: 922e2f26c5f8ded260644e8effa043b03b721020
ms.lasthandoff: 03/13/2017

---
# <a name="converting-data-types-c"></a>Conversione di tipi di dati (C#)
I metodi di conversione modificano il tipo degli oggetti di input.  
  
 Le operazioni di conversione nelle query LINQ sono utili in un'ampia gamma di applicazioni. Ecco alcuni esempi:  
  
-   Il metodo <xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName> può essere usato per nascondere l'implementazione personalizzata di un tipo di un operatore di query standard.  
  
-   Il metodo <xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName> può essere usato per abilitare le raccolte senza parametri per l'esecuzione di query LINQ.  
  
-   I metodi <xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>, <xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>, <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName> e <xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName> possono essere usati per forzare l'esecuzione immediata della query anziché rinviarla fino a quando la query viene enumerata.  
  
## <a name="methods"></a>Metodi  
 Nella tabella seguente sono elencati i metodi di operatore query standard che eseguono conversioni di tipi di dati.  
  
 I metodi di conversione nella tabella i cui nomi iniziano con "As" modificano il tipo statico della raccolta di origine ma non lo enumerano. I metodi i cui nomi iniziano con "To" enumerano la raccolta di origine e inseriscono gli elementi nel tipo di raccolta corrispondente.  
  
|Nome metodo|Descrizione|Sintassi di espressione della query C#|Altre informazioni|  
|-----------------|-----------------|---------------------------------|----------------------|  
|AsEnumerable|Restituisce l'input digitato come <xref:System.Collections.Generic.IEnumerable%601>.|Non applicabile.|<xref:System.Linq.Enumerable.AsEnumerable%2A?displayProperty=fullName>|  
|AsQueryable|Converte un <xref:System.Collections.IEnumerable> (generico) in un <xref:System.Linq.IQueryable>.</xref:System.Linq.IQueryable> (generico).|Non applicabile.|<xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName>|  
|Cast|Esegue il cast degli elementi di una raccolta a un tipo specificato.|Usare una variabile di intervallo tipizzata in modo esplicito. Ad esempio:<br /><br /> `from string str in words`|<xref:System.Linq.Enumerable.Cast%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Cast%2A?displayProperty=fullName>|  
|OfType|Filtra i valori, a seconda della loro capacità di eseguire il cast a un tipo specificato.|Non applicabile.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=fullName>|  
|ToArray|Converte una raccolta in una matrice. Questo metodo forza l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToArray%2A?displayProperty=fullName>|  
|ToDictionary|Inserisce gli elementi in un <xref:System.Collections.Generic.Dictionary%602> in base a una funzione del selettore di chiavi. Questo metodo forza l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToDictionary%2A?displayProperty=fullName>|  
|ToList|Converte una raccolta in un oggetto <xref:System.Collections.Generic.List%601>. Questo metodo forza l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>|  
|ToLookup|Inserisce gli elementi in <xref:System.Linq.Lookup%602>, un dizionario uno-a-molti, in base a una funzione del selettore di chiavi. Questo metodo forza l'esecuzione di query.|Non applicabile.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=fullName>|  
  
## <a name="query-expression-syntax-example"></a>Esempio di sintassi delle espressioni di query  
 L'esempio di codice seguente usa una variabile di intervallo tipizzata in modo esplicito per eseguire il cast di un tipo a un sottotipo prima di accedere a un membro che è disponibile solo nel sottotipo.  
  
```csharp  
class Plant  
{  
    public string Name { get; set; }  
}  
  
class CarnivorousPlant : Plant  
{  
    public string TrapType { get; set; }  
}  
  
static void Cast()  
{  
    Plant[] plants = new Plant[] {  
        new CarnivorousPlant { Name = "Venus Fly Trap", TrapType = "Snap Trap" },  
        new CarnivorousPlant { Name = "Pitcher Plant", TrapType = "Pitfall Trap" },  
        new CarnivorousPlant { Name = "Sundew", TrapType = "Flypaper Trap" },  
        new CarnivorousPlant { Name = "Waterwheel Plant", TrapType = "Snap Trap" }  
    };  
  
    var query = from CarnivorousPlant cPlant in plants  
                where cPlant.TrapType == "Snap Trap"  
                select cPlant;  
  
    foreach (Plant plant in query)  
        Console.WriteLine(plant.Name);  
  
    /* This code produces the following output:  
  
        Venus Fly Trap  
        Waterwheel Plant  
    */  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq>   
 [Standard Query Operators Overview (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  (Panoramica degli operatori di query standard)  
 [Clausola From](../../../../csharp/language-reference/keywords/from-clause.md)   
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Procedura: Eseguire una query su un ArrayList con LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)
