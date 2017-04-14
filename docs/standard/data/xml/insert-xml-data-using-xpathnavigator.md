---
title: "Inserimento dei dati XML utilizzando XPathNavigator | Microsoft Docs"
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
ms.assetid: 2ed8c28b-b88d-4be7-9c87-92df01f0821f
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Inserimento dei dati XML utilizzando XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usati per inserire nodi di pari livello, nodi figlio e nodi Attribute in un documento XML.  Per usare questi metodi, è necessario che l'oggetto <xref:System.Xml.XPath.XPathNavigator> sia modificabile, ovvero, la relativa proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> deve essere `true`.  
  
 Gli oggetti <xref:System.Xml.XPath.XPathNavigator> che possono modificare un documento XML vengono creati dal metodo <xref:System.Xml.XmlDocument.CreateNavigator%2A> della classe <xref:System.Xml.XmlDocument>.  Gli oggetti <xref:System.Xml.XPath.XPathNavigator> creati dalla classe <xref:System.Xml.XPath.XPathDocument> sono di sola lettura e qualsiasi tentativo di usare i metodi di modifica di un oggetto <xref:System.Xml.XPath.XPathNavigator> creato da un oggetto <xref:System.Xml.XPath.XPathDocument> genererà un oggetto <xref:System.NotSupportedException>.  
  
 Per altre informazioni sulla creazione di oggetti modificabili <xref:System.Xml.XPath.XPathNavigator>, vedere [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md).  
  
## Inserimento di nodi  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i metodi per inserire nodi di pari livello, nodi figlio e nodi Attribute in un documento XML.  Tali metodi consentono di inserire nodi e attributi in diverse posizioni in relazione alla posizione corrente di un oggetto <xref:System.Xml.XPath.XPathNavigator> e vengono descritti nelle seguenti sezioni.  
  
### Inserimento di nodi di pari livello  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i seguenti metodi per inserire nodi di pari livello.  
  
-   <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A>  
  
 Tali metodi consentono di inserire nodi di pari livello prima e dopo il nodo su cui l'oggetto <xref:System.Xml.XPath.XPathNavigator> è attualmente posizionato.  
  
 I metodi <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A> e <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A> sono in overload e accettano un oggetto `string`, <xref:System.Xml.XmlReader> o un oggetto <xref:System.Xml.XPath.XPathNavigator> contenente il nodo di pari livello da aggiungere come parametro.  Entrambi i metodi restituiscono inoltre un oggetto <xref:System.Xml.XmlWriter> usato per inserire i nodi di pari livello.  
  
 Nei metodi <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A> e <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A> viene inserito un nodo singolo di pari livello prima e dopo il nodo su cui un oggetto <xref:System.Xml.XPath.XPathNavigator> è attualmente posizionato usando come parametri il prefisso dello spazio dei nomi, il nome locale, l'URI dello spazio dei nomi e il valore specificato.  
  
 Nell'esempio seguente viene inserito un nuovo elemento `pages` prima dell'elemento figlio `price` del primo elemento `book` nel file `contosoBooks.xml`.  
  
 [!code-cpp[XPathNavigatorMethods#19](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#19)]
 [!code-csharp[XPathNavigatorMethods#19](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#19)]
 [!code-vb[XPathNavigatorMethods#19](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#19)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Per altre informazioni sui metodi <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertElementAfter%2A> e <xref:System.Xml.XPath.XPathNavigator.InsertElementBefore%2A>, vedere la documentazione di riferimento per la classe <xref:System.Xml.XPath.XPathNavigator>.  
  
### Inserimento di nodi figlio  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i seguenti metodi per inserire nodi figlio.  
  
-   <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A>  
  
 In tali metodi i nodi figlio sono aggiunti o anteposti alla fine e all'inizio dell'elenco dei nodi figlio del nodo sul quale un oggetto <xref:System.Xml.XPath.XPathNavigator> è attualmente posizionato.  
  
 Analogamente ai metodi descritti nella sezione "Inserimento di nodi di pari livello", nei metodi <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A> e <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> viene accettato un oggetto `string`, <xref:System.Xml.XmlReader> o un oggetto <xref:System.Xml.XPath.XPathNavigator> contenente il nodo figlio da aggiungere come parametri.  Entrambi i metodi restituiscono inoltre un oggetto <xref:System.Xml.XmlWriter> usato per inserire i nodi figlio.  
  
 Analogamente ai metodi descritti nella sezione "Inserimento di nodi di pari livello", nei metodi <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A> e <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A> viene inserito un singolo nodo figlio alla fine e all'inizio dell'elenco dei nodi figlio del nodo su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> usando come parametri il prefisso dello spazio dei nomi, il nome locale, l'URI dello spazio dei nomi e il valore specificato.  
  
 Nell'esempio seguente, viene aggiunto un nuovo elemento figlio `pages` all'elenco degli elementi figlio del primo elemento `book` nel file `contosoBooks.xml`.  
  
 [!code-cpp[XPathNavigatorMethods#2](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#2)]
 [!code-csharp[XPathNavigatorMethods#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#2)]
 [!code-vb[XPathNavigatorMethods#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#2)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Per altre informazioni sui metodi <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChildElement%2A> e <xref:System.Xml.XPath.XPathNavigator.PrependChildElement%2A>, vedere la documentazione di riferimento per la classe <xref:System.Xml.XPath.XPathNavigator>.  
  
### Inserimento di nodi Attribute  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i seguenti metodi per inserire nodi Attribute.  
  
-   <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A>  
  
 Tali metodi consentono di inserire nodi Attribute sul nodo di tipo element su cui un oggetto <xref:System.Xml.XPath.XPathNavigator> è attualmente posizionato.  Nel metodo <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> viene creato un nodo Attribute sul nodo di tipo element su cui un oggetto <xref:System.Xml.XPath.XPathNavigator> è attualmente posizionato usando come parametri il prefisso dello spazio dei nomi, il nome locale, l'URI dello spazio dei nomi e il valore specificato.  Il metodo <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> restituisce un oggetto <xref:System.Xml.XmlWriter> usato per inserire i nodi Attribute.  
  
 Nell'esempio seguente vengono creati nuovi attributi `discount` e `currency` sull'elemento figlio `price` del primo elemento `book` nel file `contosoBooks.xml` usando l'oggetto <xref:System.Xml.XmlWriter> restituito dal metodo <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A>.  
  
 [!code-cpp[XPathNavigatorMethods#8](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#8)]
 [!code-csharp[XPathNavigatorMethods#8](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#8)]
 [!code-vb[XPathNavigatorMethods#8](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#8)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Per altre informazioni sui metodi <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> e <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A>, vedere la documentazione di riferimento per la classe <xref:System.Xml.XPath.XPathNavigator>.  
  
## Copia di nodi  
 In alcuni casi può essere necessario compilare un documento XML con il contenuto di un altro documento XML.  Entrambe le classi <xref:System.Xml.XPath.XPathNavigator> e <xref:System.Xml.XmlWriter> sono in grado di copiare i nodi in un oggetto<xref:System.Xml.XmlDocument> proveniente da un oggetto <xref:System.Xml.XmlReader> esistente o da un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
 Gli overload dei metodi <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A> e <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A> della classe <xref:System.Xml.XPath.XPathNavigator> accettano tutti un oggetto <xref:System.Xml.XPath.XPathNavigator> o un oggetto <xref:System.Xml.XmlReader> come parametro.  
  
 Gli overload del metodo <xref:System.Xml.XmlWriter.WriteNode%2A> della classe <xref:System.Xml.XmlWriter> possono accettare un oggetto <xref:System.Xml.XmlNode>, <xref:System.Xml.XmlReader> o <xref:System.Xml.XPath.XPathNavigator>.  
  
 Nell'esempio seguente tutti gli elementi `book` vengono copiati da un documento all'altro.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
  
Dim newBooks As XPathDocument = New XPathDocument("newBooks.xml")  
Dim newBooksNavigator As XPathNavigator = newBooks.CreateNavigator()  
  
Dim nav As XPathNavigator  
For Each nav in newBooksNavigator.SelectDescendants("book", "", false)  
    navigator.AppendChild(nav)  
Next  
  
document.Save("newBooks.xml");  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
  
XPathDocument newBooks = new XPathDocument("newBooks.xml");  
XPathNavigator newBooksNavigator = newBooks.CreateNavigator();  
  
foreach (XPathNavigator nav in newBooksNavigator.SelectDescendants("book", "", false))  
{  
    navigator.AppendChild(nav);  
}  
  
document.Save("newBooks.xml");  
```  
  
## Inserimento dei valori  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce i metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> per inserire i valori di un nodo in un oggetto <xref:System.Xml.XmlDocument>.  
  
### Inserimento di valori non tipizzati  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> consente semplicemente di inserire il valore non tipizzato `string`, passato come parametro, come valore del nodo su cui è attualmente posizionato l'oggetto <xref:System.Xml.XPath.XPathNavigator>.  Il valore viene inserito senza alcun tipo o senza verificare la validità del nuovo valore in base al tipo del nodo se sono disponibili le informazioni sullo schema.  
  
 Nell'esempio seguente, il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> viene usato per aggiornare tutti gli elementi `price` nel file `contosoBooks.xml`.  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### Inserimento di valori tipizzati  
 Quando il tipo di un nodo è un tipo semplice di W3C XML Schema, il nuovo valore inserito tramite il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> viene controllato rispetto ai facet del tipo semplice prima dell'impostazione del valore.  Se il nuovo valore non è valido in base al tipo del nodo \(ad esempio, l'impostazione di un valore `-1` su un elemento il cui tipo è `xs:positiveInteger`\), viene generata un'eccezione.  
  
 Nell'esempio seguente si tenta di modificare il valore dell'elemento `price` del primo elemento `book` nel file `contosoBooks.xml` in un valore <xref:System.DateTime>.  Poiché il tipo XML Schema dell'elemento `price` viene definito come `xs:decimal` nei file `contosoBooks.xsd`, viene generata un'eccezione.  
  
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
  
navigator.SetTypedValue(DateTime.Now)  
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
  
navigator.SetTypedValue(DateTime.Now);  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Anche il file `contosoBooks.xsd` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
## Proprietà InnerXml e OuterXml  
 Le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> della classe <xref:System.Xml.XPath.XPathNavigator> consentono di modificare il markup XML dei nodi su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
 La proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> con il contenuto analizzato della `string` XML specificata.  Allo stesso modo, la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> nonché il nodo corrente stesso.  
  
 Oltre ai metodi descritti in questo argomento, è possibile usare le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> per rimuovere nodi e valori da un documento XML.  Per altre informazioni sull'utilizzo delle proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> per l'inserimento di nodi e valori, vedere l'argomento [Modifica dei dati XML con XPathNavigator](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md).  
  
## Conflitti tra spazio dei nomi e xml:lang  
 Determinati conflitti relativi all'ambito dello spazio dei nomi e delle dichiarazioni `xml:lang` possono verificarsi quando si inseriscono i dati XML usando i metodi <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A> e <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> della classe<xref:System.Xml.XPath.XPathNavigator> che accetta oggetti <xref:System.Xml.XmlReader> come parametri.  
  
 Di seguito sono riportati alcuni tra i possibili conflitti tra gli spazi dei nomi.  
  
-   Se viene rilevato uno spazio dei nomi nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader>, in cui il mapping del prefisso URI dello spazio dei nomi non si trova nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, viene aggiunta una nuova dichiarazione dello spazio dei nomi al nuovo nodo inserito.  
  
-   Se lo stesso URI dello spazio dei nomi si trova sia nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader> che nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, ma con un diverso prefisso mappato in entrambi i contesti, viene aggiunta una nuova dichiarazione dello spazio dei nomi al nuovo nodo inserito, con prefisso e URI dello spazio dei nomi tratti dall'oggetto <xref:System.Xml.XmlReader>.  
  
-   Se lo stesso prefisso dello spazio dei nomi si trova sia nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader> che nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, ma con un diverso URI dello spazio dei nomi mappato in entrambi i contesti, viene aggiunta una nuova dichiarazione dello spazio dei nomi al nuovo nodo inserito, che ridichiara il prefisso con l'URI dello spazio dei nomi tratto dall'oggetto <xref:System.Xml.XmlReader>.  
  
-   Se il prefisso e l'URI dello spazio dei nomi in entrambi i contesti dell'oggetto <xref:System.Xml.XmlReader> e dell'oggetto <xref:System.Xml.XPath.XPathNavigator> sono gli stessi, non viene aggiunta alcuna nuova dichiarazione dello spazio dei nomi al nuovo nodo inserito.  
  
> [!NOTE]
>  La descrizione precedente è valida anche per le dichiarazioni dello spazio dei nomi con la `string` vuota come prefisso \(ad esempio la dichiarazione dello spazio dei nomi predefinita\).  
  
 Di seguito sono riportati alcuni tra i possibili conflitti `xml:lang`.  
  
-   Se viene rilevato un attributo `xml:lang` nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader> ma non nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, viene aggiunto al nuovo nodo inserito un attributo `xml:lang` il cui valore viene tratto dall'oggetto <xref:System.Xml.XmlReader>.  
  
-   Se viene rilevato un attributo `xml:lang` sia nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader> che nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, ma ciascuno con un valore diverso, viene aggiunto al nuovo nodo inserito un attributo `xml:lang` il cui valore viene tratto dall'oggetto <xref:System.Xml.XmlReader>.  
  
-   Se viene rilevato un attributo `xml:lang` sia nell'ambito del contesto dell'oggetto <xref:System.Xml.XmlReader> che nel contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator>, ma ciascuno con lo stesso valore, non viene aggiunto alcun nuovo attributo `xml:lang` al nodo appena inserito.  
  
-   Se viene rilevato un attributo `xml:lang` nell'ambito del contesto dell'oggetto <xref:System.Xml.XPath.XPathNavigator> ma non nel contesto dell'oggetto <xref:System.Xml.XmlReader>, non viene aggiunto alcun attributo `xml:lang` al nuovo nodo inserito.  
  
## Inserimento di nodi con XmlWriter  
 I metodi usati per inserire nodi di pari livello, nodi figlio e nodi Attribute descritti nella sezione "Inserimento di nodi e valori" sono in overload.  I metodi <xref:System.Xml.XPath.XPathNavigator.InsertAfter%2A>, <xref:System.Xml.XPath.XPathNavigator.InsertBefore%2A>, <xref:System.Xml.XPath.XPathNavigator.AppendChild%2A>, <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> e <xref:System.Xml.XPath.XPathNavigator.CreateAttributes%2A> della classe <xref:System.Xml.XPath.XPathNavigator> restituiscono un oggetto <xref:System.Xml.XmlWriter> usato per inserire i nodi.  
  
### Metodi XmlWriter non supportati  
 Non tutti i metodi usati per scrivere le informazioni in un documento XML usando la classe <xref:System.Xml.XmlWriter> sono supportati dalla classe <xref:System.Xml.XPath.XPathNavigator> a causa della differenza tra il modello dati XPath e il modello DOM \(Document Object Model\).  
  
 Nella tabella seguente vengono descritti i metodi della classe <xref:System.Xml.XmlWriter> non supportati dalla classe <xref:System.Xml.XPath.XPathNavigator>.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|<xref:System.Xml.XmlWriter.WriteEntityRef%2A>|Genera un'eccezione <xref:System.NotSupportedException>.|  
|<xref:System.Xml.XmlWriter.WriteDocType%2A>|Ignorato al livello radice e genera un'eccezione <xref:System.NotSupportedException> se chiamato a qualsiasi altro livello nel documento XML.|  
|<xref:System.Xml.XmlWriter.WriteCData%2A>|Considerato come una chiamata al metodo <xref:System.Xml.XmlWriter.WriteString%2A> per il carattere o i caratteri equivalenti.|  
|<xref:System.Xml.XmlWriter.WriteCharEntity%2A>|Considerato come una chiamata al metodo <xref:System.Xml.XmlWriter.WriteString%2A> per il carattere o i caratteri equivalenti.|  
|<xref:System.Xml.XmlWriter.WriteSurrogateCharEntity%2A>|Considerato come una chiamata al metodo <xref:System.Xml.XmlWriter.WriteString%2A> per il carattere o i caratteri equivalenti.|  
  
 Per altre informazioni sulla classe <xref:System.Xml.XmlWriter>, vedere la documentazione di riferimento per la classe <xref:System.Xml.XmlWriter>.  
  
### Più oggetti XmlWriter  
 È possibile disporre di più oggetti <xref:System.Xml.XPath.XPathNavigator> che scelgono parti diverse di un documento XML con uno o più oggetti <xref:System.Xml.XmlWriter> aperti.  Sono consentiti e supportati più oggetti <xref:System.Xml.XmlWriter> in scenari a thread singolo.  
  
 Di seguito sono riportate note importanti relative all'utilizzo di più oggetti <xref:System.Xml.XmlWriter>.  
  
-   I frammenti XML scritti dagli oggetti <xref:System.Xml.XmlWriter> vengono aggiunti al documento XML quando viene chiamato il metodo <xref:System.Xml.XmlWriter.Close%2A> di ciascun oggetto <xref:System.Xml.XmlWriter>.  Fino a quel punto, l'oggetto <xref:System.Xml.XmlWriter> sta scrivendo un frammento disconnesso.  Se viene eseguita un'operazione sul documento XML, i frammenti scritti da un oggetto <xref:System.Xml.XmlWriter> prima che sia stato chiamato il metodo <xref:System.Xml.XmlWriter.Close%2A> non sono interessati dall'operazione.  
  
-   Se viene rilevato un oggetto <xref:System.Xml.XmlWriter> aperto in un particolare sottoalbero XML che viene in seguito eliminato, l'oggetto <xref:System.Xml.XmlWriter> può ancora essere aggiunto al sottoalbero.  Il sottoalbero diviene semplicemente un frammento eliminato.  
  
-   Se più oggetti <xref:System.Xml.XmlWriter> vengono aperti nello stesso punto del documento XML, verranno aggiunti al documento XML in base all'ordine in cui gli oggetti<xref:System.Xml.XmlWriter> sono stati chiusi, non nell'ordine in base al quale sono stati aperti.  
  
 Nell'esempio seguente viene creato un oggetto <xref:System.Xml.XmlDocument>, quindi un oggetto <xref:System.Xml.XPath.XPathNavigator> e infine viene usato l'oggetto <xref:System.Xml.XmlWriter> restituito dal metodo <xref:System.Xml.XPath.XPathNavigator.PrependChild%2A> per creare la struttura del primo libro nel file `books.xml`.  L'oggetto viene quindi salvato come file `book.xml`.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Using writer As XmlWriter = navigator.PrependChild()  
  
    writer.WriteStartElement("bookstore")  
    writer.WriteStartElement("book")  
    writer.WriteAttributeString("genre", "autobiography")  
    writer.WriteAttributeString("publicationdate", "1981-03-22")  
    writer.WriteAttributeString("ISBN", "1-861003-11-0")  
    writer.WriteElementString("title", "The Autobiography of Benjamin Franklin")  
    writer.WriteStartElement("author")  
    writer.WriteElementString("first-name", "Benjamin")  
    writer.WriteElementString("last-name", "Franklin")  
    writer.WriteElementString("price", "8.99")  
    writer.WriteEndElement()  
    writer.WriteEndElement()  
    writer.WriteEndElement()  
  
End Using  
  
document.Save("book.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
XPathNavigator navigator = document.CreateNavigator();  
  
using (XmlWriter writer = navigator.PrependChild())  
{  
    writer.WriteStartElement("bookstore");  
    writer.WriteStartElement("book");  
    writer.WriteAttributeString("genre", "autobiography");  
    writer.WriteAttributeString("publicationdate", "1981-03-22");  
    writer.WriteAttributeString("ISBN", "1-861003-11-0");  
    writer.WriteElementString("title", "The Autobiography of Benjamin Franklin");  
    writer.WriteStartElement("author");  
    writer.WriteElementString("first-name", "Benjamin");  
    writer.WriteElementString("last-name", "Franklin");  
    writer.WriteElementString("price", "8.99");  
    writer.WriteEndElement();  
    writer.WriteEndElement();  
    writer.WriteEndElement();  
}  
document.Save("book.xml");  
```  
  
## Salvataggio di un documento XML  
 Il salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument> mediante i metodi descritti in questo argomento viene eseguito usando i metodi della classe <xref:System.Xml.XmlDocument>.  Per altre informazioni sul salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument>, vedere [Salvataggio e scrittura di un documento](../../../../docs/standard/data/xml/saving-and-writing-a-document.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Modifica dei dati XML con XPathNavigator](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md)   
 [Rimozione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)