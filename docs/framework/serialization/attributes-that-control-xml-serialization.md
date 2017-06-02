---
title: "Attributi per il controllo della serializzazione XML | Microsoft Docs"
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
  - "classi, serializzazione"
  - "serializzazione, attributi"
  - "XML (schema), serializzazione"
  - "serializzazione XML, attributi"
  - "XmlSerializer (classe), serializzazione"
ms.assetid: 414b820f-a696-4206-b576-2711d85490c7
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Attributi per il controllo della serializzazione XML
È possibile applicare gli attributi riportati nella seguente tabella alle classi e ai membri delle classi per controllare le modalità di serializzazione o deserializzazione di un'istanza della classe da parte di [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx).Per informazioni sul modo in cui tali attributi controllano la serializzazione XML, vedere [Controllo della serializzazione XML mediante attributi](../../../docs/framework/serialization/controlling-xml-serialization-using-attributes.md).  
  
 Tali  attributi possono inoltre essere utilizzati per controllare i messaggi SOAP in stile letterale generati da qualsiasi servizio Web XML.Per ulteriori informazioni sull'applicazione di questi attributi a un metodo di servizio Web XML, vedere [Serializzazione XML con Servizi Web XML](../../../docs/framework/serialization/xml-serialization-with-xml-web-services.md).  
  
 Per ulteriori informazioni sugli attributi, vedere [Attributi](../../../docs/standard/attributes/index.md).  
  
|Attributo|Si applica a|Specifica|  
|---------------|------------------|---------------|  
|[XmlAnyAttributeAttribute](frlrfSystemXmlSerializationXmlAnyAttributeAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito che restituiscono una matrice di oggetti [XmlAttribute](frlrfSystemXmlXmlAttributeClassTopic).|Durante la deserializzazione, la matrice verrà riempita con oggetti [XmlAttribute](frlrfSystemXmlXmlAttributeClassTopic) che rappresentano tutti gli attributi XML ignoti allo schema.|  
|[XmlAnyElementAttribute](frlrfSystemXmlSerializationXmlAnyElementAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito che restituiscono una matrice di oggetti [XmlElement](frlrfSystemXmlXmlElementClassTopic).|Durante la deserializzazione, la matrice viene riempita con oggetti [XmlElement](frlrfSystemXmlXmlElementClassTopic) che rappresentano tutti gli elementi XML ignoti allo schema.|  
|[XmlArrayAttribute](frlrfSystemXmlSerializationXmlArrayAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito che restituiscono una matrice di oggetti complessi.|I membri della matrice verranno generati come membri di una matrice XML.|  
|[XmlArrayItemAttribute](frlrfSystemXmlSerializationXmlArrayItemAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito che restituiscono una matrice di oggetti complessi.|I tipi derivati che possono essere inseriti in una matrice.Applicati di solito congiuntamente a un [XmlArrayAttribute](frlrfSystemXmlSerializationXmlArrayAttributeClassTopic).|  
|[XmlAttributeAttribute](frlrfSystemXmlSerializationXmlAttributeAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito.|Il membro sarà serializzato come attributo XML.|  
|[XmlChoiceIdentifierAttribute](frlrfSystemXmlSerializationXmlChoiceIdentifierAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito.|È possibile risolvere ulteriormente l'ambiguità del membro tramite l'utilizzo di un'enumerazione.|  
|[XmlElementAttribute](frlrfSystemXmlSerializationXmlElementAttributeClassTopic)|Campo pubblico, proprietà, parametro o valore restituito.|Il campo o la proprietà verranno serializzati come elemento XML.|  
|[XmlEnumAttribute](frlrfSystemXmlSerializationXmlEnumAttributeClassTopic)|Campo pubblico che rappresenta un identificatore dell'enumerazione.|Il nome dell'elemento di un membro dell'enumerazione.|  
|[XmlIgnoreAttribute](frlrfSystemXmlSerializationXmlIgnoreAttributeClassTopic)|Proprietà e campi pubblici|La proprietà o il campo devono essere ignorati se la classe che li contiene è serializzata.|  
|[XmlIncludeAttribute](frlrfSystemXmlSerializationXmlIncludeAttributeClassTopic)|Dichiarazioni della classe derivata pubblica e valori restituiti di metodi pubblici per i documenti del linguaggio di descrizione dei servizi Web \(WSDL, Web Services Description Language\).|La classe deve essere inclusa durante la generazione degli schemi \(per essere riconosciuta se serializzata\).|  
|[XmlRootAttribute](frlrfSystemXmlSerializationXmlRootAttributeClassTopic)|Dichiarazioni di classe pubblica|Controlla la serializzazione XML della destinazione dell'attributo come un elemento radice XML.Utilizzare l'attributo per specificare ulteriormente lo spazio dei nomi e il nome dell'elemento.|  
|[XmlTextAttribute](frlrfSystemXmlSerializationXmlTextAttributeClassTopic)|Proprietà e campi pubblici|La proprietà o il campo devono essere serializzati come testo XML.|  
|[XmlTypeAttribute](frlrfSystemXmlSerializationXmlTypeAttributeClassTopic)|Dichiarazioni di classe pubblica|Nome e spazio dei nomi del tipo XML.|  
  
 Oltre a questi attributi, tutti reperibili nello spazio dei nomi [System.Xml.Serialization](frlrfSystemxmlserialization), a un campo può essere anche applicato l'attributo [System.ComponentModel.DefaultValueAttribute](frlrfSystemComponentModelDefaultValueAttributeClassTopic).**DefaultValueAttribute** imposta il valore che sarà assegnato automaticamente al membro nel caso non sia specificato alcun valore.  
  
 Per il controllo della serializzazione XML con codifica SOAP, vedere [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/framework/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
## Vedere anche  
 [Serializzazione SOAP e XML](../../../docs/framework/serialization/xml-and-soap-serialization.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [Controllo della serializzazione XML mediante attributi](../../../docs/framework/serialization/controlling-xml-serialization-using-attributes.md)   
 [Procedura: specificare un nome di elemento alternativo per un flusso XML](../../../docs/framework/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)