---
title: "Configurazione dei servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "configurazione [WCF]"
ms.assetid: beac771e-f28e-4f84-9ff1-ad9251c726d3
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Configurazione dei servizi
Dopo aver progettato e implementato il contratto di servizio, è possibile configurare il servizio.  Questa è la fase in cui si definisce e si personalizza il modo in cui il servizio viene esposto ai client, inclusa l'indicazione dell'indirizzo, del trasporto e della codifica dei messaggi usata per inviare e ricevere messaggi e del tipo di sicurezza richiesto.  
  
 La configurazione specificata in questo punto include tutti i modi, imperativo nel codice o mediante un file di configurazione, in cui è possibile definire e personalizzare i vari aspetti di un servizio, ad esempio la specifica degli indirizzi dell'endpoint, dei trasporti usati e degli schemi di sicurezza.  In pratica, la creazione della configurazione è un fattore essenziale della programmazione di applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## In questa sezione  
 [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md)  
 A partire da [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)], [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene fornito con un nuovo modello di configurazione predefinito che semplifica i requisiti di configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Se non si specifica alcuna configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per un determinato servizio, il runtime configura automaticamente il servizio con endpoint, associazioni e comportamenti predefiniti.  
  
 [Configurazione dei servizi tramite file di configurazione](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)  
 Un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] può essere configurato mediante la tecnologia di configurazione [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  In genere, gli elementi XML vengono aggiunti al file Web.config per un sito Internet Information Services \(IIS\) che ospita un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  Gli elementi consentono di modificare i dettagli, ad esempio gli indirizzi dell'endpoint \(gli indirizzi effettivi usati per comunicare con il servizio\) per i singoli computer.  
  
 [Associazioni](../../../docs/framework/wcf/bindings.md)  
 In aggiunta, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] include molte configurazioni comuni fornite dal sistema rappresentate da associazioni che consentono di selezionare rapidamente le funzionalità di base per definire la comunicazione tra un client e il servizio, ad esempio i trasporti, la sicurezza e le codifiche dei messaggi.  
  
 [Endpoint](../../../docs/framework/wcf/endpoints.md)  
 La comunicazione con un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene eseguita interamente tramite gli *endpoint* del servizio.  Gli endpoint contengono il contratto, le informazioni di configurazione specificate nelle associazioni e gli indirizzi che indicano dove si trova il servizio o dove ottenere informazioni sul servizio.  
  
 [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md)  
 Mediante [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e i meccanismi di sicurezza esistenti, è possibile implementare aspetti quali la riservatezza, l'integrità, l'autenticazione e l'autorizzazione in qualsiasi servizio.  È inoltre possibile controllare le attività di sicurezza riuscite e non riuscite.  
  
 [Creazione di servizi interoperativi WS\-I Basic Profile 1.1](../../../docs/framework/wcf/creating-ws-i-basic-profile-1-1-interoperable-services.md)  
 I requisiti per la distribuzione di un servizio che sia interoperativo con i servizi e i client su qualsiasi altra piattaforma o sistema operativo sono delineati nella specifica WS\-I Basic Profile 1.1.  
  
## Riferimenti  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Description>  
  
## Sezioni correlate  
 [Ciclo di vita della programmazione di base](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
 [Progettazione e implementazione di servizi](../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
 [Servizi host](../../../docs/framework/wcf/hosting-services.md)  
  
 [Creazione di client](../../../docs/framework/wcf/building-clients.md)  
  
 [Introduzione all'estendibilità](../../../docs/framework/wcf/introduction-to-extensibility.md)  
  
 [Amministrazione e diagnostica](../../../docs/framework/wcf/diagnostics/index.md)  
  
## Vedere anche  
 [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Panoramica dei concetti](../../../docs/framework/wcf/conceptual-overview.md)   
 [Dettagli delle funzioni di WCF](../../../docs/framework/wcf/feature-details/index.md)