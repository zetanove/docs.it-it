---
title: "System.ServiceModel.Channels.HttpChannelMessageReceiveFailed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9eb311da-fdcc-4dd3-9d85-05b3280dfdda
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
Impossibile ricevere un messaggio tramite canale HTTP.  
  
## Descrizione  
 Questa traccia può essere emessa come avviso o come errore.In entrambi i casi, la traccia viene emessa quando non viene trovato un listener compatibile per una richiesta HTTP in entrata e tale richiesta viene eliminata.Questa situazione può verificarsi in quanto il verbo HTTP della richiesta non è stato riconosciuto da un listener HTTP o perchè nessun listener era in ascolto sull'indirizzo a cui era destinata la richiesta.La traccia viene emessa come avviso nel caso di un servizio indipendente e come errore nel caso di un servizio ospitato in IIS.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)