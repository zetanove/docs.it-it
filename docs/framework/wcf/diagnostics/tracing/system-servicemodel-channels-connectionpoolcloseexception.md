---
title: "System.ServiceModel.Channels.ConnectionPoolCloseException | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8358898e-129e-4fac-a6bf-bf3aa4293ae2
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# System.ServiceModel.Channels.ConnectionPoolCloseException
Si è verificata un'eccezione durante la chiusura delle connessioni in questo pool di connessioni.  
  
## Descrizione  
 Questa analisi del livello di errore indica che si è verificato un errore durante la chiusura dei pool di connessioni utilizzati dalla funzionalità di pool di connessioni di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].Una possibile ragione è un chiusura non riuscita di una o più connessioni in pool all'interno di CloseTimeout.Quando viene generata questa eccezione, tutte le connessioni rimanenti non chiuse all'interno di tale pool vengono interrotte; le connessioni non chiuse all'interno di altri pool vengono abbandonate.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)