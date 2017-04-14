---
title: "System.ServiceModel.Channels.PeerMaintainerActivity | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef28d086-d7fb-4e81-82e9-45a54647783b
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# System.ServiceModel.Channels.PeerMaintainerActivity
Il modulo PeerMaintainer sta eseguendo un'operazione specifica \(i dettagli sono contenuti nel corpo del messaggio di traccia\).  
  
## Descrizione  
 Questa traccia si verifica durante varie operazioni PeerMaintainer.  
  
 PeerMaintainer è un componente interno di PeerNode.  Ogni minuto o ogni 32 messaggi ricevuti, invia un messaggio LinkUtility ai router adiacenti con le statistiche sulla quantità di messaggi scambiati e su quanti di essi sono utili \(non duplicati, non manomessi\).  Ciò consente di determinare l'utilità di collegamento di un determinato router adiacente.  Ogni cinque minuti circa, il componente Maintener verifica l'integrità delle connessioni al router adiacente.  Se il numero di connessioni al router adiacente supera il valore ideale, il componente elimina le connessioni meno utili.  Se il numero di connessioni non è sufficiente, il componente ne acquisisce di nuove.  
  
## Vedere anche  
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)