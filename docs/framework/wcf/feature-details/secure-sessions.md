---
title: "Sessioni protette | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b50602f-d7b5-42e9-8e92-1f0413df0d8b
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Sessioni protette
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] offre sessioni affidabili in grado di garantire che i messaggi vengano ricevuti nell'ordine in cui sono stati inviati.Negli argomenti di questa sezione vengono descritte le implicazioni di sicurezza da tenere presenti quando si crea una sessione affidabile.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sessioni affidabili, vedere [Uso di sessioni](../../../../docs/framework/wcf/using-sessions.md).  
  
> [!NOTE]
>  Quando la rappresentazione è obbligatoria in Windows XP, utilizzare una sessione protetta priva di token del contesto di sicurezza \(SCT, Security Context Token\) con stato.Infatti, quando i token SCT con stato vengono utilizzati con la rappresentazione, il sistema genera un'eccezione <xref:System.InvalidOperationException>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Scenari non supportati](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
## In questa sezione  
  
|||  
|-|-|  
|[Conversazioni e sessioni protette](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)|Il termine "conversazione protetta" è sinonimo di "sessione protetta".In questo argomento viene illustrato il funzionamento di una conversazione protetta nonché i contesti in cui utilizzare tale modello.|  
|[Procedura: creare una sessione protetta](../../../../docs/framework/wcf/feature-details/how-to-create-a-secure-session.md)|Questo argomento descrive i passaggi della procedura di base per creare una sessione protetta.|  
|[Procedura: creare un token di contesto di sicurezza per una sessione sicura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)|Questo argomento descrive i passaggi della procedura per creare una Web farm che interagisce con i client tramite una sessione protetta con stato.|  
|[Considerazioni sulla protezione per le sessioni protette](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md)|Questo argomento contiene considerazioni specifiche sulle sessioni protette.|  
  
## Riferimenti  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
## Sezioni correlate  
 [Sessioni, istanze e concorrenza](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)  
  
 [Progettazione e implementazione di servizi](../../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
## Vedere anche  
 [Procedura: attivare il rilevamento di attacchi di tipo replay dei messaggi](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)   
 [Attacchi di tipo replay](../../../../docs/framework/wcf/feature-details/replay-attacks.md)   
 [Procedura: creare un servizio che richiede sessioni](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)