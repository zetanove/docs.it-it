---
title: "117 - WorkflowInstanceTerminatedRecordWithId | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e68539d0-5338-468a-9f75-7e5b09d39a3c
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 117 - WorkflowInstanceTerminatedRecordWithId
## Proprietà  
  
|||  
|-|-|  
|ID|117|  
|Parole chiave|HealthMonitoring, WFTracking|  
|Livello|Errore|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'istanza del flusso di lavoro crea WorkflowInstanceTerminatedRecord.  
  
## Messaggio  
 TrackRecord \= WorkflowInstanceTerminatedRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, Reason \= %5, Annotations \= %6, ProfileName \= %7, WorkflowDefinitionIdentity \= %8  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|ActivityDefinitionId|xs:string|Nome dell'attività radice nel flusso di lavoro.|  
|Stato|xs:string|Stato corrente del flusso di lavoro.|  
|Annotazioni|xs:string|Annotazioni aggiunte a questo evento.  I valori sono archiviati in un elemento xml nel formato \<items\>\< item name \= "nomeAnnotazione" type\="System.String"\>valoreAnnotazione\<\/item\>\<\/items\>.  Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.  La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.  Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items\>.|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|WorkflowDefinitionIdentity|xs:string|ID della definizione del flusso di lavoro|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|