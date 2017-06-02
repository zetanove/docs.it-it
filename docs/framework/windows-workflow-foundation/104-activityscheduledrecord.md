---
title: "104 - ActivityScheduledRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae202178-8fb1-4646-a3aa-18beeda8ff93
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 104 - ActivityScheduledRecord
## Proprietà  
  
|||  
|-|-|  
|ID|104|  
|Parole chiave|EndToEndMonitoring, Risoluzione dei problemi, HealthMonitoring, WFTracking|  
|Livello|Info|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'attività all'interno di un'istanza del flusso di lavoro crea l'oggetto ActivityScheduledRecord.  
  
## Messaggio  
 TrackRecord \= ActivityScheduledRecord, InstanceID \= %1,  RecordNumber \= %2, EventTime \= %3, Name \= %4, ActivityId \= %5, ActivityInstanceId \= %6, ActivityTypeName \= %7, ChildActivityName \= %8, ChildActivityId \= %9, ChildActivityInstanceId \= %10, ChildActivityTypeName \=%11, Annotations\=%12, ProfileName \= %13  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|Name|xs:string|Nome dell'attività che ha pianificato l'attività figlio.|  
|ActivityId|xs:string|ID dell'attività che ha pianificato l'attività figlio.|  
|ActivityInstanceId|xs:string|ID istanza dell'attività che ha pianificato l'attività figlio.|  
|ActivityTypeName|xs:string|Tipo di attività che ha richiesto l'operazione di annullamento.|  
|ChildActivityName|xs:string|Nome dell'attività pianificata.|  
|ChildActivityId|xs:string|ID dell'attività pianificata.|  
|ChildActivityInstanceId|xs:string|ID istanza dell'attività pianificata.|  
|ChildActivityTypeName|xs:string|Tipo dell'attività pianificata.|  
|Annotations|xs:string|Annotazioni aggiunte a questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "annotationName" tipo\="System.String"\>annotationValue\<\/item\>\<\/items\>.Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|HostReference|xs:string|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il relativo formato è definito come 'Nome sito Web&#124;Percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio' Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|