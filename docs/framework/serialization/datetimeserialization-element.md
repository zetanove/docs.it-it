---
title: "Elemento &lt;dateTimeSerialization&gt; | Microsoft Docs"
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
  - "Elemento <dateTimeSerialization>"
  - "Elemento dateTimeSerialization"
  - "serializzazione XML, configurazione"
ms.assetid: 90fda55c-7730-41e9-bc4b-6423a4b920af
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Elemento &lt;dateTimeSerialization&gt;
Determina la modalità di serializzazione degli oggetti <xref:System.DateTime>.  
  
## Sintassi  
  
```  
  
<dateTimeSerialization  
    mode = "Roundtrip" | "Local"  
/>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributi|Descrizione|  
|---------------|-----------------|  
|`mode`|Parametro facoltativo.  Specifica la modalità di serializzazione.  Impostarlo a uno dei valori di <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>.  Il valore predefinito è **RoundTrip**.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|system.xml.serialization|L'elemento di primo livello per il controllo della serializzazione XML.|  
  
## Note  
 Nelle versioni 1.0, 1.1, 2.0 e successive di .NET Framework, se la proprietà è impostata su **Local**, gli oggetti <xref:System.DateTime> vengono sempre formattati come ora locale.  Vale a dire che le informazioni relative al fuso orario locale vengono sempre incluse tra dati serializzati.  Impostare questa proprietà su **Local** per garantire la compatibilità con le versioni precedenti di .NET Framework.  
  
 Nella versione 2.0 e versioni successive di .NET Framework in cui la proprietà è impostata su **Roundtrip**, gli oggetti <xref:System.DateTime> vengono esaminati in modo da determinare se si trovano nel fuso orario locale, UTC o in un fuso orario non specificato.  Gli oggetti <xref:System.DateTime> vengono quindi serializzati in modo tale che tali informazioni vengano preservate.  Si tratta del comportamento predefinito, consigliato per tutte le nuove applicazioni che non comunicano con le versioni precedenti del framework.  
  
## Vedere anche  
 <xref:System.DateTime>   
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>   
 [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Elemento \<schemaImporterExtensions\>](../../../docs/framework/serialization/schemaimporterextensions-element.md)   
 [Elemento \<add\> per \<xmlSchemaImporterExtensions\>](../../../docs/framework/serialization/add-element-for-xmlschemaimporterextensions.md)   
 [Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)