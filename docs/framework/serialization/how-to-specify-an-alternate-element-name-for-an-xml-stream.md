---
title: "Procedura: specificare un nome di elemento alternativo per un flusso XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "classi, override"
  - "override di classi"
  - "override della serializzazione XML"
  - "serializzazione, override"
  - "serializzazione XML, override"
  - "Flusso XML, impostazione di un nome di elemento alternativo per"
ms.assetid: 5cc1c0b0-f94b-4525-9a41-88a582cd6668
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: specificare un nome di elemento alternativo per un flusso XML
[Esempio di codice](#cpconoverridingserializationofclasseswithxmlattributeoverridesclassanchor1)  
  
 Tramite l'utilizzo di [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx), è possibile generare più di un flusso XML con lo stesso set di classi.È consigliabile eseguire questa operazione poiché due diversi servizi Web XML richiedono le stesse informazioni di base, con solo piccole differenze.Si immagini ad esempio due servizi Web XML che elaborano ordini per libri e che pertanto richiedono i numeri ISBN.Un servizio utilizza il tag \<ISBN\> mentre il secondo utilizza il tag \<BookID\>.Si dispone di una classe denominata `Book` che contiene un campo denominato `ISBN`.Quando viene serializzata un'istanza della classe `Book`, per impostazione predefinita verrà utilizzato il nome del membro \(ISBN\) come nome dell'elemento del tag.Per il primo servizio Web XML, tale comportamento è quello previsto.Per inviare invece il flusso XML al secondo servizio Web XML, è necessario eseguire l'override della serializzazione in modo che il nome dell'elemento del tag sia `BookID`.  
  
### Per creare un flusso XML con un nome dell'elemento alternativo  
  
1.  Creare un'istanza della classe [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic).  
  
2.  Impostare <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> di <xref:System.Xml.Serialization.XmlElementAttribute> su "BookID".  
  
3.  Creare un'istanza della classe [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic).  
  
4.  Aggiungere l'oggetto **XmlElementAttribute** alla raccolta a cui si accede tramite la proprietà <xref:System.Xml.Serialization.XmlAttributes.XmlElements%2A> di <xref:System.Xml.Serialization.XmlAttributes>.  
  
5.  Creare un'istanza della classe [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic).  
  
6.  Aggiungere **XmlAttributes** a <xref:System.Xml.Serialization.XmlAttributeOverrides> e passare il tipo dell'oggetto da sottoporre a override e il nome del membro da sottoporre a override.  
  
7.  Creare un'istanza della classe **XmlSerializer** con **XmlAttributeOverrides**.  
  
8.  Creare un'istanza della classe `Book` e serializzarla o deserializzarla.  
  
## Esempio  
  
```vb  
Public Class SerializeOverride()  
    ' Creates an XmlElementAttribute with the alternate name.  
    Dim myElementAttribute As XmlElementAttribute = _  
    New XmlElementAttribute()  
    myElementAttribute.ElementName = "BookID"  
    Dim myAttributes As XmlAttributes = New XmlAttributes()  
    myAttributes.XmlElements.Add(myElementAttribute)  
    Dim myOverrides As XmlAttributeOverrides = New XmlAttributeOverrides()  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes)  
    Dim mySerializer As XmlSerializer = _  
    New XmlSerializer(GetType(Book), myOverrides)  
    Dim b As Book = New Book()  
    b.ISBN = "123456789"  
    ' Creates a StreamWriter to write the XML stream to.  
    Dim writer As StreamWriter = New StreamWriter("Book.xml")  
    mySerializer.Serialize(writer, b);  
End Class  
  
```  
  
```csharp  
public class SerializeOverride()  
{  
    // Creates an XmlElementAttribute with the alternate name.  
    XmlElementAttribute myElementAttribute = new XmlElementAttribute();  
    myElementAttribute.ElementName = "BookID";  
    XmlAttributes myAttributes = new XmlAttributes();  
    myAttributes.XmlElements.Add(myElementAttribute);  
    XmlAttributeOverrides myOverrides = new XmlAttributeOverrides();  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes);  
    XmlSerializer mySerializer =   
    new XmlSerializer(typeof(Book), myOverrides)  
    Book b = new Book();  
    b.ISBN = "123456789"  
    // Creates a StreamWriter to write the XML stream to.  
    StreamWriter writer = new StreamWriter("Book.xml");  
    mySerializer.Serialize(writer, b);  
}  
```  
  
 Il flusso XML potrebbe assomigliare agli elementi seguenti.  
  
```  
<Book>  
    <BookID>123456789</BookID>  
</Book>  
```  
  
## Vedere anche  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic)   
 [XmlAttributes](frlrfSystemXmlSerializationXmlAttributesClassTopic)   
 [XmlAttributeOverrides](frlrfSystemXmlSerializationXmlAttributeOverridesClassTopic)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)