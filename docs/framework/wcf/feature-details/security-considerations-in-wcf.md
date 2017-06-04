---
title: "Considerazioni sulla sicurezza in WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sicurezza [WCF]"
  - "WCF, sicurezza"
  - "Windows Communication Foundation, sicurezza"
ms.assetid: 42055ee0-6d0c-443d-9d89-788dfc345d6d
caps.latest.revision: 49
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 49
---
# Considerazioni sulla sicurezza in WCF
Negli argomenti di questa sezione vengono elencati i vari elementi relativi alla protezione che è necessario considerare nella progettazione di un'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## In questa sezione  
 [Diffusione di informazioni](../../../../docs/framework/wcf/feature-details/information-disclosure.md)  
 Illustra le varie modalità in cui è possibile diffondere o lanciare attacchi alle informazioni e come limitare il problema  
  
 [Elevazione dei privilegi](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)  
 Descrive gli effetti causati quando all'autore di un attacco vengono assegnate autorizzazioni che vanno oltre quelle concesse inizialmente e come circoscrivere il problema.  
  
 [Denial of Service \(Negazione del servizio\)](../../../../docs/framework/wcf/feature-details/denial-of-service.md)  
 Descrive ciò che avviene quando un sistema non è in grado di elaborare messaggi in modo appropriato e come limitare il problema.  
  
 [Manomissioni](../../../../docs/framework/wcf/feature-details/tampering.md)  
 Descrive la modifica dei messaggi o del recapito dei messaggi e come limitare il problema.  
  
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)  
 Descrive ciò che avviene quando l'autore dell'attacco copia un flusso di messaggi tra due parti e lo riproduce verso una o più delle parti e spiega come limitare il problema.  
  
 [Considerazioni sulla protezione per le sessioni protette](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md)  
 Descrive gli elementi seguenti che influiscono sulla protezione durante l'implementazione di sessioni protette.  
  
 [Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)  
 Elenca i diversi scenari che non supportano un particolare aspetto della protezione e che devono essere evitati o presi in considerazione.  
  
## Riferimenti  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel>  
  
## Sezioni correlate  
 [Indicazioni di sicurezza e procedure consigliate](../../../../docs/framework/wcf/feature-details/security-guidance-and-best-practices.md)  
  
## Vedere anche  
 [Sicurezza](../../../../docs/framework/wcf/feature-details/security.md)