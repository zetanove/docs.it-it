---
title: "TextMessageEncodingBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 885e2d7a-3436-4093-bc5f-0a404c62acdc
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TextMessageEncodingBindingElement
TextMessageEncodingBindingElement  
  
## Sintassi  
  
```  
class TextMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  string Encoding;  
  sint32 MaxReadPoolSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## Metodi  
 La classe TextMessageEncodingBindingElement non definisce metodi.  
  
## Proprietà  
 La classe TextMessageEncodingBindingElement dispone delle proprietà seguenti:  
  
### Codifica  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Codifica del set di caratteri da utilizzare per l'emissione dei messaggi sull'associazione.  
  
### MaxReadPoolSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero intero che definisce il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi lettori.  
  
### MaxWritePoolSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero intero che definisce il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi scrittori.  
  
### ReaderQuotas  
 Tipo di dati: XmlDictionaryReaderQuotas  
  
 Tipo di accesso: sola lettura.  
  
 Quote dei lettori.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>