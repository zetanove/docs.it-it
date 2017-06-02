---
title: "Selezione di dati XML con XPathNavigator | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: c268c49e-32b9-4171-b782-dcb7b065fa73
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Selezione di dati XML con XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usato per selezionare un set di nodi in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument> usando un'espressione XPath.  È possibile scorrere il set di nodi dopo averlo selezionato.  
  
## Metodi di selezione di XPathNavigator  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usato per selezionare un set di nodi in un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument> usando un'espressione XPath.  La classe <xref:System.Xml.XPath.XPathNavigator> fornisce inoltre un set di metodi ottimizzati per selezionare più velocemente i nodi progenitore, figlio e discendente anziché usare un'espressione XPath.  Nel caso di un singolo nodo selezionato, il set di nodi selezionato viene restituito in un oggetto <xref:System.Xml.XPath.XPathNodeIterator> o <xref:System.Xml.XPath.XPathNavigator>.  
  
### Selezione di nodi con le espressioni XPath  
 Per selezionare un set di nodi usando un'espressione XPath, usare uno dei seguenti metodi di selezione.  
  
-   <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 Nel caso di un singolo nodo selezionato, se chiamati, questi metodi restituiscono un set di nodi che può essere esplorato liberamente usando un oggetto <xref:System.Xml.XPath.XPathNodeIterator> o <xref:System.Xml.XPath.XPathNavigator>.  
  
 L'esplorazione di un oggetto <xref:System.Xml.XPath.XPathNodeIterator> non influisce sulla posizione dell'oggetto <xref:System.Xml.XPath.XPathNavigator> usato per crearlo.  L'oggetto <xref:System.Xml.XPath.XPathNavigator> restituito dai metodi <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> è posizionato nel singolo nodo restituito e non influisce sulla posizione dell'oggetto <xref:System.Xml.XPath.XPathNavigator> usato per crearlo.  
  
 Nell'esempio seguente viene illustrata la creazione di un oggetto <xref:System.Xml.XPath.XPathNavigator> da un oggetto <xref:System.Xml.XPath.XPathDocument>, l'uso del metodo <xref:System.Xml.XPath.XPathNavigator.Select%2A> per selezionare nodi nell'oggetto <xref:System.Xml.XPath.XPathDocument> e l'uso dell'oggetto <xref:System.Xml.XPath.XPathNodeIterator> per scorrere i nodi selezionati.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim nodes As XPathNodeIterator = navigator.Select("/bookstore/book")  
  
While nodes.MoveNext()  
    Console.WriteLine(nodes.Current.Name)  
End While  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathNodeIterator nodes = navigator.Select("/bookstore/book");  
  
while(nodes.MoveNext())  
{  
    Console.WriteLine(nodes.Current.Name);  
}  
```  
  
 Nell'esempio il file `books.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### Metodi di selezione ottimizzati  
 I metodi <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> e <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> della classe <xref:System.Xml.XPath.XPathNavigator> rappresentano le espressioni XPath comunemente usate per recuperare nodi figlio, discendente e progenitore.  Questi metodi consentono di ottimizzare le prestazioni e sono più veloci delle espressioni XPath corrispondenti.  I metodi <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>, <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> e <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> consentono di selezionare i nodi progenitore, figlio e discendente in base a un valore <xref:System.Xml.XPath.XPathNodeType> o al nome locale e all'URI dello spazio dei nomi dei nodi da selezionare.  I nodi progenitore, figlio e discendente vengono restituiti in un oggetto <xref:System.Xml.XPath.XPathNodeIterator>.  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Valutazione di espressioni XPath con XPathNavigator](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)   
 [Corrispondenza di nodi utilizzando XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [Tipi di nodo riconosciuti con le query XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)   
 [Query e spazi dei nomi XPath](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)   
 [Espressioni XPath compilate](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)