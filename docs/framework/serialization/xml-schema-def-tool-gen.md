---
title: "Procedura: utilizzare lo strumento XML Schema Definition per generare classi e documenti XML Schema. | Microsoft Docs"
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
  - "la generazione di classi XML mediante lo strumento XML Schema Definition"
  - "generazione di documenti XML Schema mediante lo strumento XML Schema Definition"
  - "Strumento XML Schema Definition, utilizzo per generare classi conformi a uno schema specifico"
  - "Strumento XML Schema Definition, utilizzo per generare documenti XML Schema"
ms.assetid: 51f0edc3-993d-4051-b7f2-77753694d3d1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: utilizzare lo strumento XML Schema Definition per generare classi e documenti XML Schema.
Lo strumento XML Schema Definition \(Xsd.exe\) consente di generare uno schema XML che descrive una classe o di generare la classe definita da uno schema XML.Le procedure descritte di seguito mostrano come eseguire queste operazioni.  
  
### Per generare classi conformi a uno schema specifico  
  
1.  Aprire un prompt dei comandi.  
  
2.  Passare lo schema XML come argomento allo strumento XML Schema Definition, che crea un set di classi esattamente corrispondenti allo schema XML, ad esempio:  
  
    ```  
    xsd mySchema.xsd  
    ```  
  
     Lo strumento è in grado di elaborare solo schemi che fanno riferimento alla specifica XML del World Wide Web Consortium del 16 marzo 2001.In altri termini, lo spazio dei nomi XML Schema deve essere "http:\/\/www.w3.org\/2001\/XMLSchema", come mostrato nell'esempio seguente.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema attributeFormDefault="qualified" elementFormDefault="qualified" targetNamespace="" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    ```  
  
3.  Modificare le classi con metodi, proprietà o campi, in base alle necessità.Per ulteriori informazioni sulla modifica di una classe con attributi, vedere [Controllo della serializzazione XML mediante attributi](../../../docs/framework/serialization/controlling-xml-serialization-using-attributes.md) e [Attributi per il controllo della serializzazione SOAP codificata](../../../docs/framework/serialization/attributes-that-control-encoded-soap-serialization.md).  
  
 Spesso risulta utile esaminare lo schema del flusso XML generato quando vengono serializzate istanze di una classe \(o di più classi\).Ad esempio, è possibile pubblicare lo schema affinché venga utilizzato da altri o è possibile confrontarlo a uno schema con il quale si sta cercando di ottenere la compatibilità.  
  
#### Per generare un documento XML Schema da un set di classi  
  
1.  Compilare la classe o le classi in una DLL.  
  
2.  Aprire un prompt dei comandi.  
  
3.  Passare la DLL come argomento a Xsd.exe, ad esempio:  
  
    ```  
    xsd MyFile.dll  
    ```  
  
     Lo schema \(o gli schemi\) sarà scritto, a partire dal nome "schema0.xsd."  
  
## Vedere anche  
 [Strumento XML Schema Definition e serializzazione XML](../../../docs/framework/serialization/the-xml-schema-definition-tool-and-xml-serialization.md)   
 [Introduzione alla serializzazione XML](../../../docs/framework/serialization/introducing-xml-serialization.md)   
 [DataSet](frlrfSystemDataDataSetClassTopic)   
 [Strumento XML Schema Definition \(Xsd.exe\)](../../../docs/framework/serialization/xml-schema-definition-tool-xsd-exe.md)   
 [XmlSerializer](https://msdn.microsoft.com/en-us/library/system.xml.serialization.xmlserializer.aspx)   
 [Procedura: serializzare un oggetto](../../../docs/framework/serialization/how-to-serialize-an-object.md)   
 [Procedura: deserializzare un oggetto](../../../docs/framework/serialization/how-to-deserialize-an-object.md)