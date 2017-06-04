---
title: "225 - TraceCorrelationKeys | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9083aaf-3816-4c1c-bae0-2d7f49628345
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 225 - TraceCorrelationKeys
## Proprietà  
  
|||  
|-|-|  
|ID|225|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato quando per un servizio flusso di lavoro viene utilizzata la correlazione basata sul contenuto.Contiene le chiavi di correlazione applicate per correlare un messaggio a un'istanza.  
  
## Messaggio  
 Chiave di correlazione '%1' calcolata utilizzando i valori '%2' nell'ambito padre '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Chiave di istanza|`xs:GUID`|Chiave generata dai valori di correlazione.|  
|Valori|`xs:string`|Valori utilizzati per calcolare la chiave dell'istanza di correlazione.|  
|Ambito padre|`xs:string`||  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|