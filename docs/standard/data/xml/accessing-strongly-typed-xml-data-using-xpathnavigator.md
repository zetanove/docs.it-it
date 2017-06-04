---
title: "Accesso a dati XML fortemente tipizzati con XPathNavigator | Microsoft Docs"
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
ms.assetid: 898e0f52-8a7c-4d1f-afcd-6ffb28b050b4
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Accesso a dati XML fortemente tipizzati con XPathNavigator
Analogamente a un'istanza del modello di dati XPath versione 2.0, la classe <xref:System.Xml.XPath.XPathNavigator> può contenere dati tipizzati in modo sicuro associati a tipi CLR \(Common Language Runtime\).  In base al modello di dati XPath versione 2.0, solo gli elementi e gli attributi possono contenere dati tipizzati in modo sicuro.  La classe <xref:System.Xml.XPath.XPathNavigator> fornisce meccanismi di accesso ai dati di un oggetto <xref:System.Xml.XPath.XPathDocument> o <xref:System.Xml.XmlDocument> come dati tipizzati in modo sicuro e meccanismi di conversione da un tipo di dati a un altro.  
  
## Informazioni sul tipo esposte da XPathNavigator  
 Tecnicamente, i dati XML versione 1.0 non dispongono di tipi, a meno che non vengano elaborati tramite una DTD, uno schema XSD \(XML Schema Definition Language\) o un altro meccanismo.  Esistono diverse categorie di informazioni sul tipo che possono essere associate con un elemento o attributo XML.  
  
-   Tipi CLR semplici: nessun linguaggio XML Schema supporta i tipi CLR in modo diretto.  Dal momento che risulta utile poter visualizzare il contenuto semplice di elementi e attributi come tipo CLR più appropriato, è possibile tipizzare l'intero contenuto semplice come tipo <xref:System.String> in assenza di informazioni sullo schema e di eventuali informazioni aggiunte che possano ottimizzare tale contenuto rendendolo un tipo più appropriato.  Per individuare il tipo CLR che corrisponde maggiormente al contenuto semplice dell'elemento o attributo, usare la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueType%2A>.  Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).  
  
-   Elenchi di tipi semplici \(CLR\): un elemento o attributo con contenuto semplice può contenere un elenco di valori separati da spazi vuoti.  I valori sono specificati da un XML Schema come "dati di tipo list". In assenza di un XML Schema, questo contenuto semplice verrebbe considerato come un solo nodo di tipo text.  Se invece è disponibile un XML Schema, questo contenuto semplice può essere esposto come una serie di valori specifici, ognuno dei quali dispone di un tipo semplice associato a una raccolta di oggetti CLR.  Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).  
  
-   Valore tipizzato: un attributo o un elemento con un tipo semplice convalidato in base a uno schema presenta un valore tipizzato.  Questo valore è un tipo primitivo, ad esempio un tipo di dati numerico, di stringa o relativo alla data.  È possibile eseguire il mapping di tutti i tipi semplici incorporati in XSD a tipi CLR che consentono l'accesso al valore di un nodo come un tipo più appropriato anziché come un tipo <xref:System.String>.  Un elemento che presenta attributi o elementi figlio è considerato un tipo complesso.  Il valore tipizzato di un tipo complesso che presenta contenuto semplice, ovvero solo nodi di tipo text come nodi figlio, è uguale a quello del tipo semplice del relativo contenuto.  Il valore tipizzato di un tipo complesso che presenta contenuto complesso, ovvero più di un elemento figlio, è il valore di stringa della concatenazione di tutti i nodi figlio di tipo text restituiti come tipo <xref:System.String>.  Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).  
  
-   Nome del tipo specifico per il linguaggio di schema: nella maggior parte dei casi, i tipi CLR, impostati come effetto collaterale dell'applicazione di uno schema esterno, vengono usati per consentire l'accesso al valore di un nodo.  Tuttavia, in alcune situazioni è possibile che si desideri esaminare il tipo associato a uno schema particolare applicato a un documento XML.  Ad esempio, è possibile che si desideri eseguire una ricerca nel documento XML ed estrarre tutti gli elementi per i quali è stato determinato un contenuto di tipo "PurchaseOrder" in base a uno schema associato.  Queste informazioni sul tipo possono essere impostate solo in seguito alla convalida dello schema ed è possibile accedervi tramite le proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> e <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  Per altre informazioni, vedere di seguito la sezione relativa all'infoset sulla convalida post\-schema.  
  
-   Reflection sul tipo specifico per il linguaggio di schema: in altri casi, è possibile che si desideri ottenere ulteriori informazioni sul tipo specifico per lo schema applicato a un documento XML.  Ad esempio, durante la lettura di un file XML, è possibile che si desideri estrarre l'attributo `maxOccurs` per ciascun nodo valido nel documento XML per eseguire calcoli personalizzati.  Dal momento che queste informazioni vengono impostate solo in seguito alla convalida dello schema, è possibile accedervi tramite la proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  Per altre informazioni, vedere di seguito la sezione relativa all'infoset sulla convalida post\-schema.  
  
## Funzioni di accesso tipizzate di XPathNavigator  
 Nella tabella seguente vengono illustrate le diverse proprietà e i diversi metodi della classe <xref:System.Xml.XPath.XPathNavigator> che possono essere usati per accedere alle informazioni sul tipo di un nodo.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Xml.XPath.XPathNavigator.XmlType%2A>|Contiene le informazioni sul tipo di schema XML per il nodo se questo è valido.|  
|<xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A>|Contiene l'infoset sulla convalida post\-schema del nodo aggiunte dopo la convalida.  Sono incluse le informazioni sul tipo di schema XML e le informazioni sulla validità.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueType%2A>|Il tipo CLR del valore tipizzato del nodo.|  
|<xref:System.Xml.XPath.XPathNavigator.TypedValue%2A>|Il contenuto del nodo come uno o più valori CLR il cui tipo corrisponde maggiormente al tipo di schema XML del nodo.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsBoolean%2A>|Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Boolean>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:boolean`.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDateTime%2A>|Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.DateTime>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:datetime`.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>|Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Double>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xsd:double`.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A>|Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Int32>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:integer`.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A>|Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Int64>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:integer`.|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAs%2A>|Il contenuto del nodo di cui viene eseguito il cast nel tipo di destinazione in base alle regole di XPath 2.0 per l'esecuzione del cast.|  
  
 Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).  
  
## Infoset sulla convalida post\-schema \(PSVI, Post Schema Validation Infoset\)  
 In un processore di XML Schema, un infoset XML viene accettato come input e viene convertito in un infoset sulla convalida post\-schema.  Un PSVI rappresenta l'infoset XML di input originale con nuovi elementi informazioni e nuove proprietà aggiunti agli elementi informazioni esistenti.  Le informazioni aggiunte all'infoset XML nel PVSI possono essere suddivise in tre grandi classi che vengono esposte dal tipo <xref:System.Xml.XPath.XPathNavigator>.  
  
1.  Risultati della convalida: informazioni relative all'esito della convalida di un elemento o di un attributo.  Tali informazioni vengono esposte dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
2.  Informazioni predefinite: viene indicato se il valore dell'elemento o dell'attributo sia stato ottenuto o meno mediante i valori predefiniti specificati nello schema.  Tali informazioni vengono esposte dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.IsDefault%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
3.  Annotazioni di tipi: riferimenti a componenti dello schema che potrebbero essere definizioni di tipi o dichiarazioni di attributo o elemento.  La proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> del tipo <xref:System.Xml.XPath.XPathNavigator> contiene le informazioni sul tipo specifiche del nodo se questo è valido.  Se la validità di un nodo è sconosciuta, ad esempio nel caso in cui il nodo sia stato convalidato e modificato successivamente,  la proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> sarà impostata su `null` ma le informazioni sul tipo saranno ancora disponibili mediante diverse proprietà della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.  
  
 Nell'esempio seguente viene illustrato l'uso delle informazioni nell'infoset sulla convalida post\-schema esposto dal tipo <xref:System.Xml.XPath.XPathNavigator>.  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("books.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("published", "http://www.contoso.com/books")  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name)  
Console.WriteLine(navigator.SchemaInfo.Validity)  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("books.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("published", "http://www.contoso.com/books");  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name);  
Console.WriteLine(navigator.SchemaInfo.Validity);  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs);  
```  
  
 Nell'esempio il file `books.xml` viene considerato come input.  
  
```  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 Anche lo schema `books.xsd` viene considerato come input.  
  
```  
<xs:schema xmlns="http://www.contoso.com/books"   
attributeFormDefault="unqualified" elementFormDefault="qualified"   
targetNamespace="http://www.contoso.com/books"   
xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:simpleType name="publishedType">  
        <xs:restriction base="xs:date">  
            <xs:minInclusive value="2003-01-01" />  
            <xs:maxInclusive value="2003-12-31" />  
        </xs:restriction>  
    </xs:simpleType>  
    <xs:complexType name="bookType">  
        <xs:sequence>  
            <xs:element name="title" type="xs:string"/>  
            <xs:element name="price" type="xs:decimal"/>  
            <xs:element name="published" type="publishedType"/>  
        </xs:sequence>  
    </xs:complexType>  
    <xs:complexType name="booksType">  
        <xs:sequence>  
            <xs:element name="book" type="bookType" />  
        </xs:sequence>  
    </xs:complexType>  
    <xs:element name="books" type="booksType" />  
</xs:schema>  
```  
  
## Recupero di valori tipizzati mediante le proprietà ValueAs  
 Il valore tipizzato di un nodo può essere recuperato accedendo alla proprietà <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> del tipo <xref:System.Xml.XPath.XPathNavigator>.  In alcuni casi, è possibile che si desideri convertire il valore tipizzato di un nodo in un tipo diverso.  Un esempio comune è rappresentato dal recupero di un valore numerico da un nodo XML.  Si consideri, ad esempio, il seguente documento XML non convalidato né tipizzato:  
  
```  
<books>  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 Se il tipo <xref:System.Xml.XPath.XPathNavigator> è posizionato sull'elemento `price`, la proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> sarà `null`, la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> sarà <xref:System.String> e la proprietà <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> sarà la stringa `10.00`.  
  
 Tuttavia, è possibile estrarre il valore come valore numerico usando il metodo <xref:System.Xml.XPath.XPathItem.ValueAs%2A> oppure la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A> o <xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A>.  Nell'esempio seguente viene illustrata l'esecuzione di questo cast usando il metodo <xref:System.Xml.XPath.XPathItem.ValueAs%2A>.  
  
```vb  
Dim document As New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "")  
navigator.MoveToChild("book", "")  
navigator.MoveToChild("price", "")  
  
Dim price = navigator.ValueAs(GetType(Decimal))  
Dim discount As Decimal = 0.2  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * discount))  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "");  
navigator.MoveToChild("book", "");  
navigator.MoveToChild("price", "");  
  
Decimal price = (decimal)navigator.ValueAs(typeof(decimal));  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * (decimal)0.20));  
```  
  
 Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Navigazione del set di nodi con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)   
 [Navigazione dei nodi di attributi e dello spazio dei nomi con XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)   
 [Estrazione di dati XML con XPathNavigator](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)