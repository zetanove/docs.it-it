---
title: "Microsoft.Transactions.TransactionBridge.CreateTransactionFailure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3468e23-49a9-4a84-972d-a79a658851b3
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Microsoft.Transactions.TransactionBridge.CreateTransactionFailure
Impossibile creare una transazione.  
  
## Descrizione  
 Questa traccia viene generata quando MSDTC non è in grado di creare una transazione.  Questo problema può essere causato da risorse o spazio del registro insufficiente, oppure da altri errori.  
  
## Risoluzione dei problemi  
 Controllare la stringa di stato all'interno del messaggio di traccia per determinare se esiste un elemento processabile.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)