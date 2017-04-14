---
title: "Estrazione di dati XML con XPathNavigator | Microsoft Docs"
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
ms.assetid: 095b0987-ee4b-4595-a160-da1c956ad576
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Estrazione di dati XML con XPathNavigator
Sono disponibili diversi metodi per rappresentare un documento XML in Microsoft .NET Framework,  inclusi l'uso di una classe <xref:System.String> o l'uso delle classi <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>, <xref:System.Xml.XmlDocument> o <xref:System.Xml.XPath.XPathDocument>.  Per facilitare lo spostamento tra queste diverse rappresentazioni di un documento XML, la classe <xref:System.Xml.XPath.XPathNavigator> offre una serie di metodi e proprietà per estrarre i dati XML come oggetto <xref:System.String>, <xref:System.Xml.XmlReader> o come oggetto <xref:System.Xml.XmlWriter>.  
  
## Conversione di un XPathNavigator in stringa  
 ‎La proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> della classe <xref:System.Xml.XPath.XPathNavigator> viene usata per ottenere il markup dell'intero documento XML o di un singolo nodo e dei relativi nodi figlio.  
  
> [!NOTE]
>  La proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> ottiene solo il markup dei nodi figlio di un nodo.  
  
 Nell'esempio di codice seguente viene illustrato come salvare un intero documento XML contenuto in un oggetto <xref:System.Xml.XPath.XPathNavigator> come <xref:System.String>, sotto forma di nodo singolo assieme ai relativi nodi figlio.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("input.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Save the entire input.xml document to a string.  
Dim xml As String = navigator.OuterXml  
  
' Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element)  
Dim root As String = navigator.OuterXml  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Save the entire input.xml document to a string.  
string xml = navigator.OuterXml;  
  
// Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element);  
string root = navigator.OuterXml;  
```  
  
## Conversione di un XPathNavigator in XmlReader  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> viene usato per inviare il flusso dell'intero contenuto di un documento XML o solo di un singolo nodo e dei relativi nodi figlio a un oggetto <xref:System.Xml.XmlReader>.  
  
 Quando viene creato l'oggetto <xref:System.Xml.XmlReader> con il nodo corrente e i relativi nodi figlio, la proprietà <xref:System.Xml.XmlReader.ReadState%2A> dell'oggetto <xref:System.Xml.XmlReader> viene impostata su <xref:System.Xml.ReadState>.  Quando il metodo <xref:System.Xml.XmlReader.Read%2A> dell'oggetto <xref:System.Xml.XmlReader> viene chiamato la prima volta, l'oggetto <xref:System.Xml.XmlReader> viene spostato sul nodo corrente dell'oggetto <xref:System.Xml.XPath.XPathNavigator>.  Il nuovo oggetto <xref:System.Xml.XmlReader> prosegue la lettura fino a quando non viene raggiunta la fine dell'albero XML.  A questo punto il metodo <xref:System.Xml.XmlReader.Read%2A> restituisce `false` e la proprietà <xref:System.Xml.XmlReader.ReadState%2A> dell'oggetto <xref:System.Xml.XmlReader> viene impostata su <xref:System.Xml.ReadState>.  
  
 La posizione dell'oggetto <xref:System.Xml.XPath.XPathNavigator> non è stata modificata dalla creazione o dallo spostamento dell'oggetto <xref:System.Xml.XmlReader>.  Il metodo <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> è valido solo se è posizionato in corrispondenza di un elemento o di un nodo radice.  
  
 Nell'esempio di codice seguente viene illustrato come ottenere un oggetto <xref:System.Xml.XmlReader> contenente l'intero documento XML contenuto in un oggetto <xref:System.Xml.XPath.XPathDocument> sotto forma di nodo singolo assieme ai relativi nodi figlio.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlReader.  
Dim xml As XmlReader = navigator.ReadSubtree()  
  
While xml.Read()  
    Console.WriteLine(xml.ReadInnerXml())  
End While  
  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlReader = navigator.ReadSubtree()  
  
While book.Read()  
    Console.WriteLine(book.ReadInnerXml())  
End While  
  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlReader.  
XmlReader xml = navigator.ReadSubtree();  
  
while (xml.Read())  
{  
    Console.WriteLine(xml.ReadInnerXml());  
}  
  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlReader book = navigator.ReadSubtree();  
  
while (book.Read())  
{  
    Console.WriteLine(book.ReadInnerXml());  
}  
  
book.Close();  
```  
  
 Nell'esempio il file `books.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
## Conversione di un XPathNavigator in XmlWriter  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> viene usato per inviare il flusso dell'intero contenuto di un documento XML o solo di un singolo nodo e dei relativi nodi figlio a un oggetto <xref:System.Xml.XmlWriter>.  
  
 La posizione dell'oggetto <xref:System.Xml.XPath.XPathNavigator> non è stata modificata dalla creazione dell'oggetto <xref:System.Xml.XmlWriter>.  
  
 Nell'esempio di codice seguente viene illustrato come ottenere un oggetto <xref:System.Xml.XmlWriter> contenente l'intero documento XML contenuto in un oggetto <xref:System.Xml.XPath.XPathDocument> sotto forma di nodo singolo assieme ai relativi nodi figlio.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlWriter.  
Dim xml As XmlWriter = XmlWriter.Create("newbooks.xml")  
navigator.WriteSubtree(xml)  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlWriter = XmlWriter.Create("book.xml")  
navigator.WriteSubtree(book)  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlWriter.  
XmlWriter xml = XmlWriter.Create("newbooks.xml");  
navigator.WriteSubtree(xml);  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlWriter book = XmlWriter.Create("book.xml");  
navigator.WriteSubtree(book);  
book.Close();  
```  
  
 Nell'esempio il file `books.xml`, trovato prima in questo argomento, viene considerato come input.  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Navigazione del set di nodi con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)   
 [Navigazione dei nodi di attributi e dello spazio dei nomi con XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)   
 [Accesso a dati XML fortemente tipizzati con XPathNavigator](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)