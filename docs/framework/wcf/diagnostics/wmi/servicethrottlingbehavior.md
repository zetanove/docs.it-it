---
title: "ServiceThrottlingBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37b9e517-1f1f-4ec4-9fcb-2b8016794f5b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# ServiceThrottlingBehavior
ServiceThrottlingBehavior  
  
## Sintassi  
  
```  
class ServiceThrottlingBehavior : Behavior  
{  
  sint32 MaxConcurrentCalls;  
  sint32 MaxConcurrentInstances;  
  sint32 MaxConcurrentSessions;  
};  
```  
  
## Metodi  
 La classe ServiceThrottlingBehavior non definisce metodi.  
  
## Proprietà  
 La classe ServiceThrottlingBehavior dispone delle proprietà seguenti:  
  
### MaxConcurrentCalls  
 Tipo di dati: sint32  
  
 Tipo di accesso: in sola lettura  
  
 Numero massimo di messaggi elaborati attivamente in tutti gli oggetti dispatcher in un ServiceHost.  
  
### MaxConcurrentInstances  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di oggetti servizio che possono essere eseguiti contemporaneamente.  
  
### MaxConcurrentSessions  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di sessioni che un host può accettare contemporaneamente.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>