---
title: "212 - ParameterInspectorBeforeCallInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 063fc8d2-ceac-4c18-8368-de84f2c78035
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 212 - ParameterInspectorBeforeCallInvoked
## Proprietà  
  
|||  
|-|-|  
|ID|212|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dopo che il modello di servizi ha richiamato il metodo `BeforeCall` su un `ParameterInspector`.  
  
## Messaggio  
 Il dispatcher ha richiamato 'BeforeCall' in un ParameterInspector di tipo '%1'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|TypeName|`xs:string`|Nome completo CLR del tipo di controllo richiamato.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|