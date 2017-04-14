---
title: "BinaryMessageEncodingBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2bb3cdd-3bbd-4bb5-85fe-570457500a66
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# BinaryMessageEncodingBindingElement
BinaryMessageEncodingBindingElement  
  
## Sintassi  
  
```  
class BinaryMessageEncodingBindingElement : MessageEncodingBindingElement  
{  
  sint32 MaxReadPoolSize;  
  sint32 MaxSessionSize;  
  sint32 MaxWritePoolSize;  
  XmlDictionaryReaderQuotas ReaderQuotas;  
};  
```  
  
## Metodi  
 La classe BinaryMessageEncodingBindingElement non definisce metodi.  
  
## Proprietà  
 La classe BinaryMessageEncodingBindingElement dispone delle proprietà seguenti.  
  
## MaxReadPoolSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero intero che definisce il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi lettori.  
  
## MaxSessionSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Valore che specifica la dimensione, in byte, del buffer usato per la codifica.  
  
## MaxWritePoolSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero intero che definisce il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi writer.  
  
## ReaderQuotas  
 Tipo di dati: XmlDictionaryReaderQuotas  
  
 Tipo di accesso: sola lettura  
  
 Quote dei lettori.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>