---
title: Aggiunta di elementi, attributi e nodi a un albero XML (C#) | Microsoft Docs
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
ms.assetid: db911e4f-40aa-499a-9500-a9763bb6df56
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 858d5b2c5ed680a0e52e374b8ec98762d7fde043
ms.lasthandoff: 03/13/2017


---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-c"></a>Aggiunta di elementi, attributi e nodi a un albero XML (C#)
È possibile aggiungere contenuto (elementi, attributi, commenti, istruzioni di elaborazione, testo e CDATA) a un albero XML esistente.  
  
## <a name="methods-for-adding-content"></a>Metodi per l'aggiunta di contenuto  
 I metodi seguenti aggiungono contenuto figlio a <xref:System.Xml.Linq.XElement> o <xref:System.Xml.Linq.XDocument>:  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|Aggiunge contenuto alla fine del contenuto figlio di <xref:System.Xml.Linq.XContainer>.|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|Aggiunge contenuto all'inizio del contenuto figlio di <xref:System.Xml.Linq.XContainer>.|  
  
 I seguenti metodi consentono di aggiungere contenuto come nodi di pari livello di <xref:System.Xml.Linq.XNode>. Il nodo più comune al quale si aggiunge contenuto di pari livello è <xref:System.Xml.Linq.XElement>, sebbene sia possibile aggiungere contenuto di pari livello valido ad altri tipi di nodi, ad esempio <xref:System.Xml.Linq.XText> o <xref:System.Xml.Linq.XComment>.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|Aggiunge contenuto dopo <xref:System.Xml.Linq.XNode>.|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|Aggiunge contenuto prima di <xref:System.Xml.Linq.XNode>.|  
  
## <a name="example"></a>Esempio  
  
### <a name="description"></a>Descrizione  
 Nell'esempio seguente vengono create due strutture ad albero XML e quindi ne viene modificata una.  
  
### <a name="code"></a>Codice  
  
```csharp  
XElement srcTree = new XElement("Root",   
    new XElement("Element1", 1),  
    new XElement("Element2", 2),  
    new XElement("Element3", 3),  
    new XElement("Element4", 4),  
    new XElement("Element5", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child1", 1),  
    new XElement("Child2", 2),  
    new XElement("Child3", 3),  
    new XElement("Child4", 4),  
    new XElement("Child5", 5)  
);  
xmlTree.Add(new XElement("NewChild", "new content"));  
xmlTree.Add(  
    from el in srcTree.Elements()  
    where (int)el > 3  
    select el  
);  
// Even though Child9 does not exist in srcTree, the following statement will not  
// throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"));  
Console.WriteLine(xmlTree);  
```  
  
### <a name="comments"></a>Commenti  
 L'output del codice è il seguente:  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifica degli alberi XML (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
