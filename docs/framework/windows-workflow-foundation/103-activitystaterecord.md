---
title: "103 - ActivityStateRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57636a9a-561e-44aa-aef9-1f1894aaa6dd
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 103 - ActivityStateRecord
## Proprietà  
  
|||  
|-|-|  
|ID|103|  
|Parole chiave|EndToEndMonitoring, Risoluzione dei problemi, HealthMonitoring, WFTracking|  
|Livello|Info|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Questo evento viene creato dal partecipante del rilevamento ETW quando un'attività all'interno di un'istanza del flusso di lavoro crea l'oggetto ActivityStateRecord.  
  
## Messaggio  
 TrackRecord \= ActivityStateRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, State \= %4, Name\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Arguments\=%9, Variables\=%10, Annotations\=%11, ProfileName \= %12  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InstanceId|xs:GUID|ID istanza del flusso di lavoro.|  
|RecordNumber|xs:long|Numero di sequenza del record creato.|  
|EventTime|xs:dateTime|Ora di creazione dell'evento in UTC.|  
|State|xs:string|Stato dell'attività.|  
|Name|xs:string|Nome visualizzato dell'attività che ha creato l'evento.|  
|ActivityId|xs:string|ID attività dell'attività di creazione.|  
|ActivityInstanceId|xs:string|ID istanza dell'attività dell'attività di creazione.|  
|ActivityTypeName|xs:string|Nome tipo dell'attività di creazione.|  
|Arguments|xs:string|Argomenti rilevati con questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "argumentName" tipo\="System.String"\>argumentValue\<\/item\>\<\/items\>.Se non è stato rilevato alcun argomento, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>I tipi seguenti vengono archiviati come i relativi valori quando restituiti da ToString\(\); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.Tutti gli altri tipi sono serializzati utilizzando System.Runtime.Serialization.NetDataContractSerializer.|  
|Variables|xs:string|Variabili rilevate con questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "variableName" tipo\="System.String"\>variableValue\<\/item\>\<\/items\>.Se non è stata rilevata alcuna variabile, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore delle variabili con \<items\>...\<\/items.\>I tipi seguenti vengono archiviati come i relativi valori quando restituiti da ToString\(\); string,char,bool,int,short,long,uint,ushort,ulong,System.Single,float,double,System.Guid,System.DateTimeOffset,System.DateTime.Tutti gli altri tipi sono serializzati utilizzando System.Runtime.Serialization.NetDataContractSerializer.|  
|Annotations|xs:string|Annotazioni aggiunte a questo evento.I valori sono archiviati in un elemento xml nel formato \<items\>\< nome elemento \= "annotationName" tipo\="System.String"\>annotationValue\<\/item\>\<\/items\>.Se non è specificata alcuna annotazione, la stringa contiene \<items\/\>.La dimensione dell'evento ETW è limitata da quella del buffer ETW o dal payload massimo per un evento ETW.Se la dimensione dell'evento supera i limiti ETW, l'evento viene troncato eliminando le annotazioni e sostituendo il valore di annotazione con \<items\>...\<\/items.\>|  
|ProfileName|xs:string|Nome o profilo di rilevamento che ha determinato la creazione di questo evento.|  
|HostReference|xs:string|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il relativo formato è definito come 'Nome sito Web&#124;Percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio' Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|