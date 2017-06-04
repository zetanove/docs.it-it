---
title: "Pubblicazione di endpoint dei metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 29cd8a60-dfb7-460c-bf5a-c2b31b782671
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Pubblicazione di endpoint dei metadati
I servizi [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] pubblicano metadati tramite la pubblicazione di uno o più endpoint dei metadati.La pubblicazione di metadati del servizio rende disponibili i metadati utilizzando protocolli standard, ad esempio le richieste WS\-MetadataExchange \(MEX\) e HTTP\/GET.Gli endpoint dei metadati sono simili ad altri endpoint del servizio per indirizzo, associazione e contratto e possono essere aggiunti a un host del servizio tramite configurazione o codice.Per consentire la pubblicazione di endpoint dei metadati, è necessario aggiungere al servizio il comportamento del servizio <xref:System.ServiceModel.Description.ServiceMetadataBehavior>.  
  
## Argomenti della sezione  
 [Procedura: pubblicare metadati per un servizio usando un file di configurazione](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 Illustra come configurare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per pubblicare metadati in modo che i client possano recuperare i metadati utilizzando una richiesta WS\-MetadataExchange o HTTP\/GET tramite la stringa di query `?wsdl`.  
  
 [Procedura: pubblicare metadati per un servizio utilizzando codice](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 Illustra come consentire la pubblicazione di metadati per un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] nel codice, in modo che i client possano recuperare i metadati utilizzando una richiesta WS\-MetadataExchange o HTTP\/GET tramite la stringa di query `?wsdl`.  
  
## Vedere anche  
 [Pubblicazione di metadati](../../../docs/framework/wcf/feature-details/publishing-metadata.md)