---
title: "OneWayBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c7e17c3-39b9-4214-ae08-9e6141734305
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# OneWayBindingElement
OneWayBindingElement  
  
## Sintassi  
  
```  
class OneWayBindingElement : BindingElement  
{  
  ChannelPoolSettings ChannelPoolSettings;  
  sint32 MaxAcceptedChannels;  
  boolean PacketRoutable;  
};  
```  
  
## Metodi  
 La classe OneWayBindingElement non definisce metodi.  
  
## Proprietà  
 La classe OneWayBindingElement dispone delle proprietà seguenti:  
  
### ChannelPoolSettings  
 Tipo di dati: ChannelPoolSettings  
  
 Tipo di accesso: in sola lettura  
  
 Impostazioni del pool di canali.  
  
### MaxAcceptedChannels  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di canali accettati.  
  
### PacketRoutable  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore che indica se il pacchetto è instradabile.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.OneWayBindingElement>