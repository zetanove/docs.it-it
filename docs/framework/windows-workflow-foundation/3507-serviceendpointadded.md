---
title: "3507 - ServiceEndpointAdded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c068fc0e-07ee-4551-9824-ea7216e1fe37
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3507 - ServiceEndpointAdded
## Proprietà  
  
|||  
|-|-|  
|ID|3507|  
|Parole chiave|WFServices|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che un endpoint del servizio è stato aggiunto.  
  
## Messaggio  
 È stato aggiunto un endpoint del servizio per l'indirizzo '%1', binding '%2' e contratto '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Address|xs:string|L'indirizzo dell'endpoint.|  
|Binding|xs:string|L'associazione dell'endpoint.|  
|Contratto|xs:string|Il contratto dell'endpoint.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|