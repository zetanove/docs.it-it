---
title: Esecuzione di query su XDocument e su Esecuzione di query su XElement (C#) | Microsoft Docs
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
ms.assetid: 46221ff5-62ee-4de8-93ba-66465facb5c1
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9a3da563618ad3dbc9797f252ab51588a43ce8e6
ms.lasthandoff: 03/13/2017


---
# <a name="querying-an-xdocument-vs-querying-an-xelement-c"></a>Esecuzione di query su XDocument e su XElement (C#)
Quando si carica un documento con <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName> si noterà che è necessario scrivere query in modo leggermente diverso rispetto a quando si esegue il caricamento con <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>.  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>Confronto tra XDocument.Load e XElement.Load  
 Quando si carica un documento XML in un oggetto <xref:System.Xml.Linq.XElement> usando <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>, l'oggetto <xref:System.Xml.Linq.XElement> nella radice dell'albero XML contiene l'elemento radice del documento caricato. Tuttavia, quando si carica lo stesso documento XML in un oggetto <xref:System.Xml.Linq.XDocument> con <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>, la radice dell'albero è un nodo <xref:System.Xml.Linq.XDocument> e l'elemento radice del documento caricato è l'unico nodo figlio <xref:System.Xml.Linq.XElement> consentito di <xref:System.Xml.Linq.XDocument>. Gli assi di [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] eseguono operazioni in relazione al nodo radice.  
  
 In questo primo esempio viene caricato un albero XML usando <xref:System.Xml.Linq.XElement.Load%2A>. Viene quindi eseguita una query per gli elementi figlio della radice dell'albero.  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XElement.Load");  
Console.WriteLine("----");  
XElement doc = XElement.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 Come previsto, nell'esempio viene prodotto il seguente output:  
  
```  
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 L'esempio seguente è identico a quello precedente, con l'eccezione che l'albero XML viene caricato in un oggetto <xref:System.Xml.Linq.XDocument> anziché in un oggetto <xref:System.Xml.Linq.XElement>.  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 Questo esempio produce il seguente output:  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
</Root>  
```  
  
 Notare che la stessa query ha restituito l'unico nodo `Root` anziché i tre nodi figlio.  
  
 Per gestire questa situazione, è possibile usare la proprietà <xref:System.Xml.Linq.XDocument.Root%2A> prima di accedere ai metodi degli assi, come illustrato di seguito:  
  
```csharp  
// Create a simple document and write it to a file  
File.WriteAllText("Test.xml", @"<Root>  
    <Child1>1</Child1>  
    <Child2>2</Child2>  
    <Child3>3</Child3>  
</Root>");  
  
Console.WriteLine("Querying tree loaded with XDocument.Load");  
Console.WriteLine("----");  
XDocument doc = XDocument.Load("Test.xml");  
IEnumerable<XElement> childList =  
    from el in doc.Root.Elements()  
    select el;  
foreach (XElement e in childList)  
    Console.WriteLine(e);  
```  
  
 Questa query viene ora eseguita in modo identico alla query sull'albero inserito nella radice di <xref:System.Xml.Linq.XElement>. Questo esempio produce il seguente output:  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Basic Queries (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/basic-queries-linq-to-xml.md) (Query di base (LINQ to XML) (C#)
