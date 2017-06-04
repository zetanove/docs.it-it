---
title: "Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10ef3876-6f8e-4d4e-8444-f47847b64795
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.DurableParticipantReplayWhilePreparing
Il servizio del protocollo WS\-AT ha ricevuto un messaggio Replay da un partecipante durevole che non ha risposto a Prepare.Di conseguenza la transazione è stata interrotta.  
  
## Descrizione  
 Viene tracciato se viene ricevuto un messaggio Replay mentre un partecipante durevole è ancora in preparazione.Si tratta di un messaggio non valido per lo stato e la transazione sarà interrotta.  
  
## Risoluzione dei problemi  
 La ricezione di questo errore può indicare che un partecipante durevole \(tra cui un gestore transazioni subordinato\) ha effettuato il ripristino a seguito di un errore, ci sono tuttavia dubbi sul risultato della transazione e ne viene richiesto lo stato.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)