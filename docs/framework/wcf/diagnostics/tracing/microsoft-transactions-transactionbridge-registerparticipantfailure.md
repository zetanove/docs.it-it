---
title: "Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a4ead79-8550-4037-84e3-fd70ff56e001
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.RegisterParticipantFailure
Servizio del protocollo WS\-AT: impossibile registrare un partecipante per un protocollo di controllo.  
  
## Descrizione  
 Viene tracciato se MSDTC rileva una richiesta di registrazione non valida.Può essere causato da più richieste di registrazione di completamento e da errori interni.  
  
## Risoluzione dei problemi  
 Non tentare la registrazione di completamento più di una volta.Controllare inoltre la stringa di stato all'interno del messaggio di traccia per determinare se esiste un elemento processabile.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)