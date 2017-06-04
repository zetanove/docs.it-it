---
title: "Procedura: serializzare un oggetto come flusso XML con codifica SOAP | Microsoft Docs"
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
  - "serializzazione, SOAP"
  - "SOAP, serializzazione XML"
  - "serializzazione XML, SOAP"
ms.assetid: af406e0a-fa3a-46dd-a7ba-c80731eba3a0
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: serializzare un oggetto come flusso XML con codifica SOAP
[Esempio di codice](#cpconxmlserializationusingsoapprotocolanchor1)  
  
 Poiché un messaggio SOAP viene compilato utilizzando XML, è possibile utilizzare [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx) per serializzare classi e generare messaggi SOAP codificati.L'elemento XML ottenuto risulta conforme alla sezione 5 del documento "Simple Object Access Protocol \(SOAP\) 1.1" del World Wide Web Consortium \(www.w3.org\).Quando si crea un servizio Web XML che comunica tramite messaggi SOAP, è possibile personalizzare il flusso XML applicando un set di attributi SOAP speciali a classi e membri di classi.Per un elenco degli attributi, vedere [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/framework/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
### Per serializzare un oggetto come flusso XML con codifica SOAP  
  
1.  Creare la classe utilizzando [Strumento XML Schema Definition \(Xsd.exe\)](../../../docs/framework/serialization/xml-schema-definition-tool-xsd-exe.md).  
  
2.  Applicare uno o più degli attributi speciali disponibili in **System.Xml.Serialization**.Consultare l'elenco "Attributi per il controllo della serializzazione SOAP codificata".  
  
3.  Creare un **XmlTypeMapping** creando un nuovo **SoapReflectionImporter** e richiamando il metodo **ImportTypeMapping** con il tipo della classe serializzata.  
  
     Nell'esempio di codice riportato di seguito viene chiamato il metodo **ImportTypeMapping** della classe **SoapReflectionImporter** per creare un **XmlTypeMapping**.  
  
    ```vb  
    ' Serializes a class named Group as a SOAP message.  
    Dim myTypeMapping As XmlTypeMapping = (New SoapReflectionImporter(). _  
    ImportTypeMapping(GetType(Group))  
  
    ```  
  
    ```csharp  
    // Serializes a class named Group as a SOAP message.  
    XmlTypeMapping myTypeMapping = (new SoapReflectionImporter().  
    ImportTypeMapping(typeof(Group));  
    ```  
  
4.  Creare un'istanza della classe **XmlSerializer** passando **XmlTypeMapping** al costruttore <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29>.  
  
    ```vb  
    Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
  
    ```  
  
    ```csharp  
    XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
    ```  
  
5.  Chiamare il metodo **Serialize** o **Deserialize**.  
  
## Esempio  
  
```vb  
' Serializes a class named Group as a SOAP message.  
Dim myTypeMapping As XmlTypeMapping = (New SoapReflectionImporter(). _  
ImportTypeMapping(GetType(Group))  
Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
  
```  
  
```csharp  
// Serializes a class named Group as a SOAP message.  
XmlTypeMapping myTypeMapping = (new SoapReflectionImporter().ImportTypeMapping(typeof(Group));  
XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
```  
  
## Vedere anche  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/framework/serialization/attributes-that-control-encoded-soap-serialization.md)   
 [Serializzazione XML con Servizi Web XML](../../../docs/framework/serialization/xml-serialization-with-xml-web-services.md)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)   
 [Procedura: eseguire l'override della serializzazione XML con codifica SOAP](../../../docs/framework/serialization/how-to-override-encoded-soap-xml-serialization.md)