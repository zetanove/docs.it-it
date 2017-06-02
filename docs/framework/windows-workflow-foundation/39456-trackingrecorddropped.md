---
title: "39456 - TrackingRecordDropped | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: da13d5bc-1736-47a4-b3fd-064ca8040326
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 39456 - TrackingRecordDropped
## Proprietà  
  
|||  
|-|-|  
|ID|39456|  
|Parole chiave|WFTracking|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un record di rilevamento è stato eliminato perché le dimensioni superano il massimo consentito dal provider della sessione ETW.  
  
## Messaggio  
 La dimensione del record di rilevamento %1 supera il valore massimo consentito dalla sessione ETW per il provider %2  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Eccezione|xs:string|Dettagli dell'eccezione.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|