---
title: "Conversazioni e sessioni protette | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48cb104a-532d-40ae-aa57-769dae103fda
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# Conversazioni e sessioni protette
Una funzionalità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è la possibilità di stabilire sessioni protette tra due endpoint che si autenticano a vicenda e si accordano su un processo di crittografia e di firma digitale.L'endpoint del servizio potrebbe, ad esempio, richiedere a un endpoint client di inviare un token di sicurezza basato su un certificato X.509 per l'autenticazione.Dopo che il client è stato autenticato, l'endpoint del servizio restituisce un token del contesto di sicurezza \(SCT\) al client che viene quindi utilizzato per proteggere tutti i messaggi successivi all'interno della sessione.La creazione di questa sessione protetta consente al set di messaggi scambiati tra due endpoint di essere più efficienti, poiché SCT ha una chiave simmetrica.Le chiavi asimmetriche, sulle quali sono basati i certificati X.509, richiedono una potenza di calcolo notevolmente maggiore rispetto alle chiavi simmetriche per generare una firma digitale o la crittografia di un set di dati.  
  
 Il criterio bootstrap \(definito nella sezione 6.2.7 dello standard [WS\-SecurityPolicy](http://go.microsoft.com/fwlink/?LinkId=99817) \- la pagina potrebbe contenere informazioni in lingua inglese\) contiene le asserzioni di sicurezza del messaggio utilizzate per proteggere il canale e autenticare il client prima dello scambio tra RST\/SCT e RSTR\/SCT.Alcune associazioni standard di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dispongono di una proprietà `Security.Message.EstablishSecurityContext` che controlla l'utilizzo delle conversazioni protette.Quando si utilizzano le associazioni personalizzate, il bootstrap viene indicato annidando gli elementi di associazione di sicurezza tramite [\<bootstrapConversazioneProtetta\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) nel file di configurazione o chiamando <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A> in codice.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sessioni, vedere [Uso di sessioni](../../../../docs/framework/wcf/using-sessions.md).  
  
## Vedere anche  
 [Sessioni, istanze e concorrenza](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)   
 [Procedura: creare un servizio che richiede sessioni](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)