---
title: "3552 - MaxPendingMessagesPerChannelExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc8309d9-eb3a-4636-a6f0-dd0018c1361d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 3552 - MaxPendingMessagesPerChannelExceeded
## Proprietà  
  
|||  
|-|-|  
|ID|3552|  
|Parole chiave|Quota, WFServices|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che è stato raggiunto il limite per la velocità 'MaxPendingMessagesPerChannel'.  
  
## Messaggio  
 È stato raggiunto il limite '%1' per la velocità 'MaxPendingMessagesPerChannel'.  Per aumentare questo limite, modificare la proprietà MaxPendingMessagesPerChannel in BufferedReceiveServiceBehavior.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Limit|xs:string|È stato raggiunto il limite per la velocità MaxPendingMessagesPerChannel.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|