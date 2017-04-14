---
title: "208 - MessageInspectorAfterReceiveInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dfb5f7b0-4346-4949-8104-351726b1f502
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 208 - MessageInspectorAfterReceiveInvoked
## Proprietà  
  
|||  
|-|-|  
|ID|208|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dopo che il modello di servizi ha richiamato il metodo `AfterReceive` su un controllo dei messaggi.  
  
## Messaggio  
 'AfterReceiveReply' richiamato dal dispatcher in un elemento MessageInspector di tipo '%1'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|TypeName|`xs:string`|Nome completo CLR del tipo dell'elemento `MessageInspector` richiamato.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.  Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.  Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|