---
title: "System.ServiceModel.Channels.TcpConnectError | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22d93797-072e-405d-a3e0-5c519ddf290b
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# System.ServiceModel.Channels.TcpConnectError
Operazione di connessione TCP non riuscita.  
  
## Descrizione  
 Questa traccia di livello avviso indica un errore durante la connessione ad un endpoint TCP.Ciò può verificarsi se l'endpoint remoto non risponde ad un indirizzo IP e alla relativa porta.Questa traccia può essere ignorata se i successivi tentativi di connessione ad altri indirizzi IP validi \(ad esempio indirizzi IPv4 o IPv6 oppure altri indirizzi IP che rappresentano un nome host dato\) hanno esito positivo.Una eccezione all'interno di questa traccia potrebbe rivelare ulteriori informazioni relative all'errore.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)