---
title: "Classe Channel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9fae2ca-209c-4341-a0f5-6b79d1a67776
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Classe Channel
Canale  
  
## Sintassi  
  
```  
class Channel  
{  
  string LocalAddress;  
  Endpoint ref;  
  string RemoteAddress;  
  string SessionId;  
  string Type;  
};  
```  
  
## Metodi  
 La classe Channel non definisce metodi.  
  
## Proprietà  
 La classe Channel presenta le proprietà seguenti.  
  
### LocalAddress  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Endpoint locale del canale.  
  
### ref  
 Tipo di dati: endpoint  
  
 Tipo di accesso: sola lettura  
  
 Riferimento all'endpoint a cui si connette il canale.  
  
### RemoteAddress  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Indirizzo remoto associato al canale.  
  
### SessionId  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 ID della sessione corrente, se presente.  
  
### Tipo  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Tipo del canale.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.ChannelBase>