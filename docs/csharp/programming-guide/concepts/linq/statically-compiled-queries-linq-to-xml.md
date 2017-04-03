---
title: Query compilate in modo statico (LINQ to XML) (C#) | Documentazione Microsoft
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
ms.assetid: 3bf558fe-0705-479d-86d4-00188f5fcf9c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 10e4df75be88dc5609e0ca15666042a0354824bc
ms.lasthandoff: 03/13/2017


---
# <a name="statically-compiled-queries-linq-to-xml-c"></a>Query compilate in modo statico (LINQ to XML) (C#)
Uno dei più importanti vantaggi a livello di prestazioni di LINQ to XML, rispetto a <xref:System.Xml.XmlDocument>, consiste nel fatto che le query in LINQ to XML sono compilate in modo statico, mentre le query XPath devono essere interpretate in fase di esecuzione. Questa funzionalità è incorporata in LINQ to XML, pertanto non è necessario eseguire passaggi aggiuntivi per sfruttarla, ma è utile capire la distinzione per saper scegliere tra le due tecnologie. In questo argomento viene illustrata la differenza  
  
## <a name="statically-compiled-queries-vs-xpath"></a>Confronto tra query compilate in modo statico e XPath  
 Nell'esempio seguente viene illustrato come ottenere gli elementi discendenti con un nome specificato e con un attributo con un valore specificato.  
  
 Di seguito è riportata l'espressione XPath equivalente:  
  
```  
//Address[@Type='Shipping']  
```  
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    from el in po.Descendants("Address")  
    where (string)el.Attribute("Type") == "Shipping"  
    select el;  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 L'espressione di query di questo esempio viene scritta di nuovo dal compilatore nella sintassi delle query basate su metodo. L'esempio seguente, scritto nella sintassi delle query basate su metodo, produce gli stessi risultati del precedente:  
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    po  
    .Descendants("Address")  
    .Where(el => (string)el.Attribute("Type") == "Shipping");  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Il metodo <xref:System.Linq.Enumerable.Where%2A> è un metodo di estensione. Per altre informazioni, vedere [Metodi di estensione](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md). Poiché <xref:System.Linq.Enumerable.Where%2A> è un metodo di estensione, la query precedente è compilata come se fosse scritta come indicato di seguito:  
  
```csharp  
XDocument po = XDocument.Load("PurchaseOrders.xml");  
  
IEnumerable<XElement> list1 =  
    System.Linq.Enumerable.Where(  
        po.Descendants("Address"),  
        el => (string)el.Attribute("Type") == "Shipping");  
  
foreach (XElement el in list1)  
    Console.WriteLine(el);  
```  
  
 Questo esempio produce esattamente gli stessi risultati dei due esempi precedenti. Questo illustra il fatto che le query sono compilate efficacemente in chiamate ai metodi collegate in modo statico. Questo fatto, insieme alla semantica di esecuzione posticipata degli iteratori, consente un miglioramento delle prestazioni. Per altre informazioni sulla semantica dell'esecuzione posticipata degli iteratori, vedere [Esecuzione posticipata e valutazione lazy in LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
> [!NOTE]
>  Questi esempi rappresentano il codice che potrebbe venire scritto dal compilatore. L'implementazione effettiva potrebbe differire leggermente da questi esempi, ma le prestazioni saranno la stesse o simili.  
  
## <a name="executing-xpath-expressions-with-xmldocument"></a>Esecuzione di espressioni XPath con XmlDocument  
 Nell'esempio seguente viene usato <xref:System.Xml.XmlDocument> per ottenere gli stessi risultati degli esempi precedenti:  
  
```csharp  
XmlReader reader = XmlReader.Create("PurchaseOrders.xml");  
XmlDocument doc = new XmlDocument();  
doc.Load(reader);  
XmlNodeList nl = doc.SelectNodes(".//Address[@Type='Shipping']");  
foreach (XmlNode n in nl)  
    Console.WriteLine(n.OuterXml);  
reader.Close();  
```  
  
 Questa query restituisce lo stesso output degli esempi che usano LINQ to XML. L'unica differenza consiste nel fatto che in LINQ to XML viene applicato un rientro al codice XML stampato, mentre in <xref:System.Xml.XmlDocument> no.  
  
 L'utilizzo di <xref:System.Xml.XmlDocument> non garantisce tuttavia lo stesso livello di prestazioni di LINQ to XML, in quanto il metodo <xref:System.Xml.XmlNode.SelectNodes%2A> deve eseguire internamente le operazioni seguenti ogni volta che viene chiamato:  
  
-   Analisi della stringa che contiene l'espressione XPath, suddividendo la stringa in token.  
  
-   Convalida dei token per assicurarsi che l'espressione XPath sia valida.  
  
-   Conversione dell'espressione in un albero delle espressioni interno.  
  
-   Iterazione nei nodi, selezionando in modo appropriato i nodi per il set di risultati in base alla valutazione dell'espressione.  
  
 Queste operazioni sono in numero significativamente maggiore rispetto a quelle eseguite dalla query LINQ to XML corrispondente. La differenza di prestazioni specifica varia per tipi diversi di query, ma in generale le query LINQ to XML comportano un lavoro minore, e pertanto prestazioni migliori, rispetto alla valutazione di espressioni XPath tramite <xref:System.Xml.XmlDocument>.  
  
## <a name="see-also"></a>Vedere anche  
 [Prestazioni (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)
