---
title: "210 - MessageThrottleExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24ca08ea-c11c-4753-946e-98aa820f8711
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 210 - MessageThrottleExceeded
## Proprietà  
  
|||  
|-|-|  
|ID|210|  
|Parole chiave|EndToEndMonitoring, HealthMonitoring, Troubleshooting, ServiceModel|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato quando viene superata una delle tre velocità del servizio principali.L'evento viene generato solo quando il limite di velocità viene superato in fase iniziale.Se ad esempio il limite di velocità per le chiamate simultanee è 10, l'11ª chiamata simultanea comporta un evento `MessageThrottleExceeded`.La 12ª chiamata non comporta un altro evento.Un'attività che si aggira intorno al limite non comporta inoltre un altro evento, per evitare un flusso di eventi problematico.In questo esempio, se due chiamate vengono completate, saranno presenti 9 chiamate simultanee.Se in seguito entrano altre due chiamate, il valore corrente sarà nuovamente 11.Questa situazione non comporta un altro evento.Se il valore corrente corrisponde al 70% del limite di velocità, viene generato un evento diverso che indica che l'attività è rallentata.Un'attività futura che supera il limite comporta un altro evento `MessageThrottleExceeded` generato.In questo esempio, se la quantità di chiamate simultanee corrisponde a 7 e quindi nuovamente a 11, viene generato un altro evento `MessageThrottleExceeded`.  
  
## Messaggio  
 È stato raggiunto il limite di velocità '%1' di '%2'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Nome velocità|`xs:string`|Nome della velocità superata:`MaxConcurrentCalls`, `MaxConcurrentInstances` o `MaxConcurrentSessions`,|  
|Limit|`xs:long`|Limite attualmente configurato della velocità.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|