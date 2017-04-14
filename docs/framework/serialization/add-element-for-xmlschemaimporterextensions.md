---
title: "Elemento &lt;add&gt; per &lt;xmlSchemaImporterExtensions&gt; | Microsoft Docs"
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
  - "Elemento <add> per <xmlSchemaImporterExtensions>"
  - "serializzazione XML, configurazione"
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Elemento &lt;add&gt; per &lt;xmlSchemaImporterExtensions&gt;
Aggiunge i tipi usati da <xref:System.Xml.Serialization.XmlSchemaImporter> per l'esecuzione del mapping dei tipi XSD ai tipi .NET Framework.  Per altre informazioni sui file di configurazione, vedere [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md).  
  
 \<XmlSchemaImporterExtensions\>  
\<add\>  
  
## Sintassi  
  
```  
  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**name**|Un nome semplice usato per cercare l'istanza.|  
|**type**|Obbligatorio.  Specifica la classe delle estensioni dello schema da aggiungere.  Il valore dell'attributo **type** deve trovarsi su una riga e includere il nome completo del tipo.  Quando l'assembly viene inserito nella Global Assembly Cache \(GAC\) deve includere anche la versione, le impostazioni cultura e il token di chiave pubblica dell'assembly firmato.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|\<xmlSchemaImporterExtensions\>|Contiene i tipi usati da <xref:System.Xml.Serialization.XmlSchemaImporter>.|  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene aggiunto un tipo di estensione utilizzabile da XmlSchemaImporter durante l'esecuzione del mapping dei tipi.  
  
```  
<configuration>  
  <system.xml.serialization>  
    <xmlSchemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,   
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,   
       PublicKeyToken=b03f5f7f11d50a3a" />   
    </xmlSchemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Xml.Serialization.XmlSchemaImporter>   
 [Elemento \<system.xml.serialization\>](../../../docs/framework/serialization/system-xml-serialization-element.md)   
 [Elemento \<schemaImporterExtensions\>](../../../docs/framework/serialization/schemaimporterextensions-element.md)