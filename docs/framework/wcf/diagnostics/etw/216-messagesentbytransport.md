---
title: "216 - MessageSentByTransport | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 150c3167-4154-4225-8d94-57cc94341233
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 216 - MessageSentByTransport
## Proprietà  
  
|||  
|-|-|  
|ID|216|  
|Parole chiave|Troubleshooting, ServiceModel|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento si verifica nel caso in cui un trasporto basato su TCP invia un messaggio.A livello di trasporto è possibile scambiare più messaggi tra client e servizi per una sola operazione.Ciò può essere dovuto a un comportamento dell'infrastruttura \(un esempio valido può essere rappresentato dalla sicurezza\).Pertanto, il numero di eventi **MessageSentByTransport** generato varia in base all'associazione del servizio e alla relativa configurazione.  
  
## Messaggio  
 Il trasporto ha inviato un messaggio a '%1'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|DestinationAddress|`xs:string`|L'indirizzo a cui è stato inviato il messaggio di richiesta.|  
|HostReference|xs:string|Per i servizi ospitati su Web, questo campo identifica in modo univoco il servizio nella gerarchia Web.Il formato viene definito come 'Nome sito Web percorso virtuale applicazione&#124;Percorso virtuale servizio&#124;NomeServizio'.Esempio: 'Sito Web predefinito\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService'.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|