---
title: "Microsoft.Transactions.TransactionBridge.CoordinatorStateMachineFinished | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16cb428d-d886-4789-a961-6fded4b0dbba
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.CoordinatorStateMachineFinished
Il computer di stato per l'integrazione di un coordinatore è in stato di operazione completata.  
  
## Descrizione  
 Traccia eseguita quando il gestore transazioni locale ritiene che l'integrazione di un coordinatore superiore abbia completato l'elaborazione 2pc.Il risultato dell'integrazione può essere Committed, Aborted o Forgotten.Questa traccia viene inoltre eseguita se il gestore transazioni locale vota ReadOnly durante la fase di preparazione.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)