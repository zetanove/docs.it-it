---
title: "Host in Internet Information Services | Microsoft Docs"
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
  - "servizi host [WCF], IIS"
ms.assetid: ddae14e8-143c-442d-b660-2046809b2d43
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Host in Internet Information Services
È possibile ospitare servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] all'interno di un'applicazione Internet Information Services \(IIS\).  Questo modello host è simile al modello usato da [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e dai servizi Web ASMX.  
  
## Versioni di IIS  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere ospitato nelle versioni seguenti di IIS sui sistemi operativi seguenti:  
  
-   IIS 5.1 su [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)].  Questo ambiente è utile per la progettazione e lo sviluppo di applicazioni ospitate da IIS, successivamente distribuite in un sistema operativo server quale [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)].  
  
-   [!INCLUDE[iis601](../../../../includes/iis601-md.md)] su [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)].  [!INCLUDE[iis601](../../../../includes/iis601-md.md)] prevede un modello di processo avanzato che offre un migliore livello di scalabilità, affidabilità e isolamento dell'applicazione.  Questo ambiente è adatto per la distribuzione di produzione di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usano esclusivamente la comunicazione HTTP.  
  
-   IIS 7.0 su [!INCLUDE[wv](../../../../includes/wv-md.md)] e [!INCLUDE[lserver](../../../../includes/lserver-md.md)].  IIS 7.0 offre lo stesso modello di processo avanzato di [!INCLUDE[iis601](../../../../includes/iis601-md.md)], ma usa il servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\) per consentire l'attivazione e la comunicazione di rete su protocolli diversi da HTTP.  Questo ambiente è adatto per lo sviluppo di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che comunicano su qualsiasi protocollo di rete supportato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(inclusi HTTP, net.tcp, net.pipe e net.msmq\).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] WAS, vedere [Hosting nel servizio di attivazione dei processi di Windows](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md).  
  
-   [Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=196496) usa [!INCLUDE[iisver](../../../../includes/iisver-md.md)] e il servizio Attivazione processo Windows \(WAS, Windows Process Activation Service\) per fornire un ambiente di hosting completo per i servizi NET4 WCF e WF.  Tali vantaggi includono la gestione del ciclo di vita del processo, il riciclo del processo, l'hosting condiviso, una rapida protezione dall'errore, la gestione dell'opzione orfano processo, l'attivazione su richiesta e il monitoraggio dello stato.  Per informazioni dettagliate, vedere [Funzionalità di hosting di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=196494) e [Concetti di hosting di AppFabric](http://go.microsoft.com/fwlink/?LinkId=196495).  
  
## Vantaggi dell'hosting in IIS  
 L'hosting di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in IIS presenta diversi vantaggi:  
  
-   I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS vengono distribuiti e gestiti come qualsiasi altro tipo di applicazione IIS, incluse le applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e ASMX.  
  
-   IIS assicura l'attivazione dei processi, la gestione dello stato e il riciclo delle funzionalità, per aumentare l'affidabilità delle applicazioni ospitate.  
  
-   Come [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] possono sfruttare il modello host condiviso di [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], in cui più applicazioni risiedono in un processo di lavoro comune per migliorare densità e scalabilità del server.  
  
-   I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS usano lo stesso modello di compilazione dinamico di [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)], che semplifica lo sviluppo e la distribuzione di servizi ospitati.  
  
 Quando si decide di ospitare servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in IIS, è importante ricordare che IIS 5.1 e [!INCLUDE[iis601](../../../../includes/iis601-md.md)] si limitano alla sola comunicazione HTTP.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla scelta di un ambiente host, vedere [Servizi host](../../../../docs/framework/wcf/hosting-services.md).  
  
## Distribuzione di un servizio WCF ospitato in IIS  
 Lo sviluppo e la distribuzione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitato in IIS implicano le attività seguenti:  
  
-   Verificare che IIS, ASP.NET, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e il componente di attivazione HTTP di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] siano installati e registrati correttamente.  
  
-   Creare una nuova applicazione IIS o riusare un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] esistente.  
  
-   Creare un file con estensione svc per il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Distribuire l'implementazione del servizio nell'applicazione IIS.  
  
-   Configurare il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Per una descrizione di ognuna di queste attività, vedere [Distribuzione di un servizio WCF ospitato in Internet Information Services \(IIS\)](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md).  
  
## Servizi WCF e ASP.NET  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono essere ospitati come affiancati a [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] o in modalità di compatibilità [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], in cui i servizi possono sfruttare appieno le funzionalità fornite dalla piattaforma dell'applicazione Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  Per una discussione su queste funzionalità, vedere [Servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).  
  
## Vedere anche  
 [Estensione dell'hosting tramite ServiceHostFactory](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)   
 [Distribuzione di un servizio WCF ospitato in Internet Information Services \(IIS\)](../../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md)   
 [Servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)   
 [Procedure consigliate per l'hosting in Internet Information Services \(IIS\)](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)   
 [Configurazione di Internet Information Services 7.0 per Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/configuring-iis-for-wcf.md)   
 [Funzionalità di hosting di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)