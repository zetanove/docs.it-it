---
title: "Lettura di dati XML con XPathDocument e XmlDocument | Microsoft Docs"
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
ms.assetid: 5711b225-6aa2-4e4f-9898-19f2d518ad1a
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Lettura di dati XML con XPathDocument e XmlDocument
Sono disponibili due metodi per leggere un documento XML nello spazio dei nomi <xref:System.Xml.XPath?displayProperty=fullName>.  Un metodo consiste nel leggere un documento XML usando la classe di sola lettura <xref:System.Xml.XPath.XPathDocument>, l'altro consiste nel leggere un documento XML usando la classe modificabile <xref:System.Xml.XmlDocument> nello spazio dei nomi <xref:System.Xml?displayProperty=fullName>.  
  
## Lettura di documenti XML con la classe XPathDocument  
 La classe <xref:System.Xml.XPath.XPathDocument> fornisce una rappresentazione in memoria rapida e di sola lettura di un documento XML usando il modello di dati XPath.  Le istanze della classe <xref:System.Xml.XPath.XPathDocument> vengono create usando uno dei sei costruttori disponibili.  Tali costruttori consentono di leggere un documento XML usando un oggetto <xref:System.IO.Stream>, <xref:System.IO.TextReader> o <xref:System.Xml.XmlReader> nonché il percorso `string` di un file XML.  
  
 Nell'esempio seguente viene illustrato l'uso del costruttore `string` della classe <xref:System.Xml.XPath.XPathDocument> per leggere un documento XML.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
```  
  
## Lettura di documenti XML con la classe XmlDocument Class  
 La classe <xref:System.Xml.XmlDocument> è una rappresentazione in memoria modificabile di un documento XML implementando i componenti di base delle specifiche Document Object Model \(DOM\) Level 1 e Level 2 di W3C.  Le istanze della classe <xref:System.Xml.XmlDocument> vengono create usando uno dei tre costruttori disponibili.  È possibile creare un nuovo oggetto vuoto <xref:System.Xml.XmlDocument> chiamando il costruttore della classe <xref:System.Xml.XmlDocument> senza parametri.  Dopo che il costruttore è stato chiamato, usare il metodo <xref:System.Xml.XmlDocument.Load%2A> per caricare i dati XML nel nuovo oggetto <xref:System.Xml.XmlDocument> da un oggetto <xref:System.IO.Stream>, <xref:System.IO.TextReader> o <xref:System.Xml.XmlReader>, oppure usare il percorso `string` di un file XML.  
  
 Nell'esempio seguente viene illustrato l'uso del costruttore della classe <xref:System.Xml.XmlDocument> senza parametri e del metodo <xref:System.Xml.XmlDocument.Load%2A> per leggere un documento XML.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
```  
  
## Determinazione della codifica di un documento XML  
 È possibile usare un oggetto <xref:System.Xml.XmlReader> per leggere un documento XML e per creare oggetti <xref:System.Xml.XPath.XPathDocument> e <xref:System.Xml.XmlDocument>, come illustrato nelle sezioni precedenti.  Tuttavia, un oggetto <xref:System.Xml.XmlReader> può leggere i dati non codificati e, di conseguenza, non fornisce alcuna informazione relativa alla codifica.  
  
 La classe <xref:System.Xml.XmlTextReader> eredita dalla classe <xref:System.Xml.XmlReader>, fornisce informazioni sulla codifica usando la relativa proprietà <xref:System.Xml.XmlTextReader.Encoding%2A> e può essere usata per creare un oggetto <xref:System.Xml.XPath.XPathDocument> o un oggetto <xref:System.Xml.XmlDocument>.  
  
 Per altre informazioni sulle informazioni di codifica fornite dalla classe <xref:System.Xml.XmlTextReader>, vedere la proprietà <xref:System.Xml.XmlTextReader.Encoding%2A> nella documentazione di riferimento per la classe <xref:System.Xml.XmlTextReader>.  
  
## Creazione di oggetti XPathNavigator  
 Dopo che è stato letto un documento XML in un oggetto <xref:System.Xml.XPath.XPathDocument> o in un oggetto <xref:System.Xml.XmlDocument>, è possibile creare un oggetto <xref:System.Xml.XPath.XPathNavigator> per selezionare, valutare, esplorare e, in alcuni casi, modificare i dati XML sottostanti.  
  
 Sia la classe <xref:System.Xml.XPath.XPathDocument> che la classe <xref:System.Xml.XmlDocument>, oltre alla classe <xref:System.Xml.XmlNode>, implementano l'interfaccia <xref:System.Xml.XPath.IXPathNavigable> dello spazio dei nomi <xref:System.Xml.XPath?displayProperty=fullName>.  Di conseguenza, tutte le tre classi forniscono un metodo <xref:System.Xml.XPath.IXPathNavigable.CreateNavigator%2A> che restituisce un oggetto <xref:System.Xml.XPath.XPathNavigator>.  
  
### Modifica di documenti XML con la classe XPathNavigator  
 Oltre a selezionare, valutare ed esplorare i dati XML, in alcuni casi la classe <xref:System.Xml.XPath.XPathNavigator> può essere usata per modificare un documento XML, in base all'oggetto che l'ha creato.  
  
 La classe <xref:System.Xml.XPath.XPathDocument> è di sola lettura mentre la classe <xref:System.Xml.XmlDocument> è modificabile. Di conseguenza non è possibile usare gli oggetti <xref:System.Xml.XPath.XPathNavigator> creati da un oggetto <xref:System.Xml.XPath.XPathDocument> per modificare un documento XML, mentre è possibile usare quelli creati da un oggetto <xref:System.Xml.XmlDocument>.  La classe <xref:System.Xml.XPath.XPathDocument> deve essere usata solo per leggere un documento XML.  Se è necessario modificare un documento XML o se è richiesto l'accesso a funzionalità aggiuntive fornite dalla classe <xref:System.Xml.XmlDocument>, come la gestione degli eventi, è necessario usare la classe <xref:System.Xml.XmlDocument>.  
  
 La proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> della classe <xref:System.Xml.XPath.XPathNavigator> consente di specificare se un oggetto <xref:System.Xml.XPath.XPathNavigator> può modificare i dati XML.  
  
 Nella tabella seguente viene descritto il valore della proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> per ogni classe.  
  
|Implementazione di <xref:System.Xml.XPath.IXPathNavigable>|Valore di <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A>|  
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Xml.XPath.XPathDocument>|`false`|  
|<xref:System.Xml.XmlDocument>|`true`|  
  
## Vedere anche  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [Elaborazione di dati XML con il modello di dati XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [Accesso ai dati XML con XPathNavigator](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)   
 [Modifica di dati XML con XPathNavigator](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)   
 [Convalida dello schema con XPathNavigator](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)