---
title: "Modifica dei dati XML con XPathNavigator | Microsoft Docs"
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
ms.assetid: 03a7c5a1-b296-4af4-b209-043c958dc0a5
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Modifica dei dati XML con XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usati per modificare nodi e valori in un documento XML.  Per usare questi metodi, è necessario che l'oggetto <xref:System.Xml.XPath.XPathNavigator> sia modificabile, ovvero, la relativa proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> deve essere `true`.  
  
 Gli oggetti <xref:System.Xml.XPath.XPathNavigator> che possono modificare un documento XML vengono creati dal metodo <xref:System.Xml.XmlDocument.CreateNavigator%2A> della classe <xref:System.Xml.XmlDocument>.  Gli oggetti <xref:System.Xml.XPath.XPathNavigator> creati dalla classe <xref:System.Xml.XPath.XPathDocument> sono di sola lettura e qualsiasi tentativo di usare i metodi di modifica di un oggetto <xref:System.Xml.XPath.XPathNavigator> creato da un oggetto <xref:System.Xml.XPath.XPathDocument> genererà un oggetto <xref:System.NotSupportedException>.  
  
 Per altre informazioni sulla creazione di oggetti modificabili <xref:System.Xml.XPath.XPathNavigator>, vedere [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md).  
  
## Modifica dei nodi  
 Una tecnica semplice per modificare il valore di un nodo è quella di usare i metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
 Nella tabella seguente sono elencati gli effetti di tali metodi sui diversi tipi di nodo.  
  
|<xref:System.Xml.XPath.XPathNodeType>|Dati modificati|  
|---------------------------------------------------------------------------------------------------------------------------------------------|---------------------|  
|<xref:System.Xml.XPath.XPathNodeType>|Non supportato.|  
|<xref:System.Xml.XPath.XPathNodeType>|Contenuto dell'elemento.|  
|<xref:System.Xml.XPath.XPathNodeType>|Valore dell'attributo.|  
|<xref:System.Xml.XPath.XPathNodeType>|Contenuto di testo.|  
|<xref:System.Xml.XPath.XPathNodeType>|Contenuto eccetto la destinazione.|  
|<xref:System.Xml.XPath.XPathNodeType>|Contenuto del commento.|  
|<xref:System.Xml.XPath.XPathNodeType>|Non supportato.|  
  
> [!NOTE]
>  La modifica dei nodi <xref:System.Xml.XPath.XPathNodeType> o del nodo <xref:System.Xml.XPath.XPathNodeType> non è supportata.  
  
 La classe <xref:System.Xml.XPath.XPathNavigator> fornisce inoltre un set di metodi usati per inserire e rimuovere nodi.  Per altre informazioni sull'inserimento e la rimozione di nodi da un documento XML, vedere gli argomenti [Inserimento dei dati XML utilizzando XPathNavigator](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md) e [Rimozione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md).  
  
### Modifica dei valori non tipizzati  
 Il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> consente semplicemente di inserire il valore non tipizzato `string`, passato come parametro, come valore del nodo su cui è attualmente posizionato l'oggetto <xref:System.Xml.XPath.XPathNavigator>.  Il valore viene inserito senza alcun tipo o senza verificare la validità del nuovo valore in base al tipo del nodo se sono disponibili le informazioni sullo schema.  
  
 Nell'esempio seguente, il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> viene usato per aggiornare tutti gli elementi `price` nel file `contosoBooks.xml`.  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### Modifica dei valori tipizzati  
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
  
#### Effetti delle modifiche ai dati XML tipizzati in modo sicuro  
 La classe <xref:System.Xml.XPath.XPathNavigator> usa W3C XML Schema come base per la descrizione del codice XML tipizzato in modo sicuro.  Gli elementi e gli attributi possono essere annotati con informazioni sul tipo basate sulla convalida rispetto a un documento W3C XML Schema.  Gli elementi che possono contenere altri elementi o attributi sono denominati tipi complessi, mentre gli elementi che possono contenere solo contenuto testuale sono denominati tipi semplici.  
  
> [!NOTE]
>  Gli attributi possono disporre solo di tipi semplici.  
  
 Un elemento o attributo può essere considerato valido per lo schema se è conforme a tutte le regole specifiche della relativa definizione del tipo.  Affinché sia valido per lo schema, un elemento di tipo semplice `xs:int` deve contenere un valore numerico compreso tra \-2147483648 e 2147483647.  Per i tipi complessi, la validità di schema dell'elemento dipende dalla validità di schema dei relativi elementi e attributi figlio.  Pertanto, se un elemento è valido in base alla relativa definizione di tipo complesso, tutti gli elementi e gli attributi figlio sono validi in base alle proprie definizioni dei tipi.  In modo analogo, se anche un solo elemento o attributo figlio di un elemento non è valido in base alla definizione del tipo, o se la validità è sconosciuta, l'elemento sarà non valido o di validità sconosciuta.  
  
 Dato che la validità di un elemento dipende dalla validità degli elementi e attributi figlio, le modifiche apportate a entrambi determinano una modifica della validità dell'elemento in precedenza valido.  In particolare, se gli elementi o attributi figlio di un elemento vengono inseriti, aggiornati o eliminati, la validità dell'elemento risulterà sconosciuta.  Ciò risulterà dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> dell'elemento impostata su <xref:System.Xml.Schema.XmlSchemaValidity>.  Inoltre, questo effetto si estende in modo ricorsivo verso l'alto nel documento XML, poiché anche la validità dell'elemento padre dell'elemento \(e del suo elemento padre e così via\) risulterà sconosciuta.  
  
 Per altre informazioni sulla convalida degli schemi e sulla classe <xref:System.Xml.XPath.XPathNavigator>, vedere [Convalida dello schema con XPathNavigator](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md).  
  
### Modifica degli attributi  
 I metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> possono essere usati per modificare i nodi Attribute tipizzati e non tipizzati, nonché gli altri tipi di nodo elencati nella sezione "Modifica dei nodi".  
  
 Nell'esempio seguente viene modificato il valore dell'attributo `genre` del primo elemento `book` nel file `books.xml`.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
navigator.MoveToChild("book", String.Empty)  
navigator.MoveToAttribute("genre", String.Empty)  
  
navigator.SetValue("non-fiction")  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
navigator.MoveToChild("book", String.Empty);  
navigator.MoveToAttribute("genre", String.Empty);  
  
navigator.SetValue("non-fiction");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 Per altre informazioni sui metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A>, vedere le sezioni "Modifica dei valori non tipizzati" e "Modifica dei valori tipizzati".  
  
## Proprietà InnerXml e OuterXml  
 Le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> della classe <xref:System.Xml.XPath.XPathNavigator> consentono di modificare il markup XML dei nodi su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
 La proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> con il contenuto analizzato della `string` XML specificata.  Allo stesso modo, la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> nonché il nodo corrente stesso.  
  
 Nell'esempio seguente viene usata la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> per modificare il valore dell'elemento `price` e inserire un nuovo attributo `discount` sul primo elemento `book` nel file `contosoBooks.xml`.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml");  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>"  
  
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
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>";  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
## Modifica dei nodi dello spazio dei nomi  
 Nel DOM \(Document Object Model\) le dichiarazioni dello spazio dei nomi vengono considerate come attributi regolari che possono essere inseriti, aggiornati ed eliminati.  Nella classe <xref:System.Xml.XPath.XPathNavigator> tali operazioni sui nodi dello spazio dei nomi non sono consentite, in quanto la modifica del valore di un nodo dello spazio dei nomi può modificare a sua volta l'identità degli elementi e degli attributi nell'ambito del nodo dello spazio dei nomi, come illustrato nell'esempio seguente.  
  
```  
<root xmlns="http://www.contoso.com">  
    <child />  
</root>  
```  
  
 Se l'esempio precedente di codice XML viene modificato nel modo seguente, ciascun elemento del documento viene effettivamente rinominato in quanto il valore dell'URI dello spazio dei nomi di ogni singolo elemento è stato modificato.  
  
```  
<root xmlns="urn:contoso.com">  
    <child />  
</root>  
```  
  
 La classe <xref:System.Xml.XPath.XPathNavigator> consente l'inserimento di nodi dello spazio dei nomi che non entrino in conflitto con le dichiarazioni dello spazio dei nomi nell'ambito in cui sono stati inseriti.  In questo caso, le dichiarazioni dello spazio dei nomi non sono dichiarate in ambiti inferiori nel documento XML e non determinano alcuna rinomina, come illustrato nell'esempio seguente.  
  
```  
<root xmlns:a="http://www.contoso.com">  
    <parent>  
        <a:child />  
    </parent>  
</root>  
```  
  
 Se l'esempio precedente di codice XML viene modificato nel modo seguente, le dichiarazioni dello spazio dei nomi vengono propagate correttamente nel documento XML nell'ambito inferiore a quello della dichiarazione dello spazio dei nomi.  
  
```  
<root xmlns:a="http://www.contoso.com">  
    <parent a:parent-id="1234" xmlns:a="http://www.contoso.com/parent-id">  
        <a:child xmlns:a="http://www.contoso.com/">  
    </parent>  
</root>  
```  
  
 Nell'esempio precedente di codice XML, l'attributo `a:parent-id` viene inserito sull'elemento `parent` nello spazio dei nomi `http://www.contoso.com/parent-id`.  Il metodo <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> viene usato per inserire l'attributo quando si trova posizionato sull'elemento `parent`.  La dichiarazione dello spazio dei nomi `http://www.contoso.com` viene inserita automaticamente dalla classe <xref:System.Xml.XPath.XPathNavigator> per garantire la coerenza della parte restante del documento XML.  
  
## Modifica dei nodi dei riferimenti all'entità  
 I nodi dei riferimenti all'entità in un oggetto <xref:System.Xml.XmlDocument> sono di sola lettura e non è possibile modificarli tramite le classi <xref:System.Xml.XPath.XPathNavigator> o <xref:System.Xml.XmlNode>.  Qualsiasi tentativo di modificare un nodo dei riferimenti all'entità determinerà un'eccezione <xref:System.InvalidOperationException>.  
  
## Modifica dei nodi xsi:nil  
 La raccomandazione W3C XML Schema \(informazioni in lingua inglese\) illustra il concetto di elemento nillable.  Quando un elemento è nillable, è possibile che l'elemento non disponga di alcun contenuto pur essendo valido.  Il concetto di elemento nillable è simile a quello di oggetto con valore `null`.  La differenza principale sta tuttavia nel fatto che un oggetto `null` non è accessibile in alcun modo, mentre un elemento `xsi:nil` continua a disporre di proprietà \(gli attributi, ad esempio\) a cui è possibile accedere, pur non avendo alcun contenuto \(elementi figlio o testo\).  L'esistenza dell'attributo `xsi:nil` con valore `true` su un elemento di un documento XML viene usata per indicare che un elemento è privo di contenuto.  
  
 Se un oggetto <xref:System.Xml.XPath.XPathNavigator> viene usato per aggiungere contenuto a un elemento valido con un attributo `xsi:nil` e con un valore `true`, il valore dell'attributo `xsi:nil` viene impostato su `false`.  
  
> [!NOTE]
>  Se il contenuto di un elemento con un attributo `xsi:nil` impostato su `false` viene eliminato, il valore dell'attributo non verrà modificato in `true`.  
  
## Salvataggio di un documento XML  
 Il salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument> come risultato dei metodi di modifica descritti in questo argomento viene eseguito usando i metodi della classe <xref:System.Xml.XmlDocument>.  Per altre informazioni sul salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument>, vedere [Salvataggio e scrittura di un documento](../../../../docs/standard/data/xml/saving-and-writing-a-document.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Inserimento dei dati XML utilizzando XPathNavigator](../../../../docs/standard/data/xml/insert-xml-data-using-xpathnavigator.md)   
 [Rimozione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/remove-xml-data-using-xpathnavigator.md)