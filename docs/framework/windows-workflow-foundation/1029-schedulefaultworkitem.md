---
title: "1029 - ScheduleFaultWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a56b29e-f740-459d-8576-d81e58bf5a03
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1029 - ScheduleFaultWorkItem
## Proprietà  
  
|||  
|-|-|  
|ID|1029|  
|Parole chiave|WFRuntime|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un elemento FaultWorkItem è stato pianificato.  
  
## Messaggio  
 FaultWorkItem pianificato per l'attività '%1', DisplayName: '%2', InstanceId: '%3'. Eccezione propagata dall'attività '%4', DisplayName: '%5', InstanceId: '%6'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|FaultActivity|xs:string|Il nome del tipo di attività fault.|  
|FaultActivityDisplayName|xs:string|Nome visualizzato dell'attività fault.|  
|FaultActivityInstanceId|xs:string|ID dell'istanza dell'attività fault.|  
|ExceptionActivity|xs:string|Il nome del tipo di attività che ha generato l'eccezione.|  
|ExceptionActivityDisplayName|xs:string|Il nome visualizzato dell'attività che ha generato l'eccezione.|  
|ExceptionActivityInstanceId|xs:string|ID dell'istanza dell'attività che ha generato l'eccezione.|  
|Eccezione|xs:string|Dettagli dell'eccezione.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|