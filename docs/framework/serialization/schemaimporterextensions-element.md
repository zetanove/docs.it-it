---
title: "Elemento &lt;schemaImporterExtensions&gt; | Microsoft Docs"
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
  - "Elemento <schemaImporterExtensions>"
  - "Elemento schemaImporterExtensions"
  - "serializzazione XML, configurazione"
ms.assetid: 465ef2a0-f909-4ac1-9a56-0ead5c849698
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Elemento &lt;schemaImporterExtensions&gt;
Contiene tipi utilizzati da <xref:System.Xml.Serialization.XmlSchemaImporter> per l'esecuzione del mapping dei tipi XSD ai tipi .NET Framework.  Per ulteriori informazioni sui file di configurazione, vedere [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md) .  
  
## Sintassi  
  
```  
  
<schemaImporterExtensions>  
    <!-- Add types -->  
</SchemaImporterExtension>  
```  
  
## Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<add\> per \<xmlSchemaImporterExtensions\>](../../../docs/framework/serialization/add-element-for-xmlschemaimporterextensions.md)|Aggiunge tipi utilizzati da <xref:System.Xml.Serialization.XmlSchemaImporter> per creare i mapping.|  
  
## Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)|L'elemento di primo livello per il controllo della serializzazione XML.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come aggiungere tipi utilizzati da <xref:System.Xml.Serialization.XmlSchemaImporter> in caso di esecuzione del mapping di tipi XSD ai tipi .NET Framework.  
  
```  
<system.xml.serialization>  
    <schemaImporterExtensions>  
        <add name = "MobileCapabilities" type =   
        "System.Web.Mobile.MobileCapabilities,   
        System.Web.Mobile, Version - 2.0.0.0, Culture = neutral,   
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
/system.sxml.serializaiton>  
```  
  
## Vedere anche  
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>   
 [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<dateTimeSerialization\>](../../../docs/framework/serialization/datetimeserialization-element.md)   
 [Elemento \<add\> per \<xmlSchemaImporterExtensions\>](../../../docs/framework/serialization/add-element-for-xmlschemaimporterextensions.md)   
 [Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)