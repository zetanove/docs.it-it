---
title: Prestazioni delle query concatenate (LINQ to XML) (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 589f2adc-69f9-404d-b9d6-4c28dabea7f7
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dd5b63f255107c5864108cfbb87bef6e53a971a0
ms.lasthandoff: 03/13/2017


---
# <a name="performance-of-chained-queries-linq-to-xml-visual-basic"></a>Prestazioni delle query concatenate (LINQ to XML) (Visual Basic)
Uno dei più importanti vantaggi di LINQ (e di LINQ to XML) consiste nel fatto che le query concatenate possono offrire le stesse prestazioni di una singola query di dimensioni maggiori e più complessa.  
  
 Una query concatenata è una query che usa un'altra query come origine. Nel semplice codice seguente, ad esempio, `query2` è l'origine di `query1`:  
  
```vb  
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))  
  
Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x  
  
Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e  
  
For Each i As var In query2  
    Console.WriteLine("{0}", CInt(i))  
Next  
  
```  
  
 Questo esempio produce il seguente output:  
  
```  
4  
```  
  
 Questa query concatenata offre lo stesso profilo di prestazioni dell'iterazione in un elenco collegato.  
  
-   Il <xref:System.Xml.Linq.XContainer.Elements%2A>asse ha essenzialmente le stesse prestazioni come scorrere un elenco collegato.</xref:System.Xml.Linq.XContainer.Elements%2A> <xref:System.Xml.Linq.XContainer.Elements%2A>viene implementato come iteratore con esecuzione posticipata.</xref:System.Xml.Linq.XContainer.Elements%2A> Questo significa che esegue alcune operazioni in aggiunta all'iterazione nell'elenco collegato, ad esempio l'allocazione dell'oggetto iteratore e la registrazione dello stato di esecuzione. Queste operazioni possono essere divise in due categorie: le operazioni eseguite al momento della configurazione dell'iteratore e quelle eseguite durante ogni iterazione. Le operazioni di configurazione implicano una quantità di lavoro piccola e fissa, mentre quelle eseguite durante ogni iterazione sono proporzionali al numero di elementi nella raccolta di origine.  
  
-   In `query1`, `Where` clausola, la query di chiamare il <xref:System.Linq.Enumerable.Where%2A>(metodo).</xref:System.Linq.Enumerable.Where%2A> Questo metodo è implementato anche come iteratore. Le operazioni di configurazione consistono nella creazione di un'istanza del delegato che fa riferimento all'espressione lambda, nonché nelle normali operazioni di configurazione per un iteratore. A ogni iterazione, il delegato viene chiamato per eseguire il predicato. Le operazioni di configurazione e quelle eseguite durante ogni iterazione sono simili a quelle eseguite durante l'iterazione nell'asse.  
  
-   In `query1`, la clausola select fa sì che la query di chiamare il <xref:System.Linq.Enumerable.Select%2A>(metodo).</xref:System.Linq.Enumerable.Select%2A> Questo metodo ha lo stesso profilo delle prestazioni di <xref:System.Linq.Enumerable.Where%2A>(metodo).</xref:System.Linq.Enumerable.Where%2A>  
  
-   In `query2` sia la clausola `Where` che la clausola `Select` hanno lo stesso profilo di prestazioni, come in `query1`.  
  
 L'iterazione in `query2` è pertanto direttamente proporzionale al numero di elementi nell'origine della prima query, in altre parole un tempo lineare.  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)
