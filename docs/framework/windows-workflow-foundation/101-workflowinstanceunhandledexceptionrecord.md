---
title: "101 - WorkflowInstanceUnhandledExceptionRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab7d50a0-5347-4390-8445-1def4dfdff6a
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 101 - WorkflowInstanceUnhandledExceptionRecord
## Proprietà  
  
|||  
|-|-|  
|ID|101|  
|Parole chiave|EndToEndMonitoring, Risoluzione dei problemi, HealthMonitoring, WFTracking|  
|Livello|Errore|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'istanza del flusso di lavoro crea WorkflowInstanceUnhandledExceptionRecord.  
  
## Messaggio  
 TrackRecord \= WorkflowInstanceUnhandledExceptionRecord, InstanceID \= %1, RecordNumber \= %2, EventTime \= %3, ActivityDefinitionId \= %4, SourceName \= %5, SourceId \= %6, SourceInstanceId \= %7, SourceTypeName\=%8, Exception\=%9, Annotations\= %10, ProfileName \= %11  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|ActivityDefinitionId|xs:string|Nome dell'attività radice nel flusso di lavoro.|  
|SourceName|xs:string|Nome dell'attività di origine in cui si è verificato un errore che ha comportato l'eccezione unhandledException.|  
|SourceId|xs:string|ID attività dell'attività di origine dell'errore.|  
|SourceInstanceId|xs:string|ID istanza dell'attività di origine dell'errore.|  
|SourceTypeName|xs:string|Nome del tipo dell'attività di origine in cui si è verificato un errore che ha comportato l'eccezione unhandledException.|  
|Exception|xs:string|Dettagli dell'eccezione non gestita.|  
|Annotations|xs:string|Annotazioni aggiunte a questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "annotationName" tipo\="System.String"\>annotationValue\<\/item\>\<\/items\>.Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|HostReference|xs:string|Per i servizi ospitati su Web questo campo identifica in modo univoco il servizio nella gerarchia Web.Si tratta del formato definito come 'Nome sito Web&#124;Percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio' Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|