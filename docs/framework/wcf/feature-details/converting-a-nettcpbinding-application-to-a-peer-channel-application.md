---
title: "Conversione di un&#39;applicazione NetTcpBinding in un&#39;applicazione del canale peer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d4137292-a923-4b8f-8594-42276f2d3ce2
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Conversione di un&#39;applicazione NetTcpBinding in un&#39;applicazione del canale peer
È possibile creare connessioni tra i client con [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] usando associazioni che descrivono i parametri della connessione.  La conversione di un'applicazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per l'uso di connessioni peer\-to\-peer richiede un'associazione che supporti questa tecnologia quando si creano le connessioni client.  Il canale peer fornisce un'associazione denominata <xref:System.ServiceModel.NetPeerTcpBinding>utilizzabile in modo analogo a <xref:System.ServiceModel.NetTcpBinding>.  Le differenze principali includono la specifica di un servizio resolver e la definizione di impostazioni di sicurezza.  
  
 Se per un'applicazione si usano il resolver e le impostazioni di sicurezza predefinite, la conversione di un'applicazione client\/server normale per l'uso del canale peer comporta la modifica del nome dell'associazione da "NetTcpBinding" a "NetPeerTcpBinding" nel file di configurazione dell'applicazione. Non è necessario modificare la codebase dell'applicazione.  
  
## Vedere anche  
 [Creazione di un'applicazione del canale peer](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)   
 [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md)