---
title: "TransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54ecfbee-53c0-410c-a7fa-a98f2e40c545
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TransportBindingElement
TransportBindingElement  
  
## Sintassi  
  
```  
class TransportBindingElement : BindingElement  
{  
  boolean ManualAddressing;  
  sint64 MaxBufferPoolSize;  
  sint64 MaxReceivedMessageSize;  
  string Scheme;  
};  
```  
  
## Metodi  
 La classe TransportBindingElement non definisce metodi.  
  
## Proprietà  
 La classe TransportBindingElement dispone delle proprietà seguenti:  
  
### ManualAddressing  
 Tipo di dati: booleano  
  
 Tipo di accesso: in sola lettura  
  
 Valore booleano che specifica se l'utente desidera controllare l'indirizzamento dei messaggi.  
  
### MaxBufferPoolSize  
 Tipo di dati: sint64  
  
 Tipo di accesso: sola lettura.  
  
 Dimensioni massime del pool di buffer dell'associazione.  
  
### MaxReceivedMessageSize  
 Tipo di dati: sint64  
  
 Tipo di accesso: sola lettura.  
  
 Dimensioni massime di un messaggio elaborato dall'associazione.  
  
### Scheme  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura.  
  
 Schema URI del trasporto.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.TransportBindingElement>