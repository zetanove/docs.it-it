---
title: "System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8371d0a-843e-440b-b86a-6996db131cb0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded
La velocità di ricezione dei messaggi in ingresso è troppo elevata.  
  
## Descrizione  
 Questa traccia si verifica quando si tenta di elaborare messaggi in ingresso.  Non è possibile inoltrare un messaggio a un elemento adiacente poiché la quota impostata per tale elemento è stata superata.  Questo problema si verifica quando un elemento adiacente che non risponde non riesce a cancellare un backlog di messaggi in sospeso per tale elemento adiacente.  
  
## Risoluzione dei problemi  
 Ridurre la velocità di invio dei messaggi all'interno della rete.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)