---
title: "1002 - WorkflowApplicationTerminated | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e8b111f-79dc-4898-bb4a-e9b36f69420f
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 1002 - WorkflowApplicationTerminated
## Proprietà  
  
|||  
|-|-|  
|ID|1002|  
|Parole chiave|WFRuntime|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un'applicazione flusso di lavoro è terminata nello stato Faulted con un'eccezione.  
  
## Messaggio  
 WorkflowApplication con ID: '%1' terminata.  È stata completata nello stato Faulted con un'eccezione.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|WorkflowApplicationId|`xs:string`|ID applicazione flusso di lavoro|  
|Eccezione|`xs:string`|Dettagli dell'eccezione.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|