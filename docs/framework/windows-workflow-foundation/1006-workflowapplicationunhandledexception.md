---
title: "1006 - WorkflowApplicationUnhandledException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dfe0f316-e03b-47fb-b6a3-622c56bfd753
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1006 - WorkflowApplicationUnhandledException
## Proprietà  
  
|||  
|-|-|  
|ID|1006|  
|Parole chiave|WFRuntime|  
|Livello|Errore|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un'applicazione flusso di lavoro ha rilevato un'eccezione non gestita.  
  
## Messaggio  
 WorkflowInstance con ID: '%1' ha riscontrato un'eccezione non gestita. Eccezione originata dall'attività '%2', DisplayName: '%3'. Verrà effettuata l'azione seguente: %4.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|WorkflowInstanceId|`xs:string`|ID istanza del flusso di lavoro.|  
|Eccezione|`xs:string`|Dettagli dell'eccezione.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|