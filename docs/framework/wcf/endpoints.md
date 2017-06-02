---
title: "Endpoint di Windows Communication Foundation | Microsoft Docs"
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
  - "endpoint [WCF]"
ms.assetid: bd0c310f-dd9f-4081-9be2-3db5909850b6
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Endpoint di Windows Communication Foundation
La comunicazione con un servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] viene eseguita interamente tramite gli *endpoint* del servizio.  Gli endpoint forniscono ai client l'accesso alla funzionalità offerta da un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 Per una panoramica sulla creazione di un endpoint, vedere [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md).  Ogni endpoint contiene:  
  
-   Un indirizzo che indica dove si trova l'endpoint.  
  
-   Un'associazione che specifica in che modo un client può comunicare con l'endpoint.  
  
-   Un contratto che identifica i metodi disponibili.  
  
 Per istruzioni su come specificare queste singole parti di un endpoint, vedere:  
  
-   [Specifica di un indirizzo endpoint](../../../docs/framework/wcf/specifying-an-endpoint-address.md)  
  
-   [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)  
  
-   [Progettazione e implementazione di servizi](../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
## In questa sezione  
 [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md)  
 Viene descritta la struttura di un endpoint e viene illustrato come definire un endpoint nella configurazione e nel codice, nonché come usare gli endpoint, le associazioni e i comportamenti predefiniti forniti dal runtime.  
  
 [Specifica di un indirizzo endpoint](../../../docs/framework/wcf/specifying-an-endpoint-address.md)  
 Viene descritto come si verifica la comunicazione con un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] tramite gli endpoint.  
  
 [Procedura: creare un endpoint di servizio nella configurazione](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)  
 Viene illustrato come creare un endpoint del servizio nella configurazione.  
  
 [Procedura: creare un endpoint del servizio nel codice](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)  
 Viene illustrato come creare un endpoint del servizio nel codice.  
  
 [Pubblicazione di endpoint dei metadati](../../../docs/framework/wcf/publishing-metadata-endpoints.md)  
 Viene illustrato come pubblicare metadati mediante la pubblicazione degli endpoint dei metadati nella configurazione e nel codice.  
  
## Riferimenti  
 <xref:System.ServiceModel.EndpointAddress>  
  
## Sezioni correlate  
 [Ciclo di vita della programmazione di base](../../../docs/framework/wcf/basic-programming-lifecycle.md)