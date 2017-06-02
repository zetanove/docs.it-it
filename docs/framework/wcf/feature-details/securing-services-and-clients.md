---
title: "Protezione di servizi e client | Microsoft Docs"
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
  - "protezione del messaggio [WCF]"
ms.assetid: e681f3bd-0c09-4a58-b0e4-0ecbdf1aa6c7
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# Protezione di servizi e client
Le informazioni in questa sezione si concentrano sulla programmazione della protezione in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Quest'attività include, in genere, la selezione di un'associazione fornita dal sistema appropriata, l'impostazione delle proprietà dell'elemento di sicurezza e quindi l'impostazione delle proprietà dei comportamenti del servizio che regolano la modalità di recupero delle credenziali che devono essere usate dal servizio o dal client.  Queste tecniche soddisfano i requisiti di sicurezza della maggior parte degli utenti nella maggior parte degli scenari, come illustrato in [Scenari di sicurezza comuni](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md).  Se lo scenario richiede le più funzionalità, vedere innanzitutto [Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md); se non è visibile alcuna soluzione, vedere [Estensione della protezione](../../../../docs/framework/wcf/extending/extending-security.md).  Se si sta creando \(o si sta interoperando con\) un sistema che usa attestazioni dettagliate, vedere gli argomenti in [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md).  
  
## In questa sezione  
 [Programmazione delle funzionalità di sicurezza di WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)  
 Panoramica del modello di programmazione usato per proteggere i messaggi.  
  
 [Panoramica sulla sicurezza del trasporto](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)  
 Panoramica delle modalità di sicurezza dei messaggi tramite il livello di trasporto.  
  
 [Protezione dei messaggi](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)  
 Riepilogo dei motivi per l'uso della protezione a livello di messaggio in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 [Sessioni protette](../../../../docs/framework/wcf/feature-details/secure-sessions.md)  
 Descrizione delle considerazioni necessarie in caso di sicurezza di una sessione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)  
 Spiegazione di alcune delle attività comuni necessarie quando si usano certificati X.509.  
  
## Riferimenti  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Security>  
  
## Sezioni correlate  
 [Concetti sulla protezione](../../../../docs/framework/wcf/feature-details/security-concepts.md)  
  
 [Estensione della protezione](../../../../docs/framework/wcf/extending/extending-security.md)  
  
 [Scenari di sicurezza comuni](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)  
  
 [Associazioni e protezione](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)  
  
 [Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)  
  
 [Estensione della protezione](../../../../docs/framework/wcf/extending/extending-security.md)  
  
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
  
## Vedere anche  
 [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Modello di sicurezza per Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)