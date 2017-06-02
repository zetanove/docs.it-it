---
title: "Convalida dello schema con XPathNavigator | Microsoft Docs"
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
ms.assetid: 81fa0e41-d9c9-46f0-b22b-50da839c77f5
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# Convalida dello schema con XPathNavigator
La classe <xref:System.Xml.XmlDocument> consente di convalidare il contenuto XML di un oggetto <xref:System.Xml.XmlDocument> in due modi diversi.  Il primo modo prevede la convalida del contenuto XML mediante un oggetto di convalida <xref:System.Xml.XmlReader>, mentre il secondo modo prevede l'uso del metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  È inoltre possibile eseguire la convalida di sola lettura del contenuto XML usando la classe <xref:System.Xml.XPath.XPathDocument>.  
  
## Convalida di dati XML  
 Per impostazione predefinita, la classe <xref:System.Xml.XmlDocument> non consente di convalidare un documento XML mediante la DTD \(Document Type Definition\) o lo schema XSD \(XML Schema Definition Language\).  Tale classe consente soltanto di verificare che il documento XML sia in formato corretto.  
  
 Nel primo modo, il documento XML viene convalidato durante il caricamento in un oggetto <xref:System.Xml.XmlDocument> usando un oggetto di convalida <xref:System.Xml.XmlReader>.  Nel secondo modo, il documento XML non tipizzato in precedenza viene convalidato usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  In entrambi i casi, le modifiche apportate al documento XML convalidato possono essere convalidate di nuovo usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  
  
### Convalida di un documento durante il caricamento  
 Un oggetto di convalida <xref:System.Xml.XmlReader> viene creato passando un oggetto <xref:System.Xml.XmlReaderSettings> al metodo <xref:System.Xml.XmlReader.Create%2A> della classe <xref:System.Xml.XmlReader> che accetta un oggetto <xref:System.Xml.XmlReaderSettings> come parametro.  Nell'oggetto <xref:System.Xml.XmlReaderSettings> passato come parametro è presente una proprietà <xref:System.Xml.XmlReaderSettings.ValidationType%2A> impostata su `Schema` e un XML Schema per il documento XML contenuto nell'oggetto <xref:System.Xml.XmlDocument> aggiunto alla relativa proprietà <xref:System.Xml.XmlReaderSettings.Schemas%2A>.  L'oggetto di convalida <xref:System.Xml.XmlReader> viene quindi usato per creare l'oggetto <xref:System.Xml.XmlDocument>.  
  
 Nel seguente esempio viene convalidato il file `contosoBooks.xml` durante il caricamento nell'oggetto <xref:System.Xml.XmlDocument>, creato mediante un oggetto di convalida <xref:System.Xml.XmlReader>.  Dal momento che il documento XML è valido in base al relativo schema, non verrà generato alcun errore o avviso di convalida dello schema.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidatingReaderExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Try  
            Dim settings As XmlReaderSettings = New XmlReaderSettings()  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
            settings.ValidationType = ValidationType.Schema  
  
            Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
            Dim document As XmlDocument = New XmlDocument()  
            document.Load(reader)  
            Dim navigator As XPathNavigator = document.CreateNavigator()  
  
        Catch e As Exception  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message)  
        End Try  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidatingReaderExample  
{  
    static void Main(string[] args)  
    {  
        try  
        {  
            XmlReaderSettings settings = new XmlReaderSettings();  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
            settings.ValidationType = ValidationType.Schema;  
  
            XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
            XmlDocument document = new XmlDocument();  
            document.Load(reader);  
            XPathNavigator navigator = document.CreateNavigator();  
        }  
        catch (Exception e)  
        {  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message);  
        }  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Anche il file `contosoBooks.xsd` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 Nell'esempio precedente verrà generata un'eccezione <xref:System.Xml.Schema.XmlSchemaValidationException> quando si chiama <xref:System.Xml.XmlDocument.Load%2A> se il tipo di qualsiasi attributo o elemento non corrisponde al tipo specificato nello schema di convalida.  Se <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> è impostato sull'oggetto <xref:System.Xml.XmlReader> di convalida, verrà chiamato <xref:System.Xml.XmlReaderSettings.ValidationEventHandler> ogni volta in cui viene individuato un tipo non valido.  
  
 Verrà generata un'eccezione <xref:System.Xml.Schema.XmlSchemaException> quando <xref:System.Xml.XPath.XPathNavigator> accede a un attributo o un elemento la cui proprietà <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> è impostata su `invalid`.  
  
 È possibile usare la proprietà <xref:System.Xml.Schema.XmlSchemaInfo.Validity%2A> per determinare se un singolo attributo o elemento è valido quando si accede ad attributi o elementi tramite <xref:System.Xml.XPath.XPathNavigator>.  
  
> [!NOTE]
>  Quando un documento XML viene caricato in un oggetto <xref:System.Xml.XmlDocument> a cui è associato uno schema che definisce dei valori predefiniti, questi vengono considerati dall'oggetto <xref:System.Xml.XmlDocument> come se fossero contenuti nel documento XML.  Ciò significa che la proprietà <xref:System.Xml.XPath.XPathNavigator.IsEmptyElement%2A> restituisce sempre `false` per un elemento che è stato modificato dallo schema, anche se nel documento XML era stato scritto come elemento vuoto.  
  
### Convalida di un documento con il metodo Validate  
 Il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument> consente di convalidare il documento XML contenuto in un oggetto <xref:System.Xml.XmlDocument> in base agli schemi specificati nella proprietà <xref:System.Xml.XmlDocument.Schemas%2A> dell'oggetto <xref:System.Xml.XmlDocument> e di aumentare l'infoset.  Il risultato è la sostituzione di un documento XML non tipizzato in precedenza nell'oggetto <xref:System.Xml.XmlDocument> con un documento tipizzato.  
  
 Per segnalare gli errori e gli avvisi di convalida dello schema, nell'oggetto <xref:System.Xml.XmlDocument> viene usato il delegato <xref:System.Xml.Schema.ValidationEventHandler> passato come parametro al metodo <xref:System.Xml.XmlDocument.Validate%2A>.  
  
 Nell'esempio seguente viene convalidato il file `contosoBooks.xml` contenuto nell'oggetto <xref:System.Xml.XmlDocument> in base allo schema `contosoBooks.xsd` contenuto nella proprietà <xref:System.Xml.XmlDocument.Schemas%2A> dell'oggetto <xref:System.Xml.XmlDocument>.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidateExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Dim document As XmlDocument = New XmlDocument()  
        document.Load("contosoBooks.xml")  
        Dim navigator As XPathNavigator = document.CreateNavigator()  
  
        document.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
        Dim validation As ValidationEventHandler = New ValidationEventHandler(AddressOf SchemaValidationHandler)  
  
        document.Validate(validation)  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidateExample  
{  
    static void Main(string[] args)  
    {  
        XmlDocument document = new XmlDocument();  
        document.Load("contosoBooks.xml");  
        XPathNavigator navigator = document.CreateNavigator();  
  
        document.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
        ValidationEventHandler validation = new ValidationEventHandler(SchemaValidationHandler);  
  
        document.Validate(validation);  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Anche il file `contosoBooks.xsd` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
### Convalida delle modifiche  
 Dopo aver apportato delle modifiche a un documento XML, è possibile convalidare le modifiche in base allo schema per il documento XML usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  
  
 Nel seguente esempio viene convalidato il file `contosoBooks.xml` durante il caricamento nell'oggetto <xref:System.Xml.XmlDocument>, creato mediante un oggetto di convalida <xref:System.Xml.XmlReader>.  Il documento XML viene convalidato correttamente durante il caricamento e non viene generato alcun errore o avviso di convalida dello schema.  Nell'esempio vengono quindi apportate due modifiche al documento XML che risultano non valide in base allo schema `contosoBooks.xsd`.  Nella prima modifica viene inserito un elemento figlio non valido che genera un errore di convalida dello schema. Nella seconda modifica, invece, il valore di un nodo tipizzato viene impostato su un valore non valido in base al tipo del nodo e viene generata un'eccezione.  
  
```vb  
Imports System  
Imports System.Xml  
Imports System.Xml.Schema  
Imports System.Xml.XPath  
  
Class ValidatingReaderExample  
  
    Shared Sub Main(ByVal args() As String)  
  
        Try  
            Dim settings As XmlReaderSettings = New XmlReaderSettings()  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
            settings.ValidationType = ValidationType.Schema  
  
            Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
            Dim document As XmlDocument = New XmlDocument()  
            document.Load(reader)  
            Dim navigator As XPathNavigator = document.CreateNavigator()  
  
            Dim validation As ValidationEventHandler = New ValidationEventHandler(AddressOf SchemaValidationHandler)  
  
            navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
            navigator.MoveToChild("book", "http://www.contoso.com/books")  
            navigator.MoveToChild("author", "http://www.contoso.com/books")  
  
            navigator.AppendChild("<title>Book Title</title>")  
  
            document.Validate(validation)  
  
            navigator.MoveToParent()  
            navigator.MoveToChild("price", "http://www.contoso.com/books")  
            navigator.SetTypedValue(DateTime.Now)  
        Catch e As Exception  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message)  
        End Try  
  
    End Sub  
  
    Shared Sub SchemaValidationHandler(ByVal sender As Object, ByVal e As ValidationEventArgs)  
  
        Select Case e.Severity  
            Case XmlSeverityType.Error  
                Console.WriteLine("Schema Validation Error: {0}", e.Message)  
                Exit Sub  
            Case XmlSeverityType.Warning  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message)  
                Exit Sub  
        End Select  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.Xml.XPath;  
  
class ValidatingReaderExample  
{  
    static void Main(string[] args)  
    {  
        try  
        {  
            XmlReaderSettings settings = new XmlReaderSettings();  
            settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
            settings.ValidationType = ValidationType.Schema;  
  
            XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
            XmlDocument document = new XmlDocument();  
            document.Load(reader);  
            XPathNavigator navigator = document.CreateNavigator();  
  
            ValidationEventHandler validation = new ValidationEventHandler(SchemaValidationHandler);  
  
            navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
            navigator.MoveToChild("book", "http://www.contoso.com/books");  
            navigator.MoveToChild("author", "http://www.contoso.com/books");  
  
            navigator.AppendChild("<title>Book Title</title>");  
  
            document.Validate(validation);  
  
            navigator.MoveToParent();  
            navigator.MoveToChild("price", "http://www.contoso.com/books");  
            navigator.SetTypedValue(DateTime.Now);  
        }  
        catch (Exception e)  
        {  
            Console.WriteLine("ValidatingReaderExample.Exception: {0}", e.Message);  
        }  
    }  
  
    static void SchemaValidationHandler(object sender, ValidationEventArgs e)  
    {  
        switch (e.Severity)  
        {  
            case XmlSeverityType.Error:  
                Console.WriteLine("Schema Validation Error: {0}", e.Message);  
                break;  
            case XmlSeverityType.Warning:  
                Console.WriteLine("Schema Validation Warning: {0}", e.Message);  
                break;  
        }  
    }  
}  
```  
  
 Nell'esempio il file `contosoBooks.xml` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 Anche il file `contosoBooks.xsd` viene considerato come input.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 Nell'esempio precedente, vengono apportate due modifiche al documento XML contenuto nell'oggetto <xref:System.Xml.XmlDocument>.  Durante il caricamento del documento XML, se fossero stati rilevati errori di convalida dello schema, sarebbero stati gestiti dal gestore eventi di convalida e darebbero stati scritti nella console.  
  
 In questo esempio, gli errori di convalida sono stati introdotti dopo il caricamento del documento XML e sono stati rilevati usando il metodo <xref:System.Xml.XmlDocument.Validate%2A> della classe <xref:System.Xml.XmlDocument>.  
  
 Le modifiche effettuate usando il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> della classe <xref:System.Xml.XPath.XPathNavigator> hanno restituito un tipo <xref:System.InvalidCastException> poiché il nuovo valore non era valido in base al tipo di schema del nodo.  
  
 Per altre informazioni sulla modifica dei valori con il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A>, vedere l'argomento [Modifica dei dati XML con XPathNavigator](../../../../docs/standard/data/xml/modify-xml-data-using-xpathnavigator.md).  
  
### Convalida di sola lettura  
 La classe <xref:System.Xml.XPath.XPathDocument> è una rappresentazione in memoria e di sola lettura di un documento XML.  Le classi <xref:System.Xml.XPath.XPathDocument> e <xref:System.Xml.XmlDocument> consentono di creare oggetti <xref:System.Xml.XPath.XPathNavigator> per esplorare e modificare i documenti XML.  Dal momento che la classe <xref:System.Xml.XPath.XPathDocument> è di sola lettura, gli oggetti <xref:System.Xml.XPath.XPathNavigator> restituiti dagli oggetti <xref:System.Xml.XPath.XPathDocument> non sono in grado di modificare il documento XML contenuto nell'oggetto <xref:System.Xml.XPath.XPathDocument>.  
  
 In caso di convalida, è possibile creare un oggetto <xref:System.Xml.XPath.XPathDocument> nello stesso modo in cui si crea un oggetto <xref:System.Xml.XmlDocument> usando un oggetto di convalida <xref:System.Xml.XmlReader> come descritto in precedenza in questo argomento.  L'oggetto <xref:System.Xml.XPath.XPathDocument> consente di convalidare il documento XML durante il caricamento; tuttavia, dal momento che non è possibile modificare i dati XML nell'oggetto <xref:System.Xml.XPath.XPathDocument>, non sarà possibile eseguire di nuovo la convalida del documento XML.  
  
 Per altre informazioni sugli oggetti <xref:System.Xml.XPath.XPathNavigator> modificabili e di sola lettura, vedere l'argomento [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md).  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Lettura di dati XML con XPathDocument e XmlDocument](../../../../docs/standard/data/xml/reading-xml-data-using-xpathdocument-and-xmldocument.md)   
 [Selezione, valutazione e corrispondenza di dati XML con XPathNavigator](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)   
 [Accesso ai dati XML con XPathNavigator](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)   
 [Modifica di dati XML con XPathNavigator](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)