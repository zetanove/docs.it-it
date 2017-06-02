---
title: "Implementazione di un proxy di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dda20e79-8df3-438e-a281-69d779d978ec
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Implementazione di un proxy di individuazione
Contenuto della sezione vengono descritti i passaggi necessari per implementare un proxy di individuazione.  Un proxy di individuazione è un servizio autonomo che contiene un repository di servizi.  I client possono eseguire una query su un proxy di individuazione per cercare servizi individuabili noti al proxy.  La modalità di popolamento di un proxy con i servizi dipende dall'implementatore.  Un proxy di individuazione può ad esempio connettersi a un repository del servizio esistente e può rendere individuabili tali informazioni, un amministratore può usare un'interfaccia API di gestione per aggiungere servizi individuabili a un proxy o un proxy di individuazione può usare la funzionalità degli annunci per aggiornare la cache interna.  
  
 L'implementazione WCF fornisce classi di base che consentono di compilare con facilità un proxy.  È possibile usare queste API per compilare un proxy di individuazione sul repository esistente.  
  
 Il proxy di individuazione implementato è simile a qualsiasi altro servizio WCF. È infatti possibile renderlo individuabile e fare in modo che i client ne individuino gli endpoint.  
  
## In questa sezione  
 [Procedura: implementare un proxy di individuazione](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)  
 Descrive come implementare un proxy di individuazione.  
  
 [Procedura: implementare un servizio individuabile che esegue la registrazione al proxy di individuazione](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)  
 Descrive come implementare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] individuabile che esegue la registrazione al proxy di individuazione.  
  
 [Procedura: implementare un'applicazione client che utilizza il proxy di individuazione per cercare un servizio](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)  
 Descrive come implementare un'applicazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usa il proxy di individuazione per cercare un servizio.  
  
 [Procedura: test del proxy di individuazione](../../../../docs/framework/wcf/feature-details/how-to-test-the-discovery-proxy.md)  
 Descrive come testare il codice scritto nei tre argomenti precedenti.  
  
## Vedere anche  
 [WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery.md)   
 [Procedura: aggiungere capacità di individuazione a un client e un servizio WCF a livello di codice](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)