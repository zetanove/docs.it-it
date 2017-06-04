---
title: "Elemento &lt;system.xml.serialization&gt; | Microsoft Docs"
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
  - "Elemento <system.xml.serialization>"
  - "Elemento system.xml.serialization"
  - "serializzazione XML, configurazione"
ms.assetid: 3ce45919-388a-418c-8968-6df0372c73ec
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Elemento &lt;system.xml.serialization&gt;
L'elemento di primo livello per il controllo della serializzazione XML.  Per altre informazioni sui file di configurazione, vedere [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md).  
  
## Sintassi  
  
```  
  
<system.xml.serialization>  
</system.xml.serialization>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<dateTimeSerialization\>](../../../docs/framework/serialization/datetimeserialization-element.md)|Determina la modalità di serializzazione degli oggetti <xref:System.DateTime>.|  
|[Elemento \<schemaImporterExtensions\>](../../../docs/framework/serialization/schemaimporterextensions-element.md)|Contiene tipi usati da <xref:System.Xml.Serialization.XmlSchemaImporter> per l'esecuzione del mapping dei tipi XSD ai tipi .NET Framework.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<Configuration\>](../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento radice in ogni file di configurazione usato dal Common Language Runtime e dalle applicazioni .NET Framework.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come specificare la modalità di serializzazione di un oggetto <xref:System.DateTime> e l'aggiunta dei tipi usati da <xref:System.Xml.Serialization.XmlSchemaImporter> in caso di esecuzione del mapping di tipi XSD ai tipi .NET Framework.  
  
```  
<system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
    <dateTimeSerialization mode = "Local" />  
    <schemaImporterExtensions>  
        <add   
        name = "MobileCapabilities"   
        type = "System.Web.Mobile.MobileCapabilities,   
        System.Web.Mobile, Version - 2.0.0.0, Culture = neuutral,   
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
</system.sxml.serialization>  
```  
  
## Vedere anche  
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>   
 [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<dateTimeSerialization\>](../../../docs/framework/serialization/datetimeserialization-element.md)   
 [Elemento \<schemaImporterExtensions\>](../../../docs/framework/serialization/schemaimporterextensions-element.md)   
 [Elemento \<add\> per \<xmlSchemaImporterExtensions\>](../../../docs/framework/serialization/add-element-for-xmlschemaimporterextensions.md)