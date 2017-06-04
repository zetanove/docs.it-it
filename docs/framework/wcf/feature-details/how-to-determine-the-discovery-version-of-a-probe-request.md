---
title: "Procedura: determinare la versione di individuazione di una richiesta del probe | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3c4e2e2-2957-4074-ae6a-776a5ca84278
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: determinare la versione di individuazione di una richiesta del probe
È possibile che un proxy di individuazione esponga più endpoint di individuazione usando versioni di individuazione diverse.  Quando una richiesta del probe multicast UDP arriva al proxy, il proxy deve rispondere con un messaggio di soppressione multicast.  Per eseguire questa operazione è necessario che conosca la versione di individuazione della richiesta.  
  
### Per determinare la versione di individuazione di una richiesta del probe  
  
1.  Nel metodo che risponde a una richiesta del probe \(ad esempio <xref:System.ServiceModel.Discovery.DiscoveryProxy.OnBeginFind%2A>\) usare la proprietà statica <xref:System.ServiceModel.OperationContext.Current%2A> per cercare un elemento <xref:System.ServiceModel.Discovery.DiscoveryOperationContextExtension> come mostrato nel codice seguente.  
  
    ```  
    DiscoveryOperationContextExtension doce = OperationContext.Current.Extensions.Find<DiscoveryOperationContextExtension>();  
    // Access the discovery version from the DiscoveryOperationContextExtension  
    doce.DiscoveryVersion;  
  
    ```  
  
## Vedere anche  
 <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion%2A>   
 [Implementazione di un proxy di individuazione](../../../../docs/framework/wcf/feature-details/implementing-a-discovery-proxy.md)   
 [Esempio relativo al proxy di individuazione](../../../../docs/framework/wcf/samples/discovery-proxy-sample.md)