---
title: "Valutazione di espressioni XPath con XPathNavigator | Microsoft Docs"
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
ms.assetid: 2913ccf3-f932-4363-8028-9e2d22ce6093
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Valutazione di espressioni XPath con XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce il metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> per valutare un'espressione XPath.  Il metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> rileva un'espressione XPath, la valuta e restituisce un W3C XPath di tipo booleano, numero, stringa o set di nodi, in base al risultato dell'espressione XPath.  
  
## Metodo Evaluate  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> rileva un'espressione XPath, la valuta e restituisce un risultato di tipo booleano\(<xref:System.Boolean>\), numero \(<xref:System.Double>\), stringa \(<xref:System.String>\) o set di nodi \(<xref:System.Xml.XPath.XPathNodeIterator>\).  È possibile ad esempio usare il metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> in un metodo matematico.  Nell'esempio di codice seguente viene calcolato il prezzo totale di tutti i libri nel file `books.xml`.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Dim query As XPathExpression = navigator.Compile("sum(//price/text())")  
Dim total As Double = CType(navigator.Evaluate(query), Double)  
Console.WriteLine(total)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
XPathExpression query = navigator.Compile("sum(//price/text())");  
Double total = (Double)navigator.Evaluate(query);  
Console.WriteLine(total);  
```  
  
 Nell'esempio il file `books.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### Funzioni position e last  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> è un metodo di overload.  Uno dei metodi <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> accetta come parametro un oggetto <xref:System.Xml.XPath.XPathNodeIterator>.  Questo specifico metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> è identico al metodo <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> che accetta solo un oggetto <xref:System.Xml.XPath.XPathExpression> come parametro, ad eccezione del fatto che consente a un argomento set di nodi di specificare il contesto corrente in base al quale eseguire la valutazione.  Questo contesto è necessario per le funzioni `position()` e `last()` di XPath in quanto sono relative al nodo di contesto corrente.  A meno che non vengano usate come predicato in una fase di posizione, per la valutazione delle funzioni `position()` e `last()` è necessario specificare un riferimento a un set di nodi, altrimenti le funzioni `position` e `last` restituiscono `0`.  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Selezione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)   
 [Corrispondenza di nodi utilizzando XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [Tipi di nodo riconosciuti con le query XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)   
 [Query e spazi dei nomi XPath](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)   
 [Espressioni XPath compilate](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)