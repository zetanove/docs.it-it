---
title: "Attributi per il controllo della serializzazione SOAP codificata | Microsoft Docs"
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
  - "attributi [.NET Framework], serializzazione XML"
  - "serializzazione, attributi"
  - "SOAP, serializzazione XML"
  - "serializzazione XML, attributi"
  - "serializzazione XML, SOAP"
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Attributi per il controllo della serializzazione SOAP codificata
Il documento "Simple Object Access Protocol \(SOAP\) 1.1" del World Wide Web Consortium \(www.w3.org\) contiene una sezione aggiuntiva \(la sezione 5\) che descrive le modalità di codifica dei parametri SOAP.Per ottenere la conformità alla sezione 5 delle specifiche, è necessario utilizzare un set speciale di attributi reperibile nello spazio dei nomi [System.Xml.Serialization](frlrfSystemXmlSerialization).Applicare tali attributi nel modo appropriato alle classi e ai membri delle classi, quindi utilizzare [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx) per serializzare le istanze della classe o delle classi.  
  
 Nella seguente tabella sono illustrati gli attributi, dove è possibile applicarli e la loro funzione.Per ulteriori informazioni sull'utilizzo di tali attributi per il controllo della serializzazione XML, vedere [Procedura: serializzare un oggetto come flusso XML con codifica SOAP](../../../docs/framework/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) e [Procedura: eseguire l'override della serializzazione XML con codifica SOAP](../../../docs/framework/serialization/how-to-override-encoded-soap-xml-serialization.md).  
  
 Per ulteriori informazioni sugli attributi, vedere [Attributi](../../../docs/standard/attributes/index.md).  
  
|Attributo|Si applica a|Specifica|  
|---------------|------------------|---------------|  
|[SoapAttributeAttribute](frlrfSystemXmlSerializationSoapAttributeAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito.|Il membro della classe sarà serializzato come attributo XML.|  
|[SoapElementAttribute](frlrfSystemXmlSerializationSoapElementAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito.|La classe verrà serializzata come elemento XML.|  
|[SoapEnumAttribute](frlrfSystemXmlSerializationSoapEnumAttributeClassTopic)|Campo pubblico che rappresenta un identificatore dell'enumerazione.|Il nome dell'elemento di un membro dell'enumerazione.|  
|[SoapIgnoreAttribute](frlrfSystemXmlSerializationSoapIgnoreAttributeClassTopic)|Proprietà e campi pubblici|La proprietà o il campo devono essere ignorati se la classe che li contiene è serializzata.|  
|[SoapIncludeAttribute](frlrfSystemXmlSerializationSoapIncludeAttributeClassTopic)|Dichiarazioni della classe derivata pubblica e metodi pubblici per i documenti del linguaggio di descrizione dei servizi Web \(WSDL, Web Services Description Language\).|Il tipo deve essere incluso durante la generazione degli schemi \(per essere riconosciuto se serializzato\).|  
|[SoapTypeAttribute](frlrfSystemXmlSerializationSoapTypeAttributeClassTopic)|Dichiarazioni di classe pubblica|La classe deve essere serializzata come un tipo XML.|  
  
## Vedere anche  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [Procedura: serializzare un oggetto come flusso XML con codifica SOAP](../../../docs/framework/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)   
 [Procedura: eseguire l'override della serializzazione XML con codifica SOAP](../../../docs/framework/serialization/how-to-override-encoded-soap-xml-serialization.md)   
 [Attributi](../../../docs/standard/attributes/index.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)