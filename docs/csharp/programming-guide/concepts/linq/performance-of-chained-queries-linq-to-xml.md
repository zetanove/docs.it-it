---
title: Prestazioni delle query concatenate (LINQ to XML) (C#) | Microsoft Docs
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
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3429da268df07900ebe59ed206b927d209b1cf7f
ms.lasthandoff: 03/13/2017


---
# <a name="performance-of-chained-queries-linq-to-xml-c"></a>Prestazioni delle query concatenate (LINQ to XML) (C#)
Uno dei più importanti vantaggi di LINQ (e di LINQ to XML) consiste nel fatto che le query concatenate possono offrire le stesse prestazioni di una singola query di dimensioni maggiori e più complessa.  
  
 Una query concatenata è una query che usa un'altra query come origine. Nel semplice codice seguente, ad esempio, `query2` è l'origine di `query1`:  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    new XElement("Child", 3),  
    new XElement("Child", 4)  
);  
  
var query1 = from x in root.Elements("Child")  
             where (int)x >= 3  
             select x;  
  
var query2 = from e in query1  
             where (int)e % 2 == 0  
             select e;  
  
foreach (var i in query2)  
    Console.WriteLine("{0}", (int)i);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
4  
```  
  
 Questa query concatenata offre lo stesso profilo di prestazioni dell'iterazione in un elenco collegato.  
  
-   L'asse <xref:System.Xml.Linq.XContainer.Elements%2A> offre essenzialmente le stesse prestazioni dell'iterazione attraverso un elenco collegato. <xref:System.Xml.Linq.XContainer.Elements%2A> è implementato come iteratore con esecuzione posticipata. Questo significa che esegue alcune operazioni in aggiunta all'iterazione nell'elenco collegato, ad esempio l'allocazione dell'oggetto iteratore e la registrazione dello stato di esecuzione. Queste operazioni possono essere divise in due categorie: le operazioni eseguite al momento della configurazione dell'iteratore e quelle eseguite durante ogni iterazione. Le operazioni di configurazione implicano una quantità di lavoro piccola e fissa, mentre quelle eseguite durante ogni iterazione sono proporzionali al numero di elementi nella raccolta di origine.  
  
-   In `query1` la clausola `where` fa in modo che la query chiami il metodo <xref:System.Linq.Enumerable.Where%2A>. Questo metodo è implementato anche come iteratore. Le operazioni di configurazione consistono nella creazione di un'istanza del delegato che fa riferimento all'espressione lambda, nonché nelle normali operazioni di configurazione per un iteratore. A ogni iterazione, il delegato viene chiamato per eseguire il predicato. Le operazioni di configurazione e quelle eseguite durante ogni iterazione sono simili a quelle eseguite durante l'iterazione nell'asse.  
  
-   In `query1` la clausola select fa in modo che la query chiami il metodo <xref:System.Linq.Enumerable.Select%2A>. Questo metodo ha lo stesso profilo di prestazioni del metodo <xref:System.Linq.Enumerable.Where%2A>.  
  
-   In `query2` sia la clausola `where` che la clausola `select` hanno lo stesso profilo di prestazioni, come in `query1`.  
  
 L'iterazione in `query2` è pertanto direttamente proporzionale al numero di elementi nell'origine della prima query, in altre parole un tempo lineare. In un esempio di Visual Basic corrispondente il profilo di prestazioni sarebbe lo stesso.  
  
 Per altre informazioni sugli iteratori, vedere [yield](../../../../csharp/language-reference/keywords/yield.md).  
  
 Per un'esercitazione dettagliata sul concatenamento di query, vedere [Esercitazione: concatenamento di query](http://msdn.microsoft.com/library/c08d228a-f07a-4c98-810f-1bf0e8f2257c).  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)
