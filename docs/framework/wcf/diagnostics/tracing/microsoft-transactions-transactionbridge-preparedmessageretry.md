---
title: "Microsoft.Transactions.TransactionBridge.PreparedMessageRetry | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2194292d-bf5f-4aef-9336-cd3c4795cb71
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.PreparedMessageRetry
Tentativo di invio di un messaggio Prepared a un coordinatore che non risponde.  
  
## Descrizione  
 Viene tracciato se il gestore transazioni locale deve inviare nuovamente un messaggio Pepared a un coordinatore superiore poiché non viene ricevuta alcuna risposta entro un determinato periodo di tempo.  
  
## Risoluzione dei problemi  
 Esaminare i potenziali problemi della rete o del prodotto che impediscono il recapito della risposta entro il periodo di tempo specificato.La visualizzazione di molti di questi messaggi, può indicare problemi dell'infrastruttura o tempi di risposta insolitamente lunghi.Entrambi i problemi ridurranno drasticamente la velocità effettiva delle transazioni all'interno del sistema.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)