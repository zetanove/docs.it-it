---
title: "1104 - WorkflowActivityResume | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7fe95d1e-34bd-43ca-b92e-587d2d248fff
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1104 - WorkflowActivityResume
## Proprietà  
  
|||  
|-|-|  
|ID|1104|  
|Parole chiave|WFRuntime|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un'attività del flusso di lavoro è stata ripresa.  
  
## Messaggio  
 Attività end\-to\-end di WorkflowInstance con ID: '%1'  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|WorkflowInstanceId|xs:string|ID dell'istanza del flusso di lavoro.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|