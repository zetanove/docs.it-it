---
title: "57398 - MaxInstancesExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f943d209-dfeb-43e5-b572-c9a06217936e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 57398 - MaxInstancesExceeded
## Proprietà  
  
|||  
|-|-|  
|ID|57398|  
|Parole chiave|WFServices|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che il sistema ha raggiunto il limite impostato per la velocità 'MaxConcurrentInstances'.  
  
## Messaggio  
 Il sistema ha raggiunto il limite impostato per la velocità 'MaxConcurrentInstances'.  Il limite per questa velocità è stato impostato su %1.  Il valore della velocità può essere modificato cambiando l'attributo 'maxConcurrentInstances' nell'elemento serviceThrottle o modificando la proprietà 'MaxConcurrentInstances' nel comportamento ServiceThrottlingBehavior.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Nome|xs:string|Nome dell'elemento.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|