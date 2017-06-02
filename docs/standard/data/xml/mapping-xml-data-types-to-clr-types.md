---
title: "Mapping dei tipi di dati XML a tipi di dati CLR | Microsoft Docs"
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
ms.assetid: cabdfcad-f359-479b-b71c-8b2fad42ca49
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Mapping dei tipi di dati XML a tipi di dati CLR
Nella tabella seguente viene descritto il mapping predefinito tra i tipi di dati XML e i tipi CLR \(Common Language Runtime\).  
  
## Nella tabella seguente vengono descritti i mapping predefiniti di un tipo di dati XML a un tipo CLR.  
  
> [!NOTE]
>  I prefissi `xs` e `xdt` sono associati rispettivamente agli URI dello spazio dei nomi http:\/\/www.w3.org\/2001\/XMLSchema e http:\/\/www.w3.org\/2003\/05\/xpath\-datatypes.  
  
|Tipo XML|Tipo CLR|  
|--------------|--------------|  
|`xs:anyURI`|<xref:System.Uri>|  
|`xs:base64Binary`|`Byte[]`|  
|`xs:boolean`|<xref:System.Boolean>|  
|`xs:byte`|<xref:System.SByte>|  
|`xs:date`|<xref:System.DateTime>|  
|`xs:dateTime`|<xref:System.DateTime>|  
|`xs:decimal`|<xref:System.Decimal>|  
|`xs:double`|<xref:System.Double>|  
|`xs:duration`|<xref:System.TimeSpan>|  
|`xs:ENTITIES`|`String[]`|  
|`xs:ENTITY`|<xref:System.String>|  
|`xs:float`|<xref:System.Single>|  
|`xs:gDay`|<xref:System.DateTime>|  
|`xs:gMonthDay`|<xref:System.DateTime>|  
|`xs:gYear`|<xref:System.DateTime>|  
|`xs:gYearMonth`|<xref:System.DateTime>|  
|`xs:hexBinary`|`Byte[]`|  
|`xs:ID`|<xref:System.String>|  
|`xs:IDREF`|<xref:System.String>|  
|`xs:IDREFS`|`String[]`|  
|`xs:int`|<xref:System.Int32>|  
|`xs:integer`|<xref:System.Decimal>|  
|`xs:language`|<xref:System.String>|  
|`xs:long`|<xref:System.Int64>|  
|`xs:gMmonth`|<xref:System.DateTime>|  
|`xs:Name`|<xref:System.String>|  
|`xs:NCName`|<xref:System.String>|  
|`xs:negativeInteger`|<xref:System.Decimal>|  
|`xs:NMTOKEN`|<xref:System.String>|  
|`xs:NMTOKENS`|`String[]`|  
|`xs:nonNegativeInteger`|<xref:System.Decimal>|  
|`xs:nonPositiveInteger`|<xref:System.Decimal>|  
|`xs:normalizedString`|<xref:System.String>|  
|`xs:NOTATION`|<xref:System.Xml.XmlQualifiedName>|  
|`xs:positiveInteger`|<xref:System.Decimal>|  
|`xs:QName`|<xref:System.Xml.XmlQualifiedName>|  
|`xs:short`|<xref:System.Int16>|  
|`xs:string`|<xref:System.String>|  
|`xs:time`|<xref:System.DateTime>|  
|`xs:token`|<xref:System.String>|  
|`xs:unsignedByte`|<xref:System.Byte>|  
|`xs:unsignedInt`|<xref:System.UInt32>|  
|`xs:unsignedLong`|<xref:System.UInt64>|  
|`xs:unsignedShort`|<xref:System.UInt16>|  
|`xdt:dayTimeDuration`|<xref:System.TimeSpan>|  
|`xdt:yearMonthDuration`|<xref:System.TimeSpan>|  
|`xdt:untypedAtomic`|<xref:System.String>|  
|`xdt:anyAtomicType`|<xref:System.Object>|  
|`xs:anySimpleType`|<xref:System.String>|  
|Nodo documento|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo elemento|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo attributo|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo spazio dei nomi|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo testo|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo commento|<xref:System.Xml.XPath.XPathNavigator>|  
|Nodo istruzione di elaborazione|<xref:System.Xml.XPath.XPathNavigator>|  
  
## Vedere anche  
 [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)