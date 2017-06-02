---
title: "105 - FaultPropagationRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 168473b1-b1e5-4e9f-8a2a-35bbdb2ef531
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 105 - FaultPropagationRecord
## Proprietà  
  
|||  
|-|-|  
|ID|105|  
|Parole chiave|EndToEndMonitoring, Risoluzione dei problemi, HealthMonitoring, WFTracking|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'attività con l'istanza del flusso di lavoro crea l'oggetto FaultPropagationRecord.  
  
## Messaggio  
 TrackRecord \= FaultPropagationRecord, InstanceID\=%1, RecordNumber\=%2, EventTime\=%3, FaultSourceActivityName\=%4, FaultSourceActivityId\=%5, FaultSourceActivityInstanceId\=%6, FaultSourceActivityTypeName\=%7, FaultHandlerActivityName\=%8,  FaultHandlerActivityId \= %9, FaultHandlerActivityInstanceId \=%10, FaultHandlerActivityTypeName\=%11, Fault\=%12, IsFaultSource\=%13, Annotations\=%14, ProfileName \= %15  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|FaultSourceActivityName|xs:string|Nome dell'attività che ha creato l'errore.|  
|FaultSourceActivityId|xs:string|ID dell'attività che ha creato l'errore.|  
|FaultSourceActivityInstanceId|xs:string|ID istanza dell'attività che ha creato l'errore.|  
|FaultSourceActivityTypeName|xs:string|Tipo dell'attività che ha creato l'errore.|  
|FaultHandlerActivityName|xs:string|Nome visualizzato dell'attività del gestore fault.|  
|FaultHandlerActivityId|xs:string|ID dell'attività del gestore fault.|  
|FaultHandlerActivityInstanceId|xs:string|ID istanza dell'attività del gestore fault.|  
|FaultHandlerActivityTypeName|xs:string|Tipo dell'attività del gestore fault.|  
|Fault|xs:string|Dettagli dell'errore.|  
|IsFaultSource|xs:unsignedByte|Indica se l'evento è stato creato dall'origine dell'errore.|  
|Annotations|xs:string|Annotazioni aggiunte a questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "annotationName" tipo\="System.String"\>annotationValue\<\/item\>\<\/items\>.Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|HostReference|xs:string|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il relativo formato è definito come 'Nome sito Web&#124;Percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio' Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|