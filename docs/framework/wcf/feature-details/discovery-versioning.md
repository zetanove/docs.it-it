---
title: "Controllo delle versioni per l&#39;individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Controllo delle versioni per l&#39;individuazione
In questo argomento viene fornita una breve panoramica dell'implementazione di alcune nuove funzionalità di individuazione.  Vengono inoltre forniti cenni preliminari sulla scelta della versione dell'individuazione da usare.  
  
## Controllo delle versioni per l'individuazione  
 La funzionalità di individuazione include il supporto per tre versioni del protocollo WS\_Discovery.  Le interfacce API di individuazione consentono di selezionare la versione del protocollo che si desidera usare.  Questo documento contiene brevi descrizioni sulle impostazioni correlate al controllo delle versioni.  
  
 Le classi di individuazione seguenti dispongo ora di una proprietà <xref:System.ServiceModel.Discovery.DiscoveryVersion> e usano un argomento <xref:System.ServiceModel.Discovery.DiscoveryVersion> nei propri costruttori:  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
### DiscoveryVersion.WSDiscoveryApril2005  
 Se viene fornito <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> come parametro costruttore, l'implementazione utilizzerà la versione April2005 del protocollo WS\-Discovery.  Questa versione corrisponde alla versione pubblicata della specifica del protocollo di WS\-Discovery  e deve essere usata per interoperare con l'applicazione legacy che usa la versione April2005 di WS\-Discovery.  
  
### DiscoveryVersion.WSDiscovery11  
 La versione per l'individuazione predefinita usata dalle interfacce API è <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11>.  Si tratta della versione standardizzata corrente del protocollo di WS\-Discovery.  
  
## DiscoveryVersion.WSDiscoveryCD1  
 Se viene fornito <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1> come parametro costruttore, l'implementazione utilizzerà la versione 1 della bozza del comitato del protocollo WS\-Discovery.  Questa versione del protocollo deve essere usata per interoperare con le implementazioni che eseguono la versione CD1 del protocollo WS\-Discovery.  
  
## Supporto di più endpoint di individuazione UDP per varie versioni per l'individuazione su un solo host del servizio  
 Potrebbe risultare opportuno esporre più endpoint di individuazione UDP per varie versioni per l'individuazione su un solo host del servizio.  A tale scopo è necessario specificare un indirizzo univoco per ogni endpoint di individuazione UDP.  Nell'esempio seguente viene illustrato come effettuare questa operazione.  
  
```  
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);  
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
  
newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");  
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionAril2005");  
  
serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);  
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);  
  
```