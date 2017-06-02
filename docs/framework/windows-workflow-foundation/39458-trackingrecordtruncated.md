---
title: "39458 - TrackingRecordTruncated | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5352f0eb-d571-454a-bab5-e2162888b218
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 39458 - TrackingRecordTruncated
## Proprietà  
  
|||  
|-|-|  
|ID|39458|  
|Parole chiave|WFTracking|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un record di rilevamento è stato troncato.  Variabili\/annotazioni\/dati utente rimossi.  
  
## Messaggio  
 Record di rilevamento %1 troncato scritto nella sessione ETW con il provider %2.  Variabili\/annotazioni\/dati utente rimossi  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|RecordNumber|xs:string|Numero del record di rilevamento.|  
|ProviderId|xs:string|ID del provider ETW.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|