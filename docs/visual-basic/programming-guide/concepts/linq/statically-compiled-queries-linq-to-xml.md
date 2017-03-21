---
title: Query (LINQ to XML) compilate in modo statico (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 3f4825c7-c3b0-48da-ba4e-8e97fb2a2f34
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2ea8e71acf861b93a21296c74254b3ca4d977d0a
ms.lasthandoff: 03/13/2017


---
# <a name="statically-compiled-queries-linq-to-xml-visual-basic"></a>Query (LINQ to XML) compilate in modo statico (Visual Basic)
Uno delle prestazioni più importanti vantaggi a livello LINQ to XML, in contrapposizione a <xref:System.Xml.XmlDocument>, sono che le query in LINQ to XML sono staticamente compilate, mentre le query XPath devono essere interpretate in fase di esecuzione.</xref:System.Xml.XmlDocument> Questa funzionalità è incorporata in LINQ to XML, pertanto non è necessario eseguire passaggi aggiuntivi per sfruttarla, ma è utile capire la distinzione per saper scegliere tra le due tecnologie. In questo argomento viene illustrata la differenza  
  
## <a name="statically-compiled-queries-vs-xpath"></a>Confronto tra query compilate in modo statico e XPath  
 Nell'esempio seguente viene illustrato come ottenere gli elementi discendenti con un nome specificato e con un attributo con un valore specificato.  
  
 Di seguito è riportata l'espressione XPath equivalente:  
  
```  
//Address[@Type='Shipping']  
```  
  
```vb  
Dim po = XDocument.Load("PurchaseOrders.xml")  
  
Dim list1 = From el In po.Descendants("Address")  
            Where el.@Type = "Shipping"  
  
For Each el In list1  
    Console.WriteLine(el)  
Next  
  
```  
  
 L'espressione di query di questo esempio viene scritta di nuovo dal compilatore nella sintassi delle query basate su metodo. L'esempio seguente, scritto nella sintassi delle query basate su metodo, produce gli stessi risultati del precedente:  
  
```vb  
Dim po = XDocument.Load("PurchaseOrders.xml")  
  
Dim list1 As IEnumerable(Of XElement) = po.Descendants("Address").Where(Function(el) el.@Type = "Shipping")  
  
For Each el In list1  
    Console.WriteLine(el)  
Next   
```  
  
 Il <xref:System.Linq.Enumerable.Where%2A>è un metodo di estensione.</xref:System.Linq.Enumerable.Where%2A> Per ulteriori informazioni, vedere [metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md). Poiché <xref:System.Linq.Enumerable.Where%2A>è un metodo di estensione, la query precedente è compilata come se fosse scritta come indicato di seguito:</xref:System.Linq.Enumerable.Where%2A>  
  
```vb  
Dim po = XDocument.Load("PurchaseOrders.xml")  
  
Dim list1 = Enumerable.Where(po.Descendants("Address"), Function(el) el.@Type = "Shipping")  
  
For Each el In list1  
    Console.WriteLine(el)  
Next  
```  
  
 Questo esempio produce esattamente gli stessi risultati dei due esempi precedenti. Questo illustra il fatto che le query sono compilate efficacemente in chiamate ai metodi collegate in modo statico. Questo fatto, insieme alla semantica di esecuzione posticipata degli iteratori, consente un miglioramento delle prestazioni. Per ulteriori informazioni sulla semantica di esecuzione posticipata degli iteratori, vedere [l'esecuzione posticipata e valutazione differita in LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
> [!NOTE]
>  Questi esempi rappresentano il codice che potrebbe venire scritto dal compilatore. L'implementazione effettiva potrebbe differire leggermente da questi esempi, ma le prestazioni saranno la stesse o simili.  
  
## <a name="executing-xpath-expressions-with-xmldocument"></a>Esecuzione di espressioni XPath con XmlDocument  
 Nell'esempio seguente viene utilizzato <xref:System.Xml.XmlDocument>per ottenere gli stessi risultati degli esempi precedenti:</xref:System.Xml.XmlDocument>  
  
```vb  
Dim reader = Xml.XmlReader.Create("PurchaseOrders.xml")  
Dim doc As New Xml.XmlDocument()  
doc.Load(reader)  
Dim nl As Xml.XmlNodeList = doc.SelectNodes(".//Address[@Type='Shipping']")  
For Each n As Xml.XmlNode In nl  
    Console.WriteLine(n.OuterXml)  
Next  
reader.Close()  
  
```  
  
 Questa query restituisce lo stesso output degli esempi che utilizzano LINQ to XML. l'unica differenza è che LINQ to XML viene applicato un rientro al codice XML stampato, mentre <xref:System.Xml.XmlDocument>non esiste.</xref:System.Xml.XmlDocument>  
  
 Tuttavia, il <xref:System.Xml.XmlDocument>approccio in genere non esegue e LINQ to XML, perché il <xref:System.Xml.XmlNode.SelectNodes%2A>metodo deve eseguire le operazioni seguenti internamente, ogni volta che viene chiamato:</xref:System.Xml.XmlNode.SelectNodes%2A> </xref:System.Xml.XmlDocument>  
  
-   Analisi della stringa che contiene l'espressione XPath, suddividendo la stringa in token.  
  
-   Convalida dei token per assicurarsi che l'espressione XPath sia valida.  
  
-   Conversione dell'espressione in un albero delle espressioni interno.  
  
-   Iterazione nei nodi, selezionando in modo appropriato i nodi per il set di risultati in base alla valutazione dell'espressione.  
  
 Queste operazioni sono in numero significativamente maggiore rispetto a quelle eseguite dalla query LINQ to XML corrispondente. La differenza di prestazioni specifica varia per diversi tipi di query, ma in genere meno operazioni di query LINQ to XML e pertanto prestazioni migliori rispetto alla valutazione di espressioni XPath tramite <xref:System.Xml.XmlDocument>.</xref:System.Xml.XmlDocument>  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)
