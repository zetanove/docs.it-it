---
title: "System.ServiceModel.Channels.MsmqPoisonMessageRejected | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e64b9bd-1f12-43df-a189-d7be3c2bace1
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.MsmqPoisonMessageRejected
Messaggio non elaborabile rifiutato.  
  
## Descrizione  
 La traccia indica che è stato rilevato e successivamente rifiutato un messaggio non elaborabile.Ciò accade quando la proprietà `ReceiveErrorHandling` su NetMsmqBinding o MsmqIntegrationBinding è impostata su `Reject`.Un messaggio rifiutato viene recapitato nuovamente alla [coda di messaggi non recapitabili](http://go.microsoft.com/fwlink/?LinkId=99544) del mittente.  
  
 Per ulteriori dettagli su quando i messaggi diventano non elaborabili e su come configurare il servizio per gestire tali messaggi in modo appropriato, vedere [Gestione dei messaggi non elaborabili](http://go.microsoft.com/fwlink/?LinkId=99546).Per ulteriori dettagli su cosa significa un messaggio rifiutato in MSMQ, vedere la pagina [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkId=99548) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [Gestione dei messaggi non elaborabili](http://go.microsoft.com/fwlink/?LinkId=99546)   
 [MQMarkMessageRejected](http://go.microsoft.com/fwlink/?LinkId=99548)