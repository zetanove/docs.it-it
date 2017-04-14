---
title: "205 - OperationInvoked | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c8d6c90-dfa5-4ae0-a589-96679a8fb3ba
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 205 - OperationInvoked
## Proprietà  
  
|||  
|-|-|  
|ID|205|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento viene generato precedentemente alla chiamata a un metodo da parte dell'elemento `OperationInvoker` predefinito del modello di servizi.  
  
## Messaggio  
 Metodo '%1' richiamato da OperationInvoker.Informazioni sul chiamante: '%2'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Nome metodo|`xs:string`|Nome CLR del metodo richiamato dall'elemento `OperationInvoker`.|  
|Informazioni sul chiamante|`xs:string`|Indirizzo IP e numero di porta del client nel formato 'IndirizzoIP:NumeroPorta'.I due valori vengono recuperati dalla proprietà 'System.ServiceModel.Channels.RemoteEndpointMessageProperty' del messaggio all'interno del contesto dell'operazione.Per le associazioni non TCP questo valore è `null`.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|