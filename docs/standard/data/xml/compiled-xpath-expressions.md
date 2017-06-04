---
title: "Espressioni XPath compilate | Microsoft Docs"
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
ms.assetid: e25dd95f-b64c-4d8b-a3a4-379e1aa0ad55
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Espressioni XPath compilate
Un oggetto <xref:System.Xml.XPath.XPathExpression> rappresenta una query XPath compilata che viene restituita dal metodo statico <xref:System.Xml.XPath.XPathExpression.Compile%2A> della classe <xref:System.Xml.XPath.XPathExpression> oppure dal metodo <xref:System.Xml.XPath.XPathNavigator.Compile%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
## Classe XPathExpression  
 Una query XPath compilata rappresentata da un oggetto <xref:System.Xml.XPath.XPathExpression> risulta utile se la stessa query XPath viene usata più volte.  
  
 Ad esempio, se si chiama il metodo <xref:System.Xml.XPath.XPathNavigator.Select%2A> più volte, anziché usare ogni volta una stringa che rappresenti la query XPath, è possibile usare il metodo <xref:System.Xml.XPath.XPathExpression.Compile%2A> della classe <xref:System.Xml.XPath.XPathExpression> oppure il metodo <xref:System.Xml.XPath.XPathNavigator.Compile%2A> della classe <xref:System.Xml.XPath.XPathNavigator> per compilare e memorizzare nella cache la query XPath in un oggetto <xref:System.Xml.XPath.XPathExpression> e poterla riutilizzare migliorando le prestazioni.  
  
 Una volta compilato, l'oggetto <xref:System.Xml.XPath.XPathExpression> può essere usato come input ai seguenti metodi della classe <xref:System.Xml.XPath.XPathNavigator> in base al tipo restituito dalla query XPath.  
  
-   <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.XPath.XPathNavigator.Matches%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 Nella tabella seguente vengono descritti ciascun tipo W3C XPath restituito, il tipo equivalente di Microsoft .NET Frameworks e i metodi che possono essere usati dall'oggetto <xref:System.Xml.XPath.XPathExpression> in base al relativo tipo restituito.  
  
|Tipo W3C XPath restituito|Tipo equivalente di .NET Framework|Descrizione|Metodi|  
|-------------------------------|----------------------------------------|-----------------|------------|  
|`Node set`|<xref:System.Xml.XPath.XPathNodeIterator>|Raccolta non ordinata di nodi senza duplicati creati in ordine di documento.|<xref:System.Xml.XPath.XPathNavigator.Select%2A> oppure <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`Boolean`|<xref:System.Boolean>|Valore `true` o `false`.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> oppure<br /><br /> <xref:System.Xml.XPath.XPathNavigator.Matches%2A>|  
|`Number`|<xref:System.Double>|Numero a virgola mobile.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
|`String`|<xref:System.String>|Sequenza di caratteri UCS.|<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>|  
  
> [!NOTE]
>  Il metodo <xref:System.Xml.XPath.XPathNavigator.Matches%2A> accetta come parametro un'espressione XPath.  Il metodo <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> restituisce un oggetto <xref:System.Xml.XPath.XPathNavigator> e non uno dei tipi W3C XPath restituiti.  
  
### Proprietà ReturnType  
 Una volta compilata una query XPath in un oggetto <xref:System.Xml.XPath.XPathExpression>, è possibile usare la proprietà <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> dell'oggetto <xref:System.Xml.XPath.XPathExpression> per determinare ciò che restituisce la query XPath.  
  
 La proprietà <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> restituisce uno dei seguenti valori di enumerazione <xref:System.Xml.XPath.XPathResultType> che rappresenta il tipo W3C XPath restituito.  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
-   <xref:System.Xml.XPath.XPathResultType>  
  
 Nell'esempio seguente viene usato l'oggetto <xref:System.Xml.XPath.XPathExpression> per restituire un numero e un set di nodi dal file `books.xml`.  La proprietà <xref:System.Xml.XPath.XPathExpression.ReturnType%2A> di ciascun oggetto <xref:System.Xml.XPath.XPathExpression> e i risultati dai metodi <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> e <xref:System.Xml.XPath.XPathNavigator.Select%2A> vengono scritti nella console.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Returns a number.  
Dim query1 As XPathExpression = navigator.Compile("bookstore/book/price/text()*10")  
Console.WriteLine(query1.ReturnType)  
  
Dim number As Double = CType(navigator.Evaluate(query1), Double)  
Console.WriteLine(number)  
  
' Returns a node set.  
Dim query2 As XPathExpression = navigator.Compile("bookstore/book/price")  
Console.WriteLine(query2.ReturnType)  
  
Dim nodes As XPathNodeIterator = navigator.Select(query2)  
nodes.MoveNext()  
Console.WriteLine(nodes.Current.Value)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Returns a number.  
XPathExpression query1 = navigator.Compile("bookstore/book/price/text()*10");  
Console.WriteLine(query1.ReturnType);  
  
Double number = (Double)navigator.Evaluate(query1);  
Console.WriteLine(number);  
  
// Returns a node set.  
XPathExpression query2 = navigator.Compile("bookstore/book/price");  
Console.WriteLine(query2.ReturnType);  
  
XPathNodeIterator nodes = navigator.Select(query2);  
nodes.MoveNext();  
Console.WriteLine(nodes.Current.Value);  
```  
  
 Nell'esempio il file `books.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### Espressioni XPath a prestazioni più elevate  
 Per ottimizzare le prestazioni, si consiglia di usare l'espressione XPath più specifica possibile nelle query.  Ad esempio, se il nodo `book` è un nodo figlio del nodo `bookstore` e il nodo `bookstore` è l'elemento principale di un documento XML, l'uso dell'espressione XPath `/bookstore/book` garantisce una velocità maggiore rispetto all'utilizzo di `//book`.  Per identificare i nodi corrispondenti, infatti, l'espressione XPath `//book` eseguirà l'analisi di ciascun nodo nell'albero XML.  
  
 Inoltre, nei casi in cui i criteri di selezione sono semplici, l'uso dei metodi di navigazione dei set di nodi forniti dalla classe <xref:System.Xml.XPath.XPathNavigator> può garantire un livello di prestazioni più elevato rispetto a quello fornito dai metodi della classe <xref:System.Xml.XPath.XPathNavigator>.  Ad esempio, se è necessario selezionare il primo nodo figlio del nodo corrente, risulta più veloce usare il metodo <xref:System.Xml.XPath.XPathNavigator.MoveToFirst%2A> anziché l'espressione XPath `child::*[1]` e il metodo <xref:System.Xml.XPath.XPathNavigator.Select%2A>.  
  
 Per altre informazioni sui metodi di navigazione dei set di nodi della classe <xref:System.Xml.XPath.XPathNavigator>, vedere [Navigazione del set di nodi con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Selezione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)   
 [Valutazione di espressioni XPath con XPathNavigator](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)   
 [Corrispondenza di nodi utilizzando XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [Tipi di nodo riconosciuti con le query XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)   
 [Query e spazi dei nomi XPath](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)