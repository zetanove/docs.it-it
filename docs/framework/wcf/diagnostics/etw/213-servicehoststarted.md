---
title: "213 - ServiceHostStarted | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6f7facc-342f-46bb-9d52-a470178ba6bb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 213 - ServiceHostStarted
## Proprietà  
  
|||  
|-|-|  
|ID|213|  
|Parole chiave|EndToEndMonitoring, HealthMonitoring, Troubleshooting, ServiceHost|  
|Livello|LogAlways|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato quando viene avviato un host del servizio ospitato su Web.Ciò si verifica in genere quando il servizio viene attivato da un messaggio,ma anche se viene configurato per essere avviato in modo automatico.  
  
## Messaggio  
 ServiceHost avviato: '%1'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Nome tipo servizio|`xs:string`|Nome completo CLR del tipo di implementazione del servizio.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|