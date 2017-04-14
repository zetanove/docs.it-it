---
title: "108 - CustomTrackingRecordInfo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5bee501e-4e00-42cd-b949-e88009c3d4e8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 108 - CustomTrackingRecordInfo
## Proprietà  
  
|||  
|-|-|  
|ID|108|  
|Parole chiave|UserEvents, EndToEndMonitoring, Risoluzione dei problemi, HealthMonitoring, WFTracking|  
|Livello|Info|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'attività all'interno di un'istanza del flusso di lavoro crea l'oggetto CustomTrackingRecord con informazioni sul livello.  
  
## Messaggio  
 TrackRecord \= CustomTrackingRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3,  Name\=%4, ActivityName\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Data\=%9, Annotations\=%10, ProfileName \= %11  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|Name|xs:string|Nome dell'oggetto CustomTrackingRecord.|  
|ActivityName|xs:string|Nome dell'attività che ha creato l'oggetto CustomTrackingRecord.|  
|ActivityId|xs:string|ID dell'attività che ha creato l'oggetto CustomTrackingRecord.|  
|ActivityInstanceId|xs:string|ID istanza dell'attività che ha creato l'oggetto CustomTrackingRecord.|  
|ActivityTypeName|xs:string|Nome dell'attività che ha creato l'oggetto CustomTrackingRecord.|  
|Data|xs:string|Dati rilevati con questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "dataName" tipo\="System.String"\>dataValue\<\/item\>\<\/items\>.Se non è stato rilevato alcun dato, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore dei dati con \<items\>...\<\/items.\>I tipi seguenti vengono archiviati come i relativi valori quando restituiti da ToString\(\); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.Tutti gli altri tipi sono serializzati utilizzando System.Runtime.Serialization.NetDataContractSerializer.|  
|Annotations|xs:string|Annotazioni aggiunte a questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "annotationName" tipo\="System.String"\>annotationValue\<\/item\>\<\/items\>.Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|HostReference|xs:string|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il relativo formato è definito come 'Nome sito Web&#124;Percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio' Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|