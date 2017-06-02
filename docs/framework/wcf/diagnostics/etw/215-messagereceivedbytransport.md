---
title: "215 - MessageReceivedByTransport | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bb32aa60-5207-4711-9f08-110e8ac327e5
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 215 - MessageReceivedByTransport
## Proprietà  
  
|||  
|-|-|  
|ID|215|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento si verifica quando un trasporto basato su TCP riceve un messaggio.  Si noti che a livello di trasporto è possibile che si verifichi lo scambio di più messaggi tra client e servizi per una singola operazione.  Questo può dipendere dal comportamento dell'infrastruttura \(un esempio valido può essere rappresentato dalla sicurezza\).  Pertanto, il numero di eventi `MessageReceivedByTransport` generati varia in base all'associazione del servizio e alla relativa configurazione.  
  
> [!NOTE]
>  Questo evento non viene generato per i trasporti unidirezionali.  
  
## Messaggio  
 Il trasporto ha ricevuto un messaggio da '%1'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Indirizzo di ascolto|`xs:string`|Indirizzo che riceve il messaggio.|  
|HostReference|`xs:string`|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.  Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.  Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|