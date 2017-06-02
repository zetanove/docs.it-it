---
title: "System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d75d39da-7502-4a6a-91b9-eaa05b8e24d5
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed
Impossibile spostare o eliminare il messaggio.  
  
## Descrizione  
 La traccia indica che si è verificato un errore durante il tentativo di spostare, eliminare o rifiutare un messaggio MSMQ.  
  
 I messaggi MSMQ vengono usati da [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] \(in caso di uso con NetMsmqBinding o MsmqIntegrationBinding\). Questa traccia è correlata al valore scelto della proprietà `ReceiveErrorHandling` su NetMsmqBinding o MsmqIntegrationBinding.  
  
 Questa traccia non è indicativa di un errore di sistema complessivo.  Tuttavia, indica che l'eliminazione del messaggio non elaborabile scelta ha avuto esito negativo per un messaggio.  Per altri dettagli sui casi in cui i messaggi diventano non elaborabili e su come configurare il servizio per gestirli nel modo appropriato, vedere [Gestione dei messaggi non elaborabili](http://go.microsoft.com/fwlink/?LinkID=99546).  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)