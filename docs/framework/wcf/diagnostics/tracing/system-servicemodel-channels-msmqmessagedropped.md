---
title: "System.ServiceModel.Channels.MsmqMessageDropped | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b6e644d-fa68-4be7-abe9-3659671a37c1
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqMessageDropped
MSMQ ha eliminato il messaggio.  
  
## Descrizione  
 La traccia indica che è stato eliminato un messaggio MSMQ.I messaggi MSMQ possono essere eliminati quando [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] \(utilizzato con NetMsmqBinding o MsmqIntegrationBinding\) non è in grado di elaborarli.Tali messaggi vengono definiti messaggi non elaborabili.  
  
 Un messaggio non elaborabile viene eliminato quando la proprietà `ReceiveErrorHandling` su NetMsmqBinding o MsmqIntegrationBinding è impostata su `Drop`.Un messaggio eliminato viene rimosso dalla coda e non è più recuperabile.  
  
 Per ulteriori dettagli su quando i messaggi diventano non elaborabili e su come configurare il servizio per gestire tali messaggi in modo appropriato, vedere la [Poison\-Message Handling](http://go.microsoft.com/fwlink/?LinkID=99546) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [Gestione dei messaggi non elaborabili](http://go.microsoft.com/fwlink/?LinkID=99546)