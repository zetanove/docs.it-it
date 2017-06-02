---
title: "System.ServiceModel.Channels.PeerNodeAuthenticationFailure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b50f782-ca06-4a82-aa7f-71f78ddc5177
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# System.ServiceModel.Channels.PeerNodeAuthenticationFailure
L’handshake di sicurezza con un router adiacente potenziale non è riuscito.  
  
## Descrizione  
 Questa traccia si verifica quando si tenta di stabilire una connessione protetta con un router adiacente.Tale situazione può verificarsi a causa di credenziali insufficienti o incorrette.  
  
 PeerChannel riconosce un solo tipo di token per identificazione sicura, i certificati X.509 che offrono un modello sicuro di identità basato sul tipo di autenticazione e di autorizzazione che può essere implementato.PeerChannel fornisce inoltre il supporto per applicazioni semplici tramite l'utilizzo di password.Le password possono essere utilizzate solo per consentire l'accesso alla sessione, non per eseguire l'autenticazione dei messaggi.Ciò è dovuto al fatto che è difficile e inappropriato utilizzare per l'autenticazione dell'origine un token simmetrico condiviso da un gruppo di peer.  
  
## Risoluzione dei problemi  
 Assicurarsi che tutti i router adiacenti abbiano le credenziali di sicurezza appropriate.  
  
## Vedere anche  
 [Protezione del canale peer](../../../../../docs/framework/wcf/feature-details/peer-channel-security.md)   
 [Traccia](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [Amministrazione e diagnostica](../../../../../docs/framework/wcf/diagnostics/index.md)