---
title: "Pubblicazione di metadati | Microsoft Docs"
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
  - "metadati [WCF], pubblicazione"
ms.assetid: 3a56831a-cabc-45c0-bd02-12e2e9bd7313
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Pubblicazione di metadati
I servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] pubblicano metadati tramite la pubblicazione di uno o più endpoint dei metadati.La pubblicazione di metadati del servizio rende disponibili i metadati utilizzando protocolli standard, ad esempio le richieste WS\-MetadataExchange \(MEX\) e HTTP\/GET.Gli endpoint dei metadati sono simili ad altri endpoint del servizio per indirizzo, associazione e contratto e possono essere aggiunti a un host del servizio tramite configurazione o codice imperativo.  
  
## Pubblicazione di endpoint dei metadati  
 Per pubblicare endpoint dei metadati per un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è innanzitutto necessario aggiungere al servizio il comportamento del servizio <xref:System.ServiceModel.Description.ServiceMetadataBehavior>.L'aggiunta di un'istanza <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> consente al servizio di esporre gli endpoint dei metadati.Quando viene aggiunto il comportamento del servizio <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName>, è possibile esporre gli endpoint dei metadati che supportano il protocollo MEX o che rispondono alle richieste HTTP\/GET.  
  
 L'oggetto <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> utilizza un oggetto <xref:System.ServiceModel.Description.WsdlExporter> per esportare metadati per tutti gli endpoint del servizio nel servizio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] esportazione di metadati da un servizio, vedere [Esportazione e importazione di metadati](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md).  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> aggiunge un'istanza <xref:System.ServiceModel.Description.ServiceMetadataExtension> come estensione all'host del servizio.<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> fornisce l'implementazione per i metadati che pubblicano protocolli.È inoltre possibile utilizzare <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=fullName> per ottenere i metadati del servizio in fase di esecuzione accedendo alla proprietà <xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A?displayProperty=fullName>.  
  
### Endpoint dei metadati MEX  
 Per aggiungere endpoint dei metadati che utilizzano il protocollo MEX, aggiungere endpoint del servizio all'host del servizio che utilizza il contratto del servizio `IMetadataExchange`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include un'interfaccia <xref:System.ServiceModel.Description.IMetadataExchange> con questo nome di contratto del servizio che è possibile utilizzare come parte del modello di programmazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Gli endpoint WS\-MetadataExchange o MEX, possono utilizzare una delle quattro associazioni predefinite che i metodi factory statici espongono sulla classe <xref:System.ServiceModel.Description.MetadataExchangeBindings> in modo che corrispondano alle associazioni predefinite utilizzate dagli strumenti [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio Svcutil.exe.È inoltre possibile configurare gli endpoint dei metadati MEX utilizzando un'associazione personalizzata.  
  
### Endpoint dei metadati HTTP GET  
 Per aggiungere un endpoint dei metadati al servizio che risponda alle richieste HTTP\/GET, impostare la proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> in <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> su `true`.È inoltre possibile configurare un endpoint dei metadati che utilizza HTTPS impostando la proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> in <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=fullName> su `true`.  
  
## Argomenti della sezione  
 [Procedura: pubblicare metadati per un servizio usando un file di configurazione](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 Illustra come configurare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per pubblicare metadati in modo che i client possano recuperare i metadati utilizzando una richiesta WS\-MetadataExchange o HTTP\/GET tramite la stringa di query `?wsdl`.  
  
 [Procedura: pubblicare metadati per un servizio utilizzando codice](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 Illustra come consentire la pubblicazione di metadati per un servizio nel codice [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in modo che i client possano recuperare i metadati utilizzando una richiesta WS\-MetadataExchange o HTTP\/GET tramite la stringa di query `?wsdl`.  
  
## Riferimenti  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>  
  
 <xref:System.ServiceModel.Description.IMetadataExchange>  
  
 <xref:System.ServiceModel.Description.ServiceMetadataExtension>  
  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings>  
  
## Vedere anche  
 [Esportazione e importazione di metadati](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md)