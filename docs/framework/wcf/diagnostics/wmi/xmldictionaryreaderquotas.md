---
title: "XmlDictionaryReaderQuotas | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b4ca8b4-0a89-4758-97ab-528a8ce18f07
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# XmlDictionaryReaderQuotas
XmlDictionaryReaderQuotas  
  
## Sintassi  
  
```  
class XmlDictionaryReaderQuotas  
{  
  sint32 MaxArrayLength;  
  sint32 MaxBytesPerRead;  
  sint32 MaxDepth;  
  sint32 MaxNameTableCharCount;  
  sint32 MaxStringContentLength;  
};  
```  
  
## Metodi  
 La classe XmlDictionaryReaderQuotas non definisce metodi.  
  
## Proprietà  
 La classe XmlDictionaryReaderQuotas presenta le proprietà seguenti:  
  
### MaxArrayLength  
 Tipo di dati: sint32  
  
 Tipo di accesso: in sola lettura  
  
 Lunghezza massima consentita della matrice.  
  
### MaxBytesPerRead  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Byte massimi consentiti restituiti per ogni lettura.  
  
### MaxDepth  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Profondità massima dei nodi annidati per ogni lettura.  
  
### MaxNameTableCharCount  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Caratteri massimi consentiti in un nome di tabella.  
  
### MaxStringContentLength  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Caratteri massimi consentiti nel contenuto di un elemento XML.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.Xml.XmlDictionaryReaderQuotas>   
 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>