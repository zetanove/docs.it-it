---
title: "207 - FaultProviderInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b730d903-01c2-4deb-85a4-da12f8a21fe4
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 207 - FaultProviderInvoked
## Proprietà  
  
|||  
|-|-|  
|ID|207|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dopo che è stato richiamato un elemento `FaultProvider`.  
  
## Messaggio  
 FaultProvider di tipo '%1' richiamato dal dispatcher con un'eccezione di tipo '%2'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|TypeName|`xs:string`|Nome completo CLR del tipo dell'elemento `FaultProvider` richiamato.|  
|ExceptionTypeName|`xs:string`|Nome completo CLR dell'eccezione usata da `FaultProvider`.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.  Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.  Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|