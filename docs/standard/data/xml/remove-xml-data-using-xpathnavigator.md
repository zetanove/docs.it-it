---
title: "Rimozione di dati XML con XPathNavigator | Microsoft Docs"
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
ms.assetid: 9f436bca-1b96-494b-a6d2-e102c7551752
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Rimozione di dati XML con XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usati per rimuovere nodi e valori da un documento XML.  Per usare questi metodi, è necessario che l'oggetto <xref:System.Xml.XPath.XPathNavigator> sia modificabile, ovvero, la relativa proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> deve essere `true`.  
  
 Gli oggetti <xref:System.Xml.XPath.XPathNavigator> che possono modificare un documento XML vengono creati dal metodo <xref:System.Xml.XmlDocument.CreateNavigator%2A> della classe <xref:System.Xml.XmlDocument>.  Gli oggetti <xref:System.Xml.XPath.XPathNavigator> creati dalla classe <xref:System.Xml.XPath.XPathDocument> sono di sola lettura e qualsiasi tentativo di usare i metodi di modifica di un oggetto <xref:System.Xml.XPath.XPathNavigator> creato da un oggetto <xref:System.Xml.XPath.XPathDocument> genererà un oggetto <xref:System.NotSupportedException>.  
  
 Per altre informazioni sulla creazione di oggetti modificabili <xref:System.Xml.XPath.XPathNavigator>, vedere [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md).  
  
## Rimozione di nodi  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> per rimuovere nodi da un documento XML.  
  
### Rimozione di un nodo  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> per eliminare da un documento XML il nodo corrente su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
 Dopo che un nodo è stato eliminato usando il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A>, non è più possibile raggiungerlo dal livello radice dell'oggetto <xref:System.Xml.XmlDocument>.  Dopo che un nodo è stato eliminato, la classe <xref:System.Xml.XPath.XPathNavigator> viene posizionata sul nodo padre del nodo eliminato.  
  
 Un'operazione di eliminazione non influenza la posizione di un oggetto <xref:System.Xml.XPath.XPathNavigator> collocato sul nodo eliminato.  Questi oggetti <xref:System.Xml.XPath.XPathNavigator> sono validi nel senso che è possibile spostarli all'interno del sottoalbero eliminato ma non è possibile spostarli nell'albero principale dei nodi usando i normali metodi di navigazione dei set di nodi della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
> [!NOTE]
>  È possibile usare il metodo <xref:System.Xml.XPath.XPathNavigator.MoveTo%2A> della classe <xref:System.Xml.XPath.XPathNavigator> per riportare questi oggetti <xref:System.Xml.XPath.XPathNavigator> nell'albero principale dei nodi o per spostarli dall'albero principale al sottoalbero eliminato.  
  
 Nell'esempio seguente l'elemento `price` del primo elemento `book` del file `contosoBooks.xml` viene eliminato usando il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A>.  Dopo che l'elemento `price` è stato eliminato, l'oggetto <xref:System.Xml.XPath.XPathNavigator> è posizionato sull'elemento padre `book`.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.DeleteSelf()  
  
Console.WriteLine("Position after delete: {0}", navigator.Name)  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.DeleteSelf();  
  
Console.WriteLine("Position after delete: {0}", navigator.Name);  
Console.WriteLine(navigator.OuterXml);  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### Rimozione di un nodo Attribute  
 I nodi Attribute vengono rimossi da un documento XML usando il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A>.  
  
 Dopo che un nodo Attribute è stato eliminato, non è più possibile raggiungerlo dal nodo radice di un oggetto <xref:System.Xml.XmlDocument> e l'oggetto <xref:System.Xml.XPath.XPathNavigator> viene posizionato sull'elemento padre.  
  
#### Attributi predefiniti  
 Indipendentemente dal metodo usato per rimuovere gli attributi, la rimozione di attributi definiti come attributi predefiniti nella DTD o in XML Schema per il documento XML è soggetta ad alcuni limiti specifici.  Non è possibile rimuovere gli attributi predefiniti, a meno che non venga rimosso anche l'elemento al quale appartengono.  Gli attributi predefiniti sono sempre presenti per gli elementi con attributi predefiniti dichiarati. Di conseguenza, l'eliminazione di un attributo predefinito determina l'inserimento di un attributo di sostituzione nell'elemento e la relativa inizializzazione in base al valore predefinito che era stato dichiarato.  
  
## Rimozione di valore  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> per rimuovere valori tipizzati e non tipizzati da un documento XML.  
  
### Rimozione di valori non tipizzati  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> consente semplicemente di inserire il valore non tipizzato `string`, passato come parametro, come valore del nodo su cui è attualmente posizionato l'oggetto <xref:System.Xml.XPath.XPathNavigator>.  Il passaggio di una stringa vuota al metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> causa la rimozione del valore del nodo corrente.  
  
 Nell'esempio seguente il valore dell'elemento `price` del primo elemento `book` del file `contosoBooks.xml` viene rimosso usando il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A>.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetValue("")  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.SetValue("");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### Rimozione di valori tipizzati  
 Quando il tipo di un nodo è un tipo semplice di W3C XML Schema, il nuovo valore inserito tramite il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> viene controllato rispetto ai facet del tipo semplice prima dell'impostazione del valore.  Se il nuovo valore non è valido in base al tipo del nodo \(ad esempio, l'impostazione di un valore `-1` su un elemento il cui tipo è `xs:positiveInteger`\), viene generata un'eccezione.  Anche al metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> non può essere passato il valore `null` come parametro.  Di conseguenza la rimozione del valore di un nodo tipizzato deve essere conforme al tipo di schema del nodo.  
  
 Nell'esempio seguente il valore dell'elemento `price` del primo elemento `book` del file `contosoBooks.xml` viene rimosso usando il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A>, impostando il valore su `0`.  Il valore del nodo non viene rimosso, ma il prezzo del libro è stato rimosso in base al relativo tipo di dati `xs:decimal`.  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetTypedValue(0)  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.SetTypedValue(0);  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
## Nodi dello spazio dei nomi  
 Non è possibile eliminare i nodi dello spazio dei nomi da un oggetto <xref:System.Xml.XmlDocument>.  I tentativi di eliminare i nodi dello spazio dei nomi usando il metodo <xref:System.Xml.XPath.XPathNavigator.DeleteSelf%2A> generano un'eccezione.  
  
## Proprietà InnerXml e OuterXml  
 Le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> della classe <xref:System.Xml.XPath.XPathNavigator> consentono di modificare il markup XML dei nodi su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
 La proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> con il contenuto analizzato della `string` XML specificata.  Allo stesso modo, la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> nonché il nodo corrente stesso.  
  
 Oltre ai metodi descritti in questo argomento, è possibile usare le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> per rimuovere nodi e valori da un documento XML.  Per altre informazioni sull'utilizzo delle proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A>, vedere l'argomento [Modifica dei dati XML con XPathNavigator](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md).  
  
## Salvataggio di un documento XML  
 Il salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument> mediante i metodi descritti in questo argomento viene eseguito usando i metodi della classe <xref:System.Xml.XmlDocument>.  Per altre informazioni sul salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument>, vedere [Salvataggio e scrittura di un documento](../../../../docs/standard/data/xml/saving-and-writing-a-document.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Inserimento dei dati XML utilizzando XPathNavigator](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)   
 [Modifica dei dati XML con XPathNavigator](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md)