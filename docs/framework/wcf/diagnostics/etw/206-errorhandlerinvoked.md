---
title: "206 - ErrorHandlerInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97340f4d-4e09-4e42-a17a-982b3868dbcf
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 206 - ErrorHandlerInvoked
## Proprietà  
  
|||  
|-|-|  
|ID|206|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato dopo che un `ErrorHandler` ha avuto la possibilità di gestire un'eccezione verificatasi in un'operazione del servizio.  
  
## Messaggio  
 ErrorHandler di tipo '%1' richiamato dal dispatcher con un'eccezione di tipo '%3'.ErrorHandled \=\= '%2'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|TypeName|`xs:string`|Nome completo CLR del tipo dell'elemento `ErrorHandler` richiamato.|  
|Handled|`xs:unsignedByte`|`true` se l'errore è stato gestito. In caso contrario, `false`.|  
|ExceptionTypeName|`xs:string`|Nome completo CLR dell'eccezione gestita.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|