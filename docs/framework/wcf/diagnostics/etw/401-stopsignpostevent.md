---
title: "401- StopSignPostEvent | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e033d03a-510d-4300-aa65-ef02cb4807f2
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 401- StopSignPostEvent
## Proprietà  
  
|||  
|-|-|  
|ID|401|  
|Parole chiave|Risoluzione dei problemi|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento contrassegna la fine di un'attività end\-to\-end  contenente il nome dell’attività.  
  
## Messaggio  
 Limite dell'attività.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Dati estesi|`xs:string`|Nome dell'attività.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|