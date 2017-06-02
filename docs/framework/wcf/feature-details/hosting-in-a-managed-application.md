---
title: "Hosting in un&#39;applicazione gestita | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: af70132d-e9e1-4f32-b20f-f0014629758a
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Hosting in un&#39;applicazione gestita
I servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono essere ospitati in qualsiasi applicazione [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Il self\-hosting dei servizi è l'opzione di hosting più flessibile, poiché richiede la distribuzione di un'infrastruttura minima. Si tratta però dell'opzione meno solida, poiché le applicazioni gestite non forniscono le avanzate funzionalità di gestione e hosting di altre opzioni di hosting disponibili in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], quali Internet Information Services \(IIS\) e i servizi di Windows.  
  
 Per creare un servizio indipendente, creare e aprire un'istanza di <xref:System.ServiceModel.ServiceHost>, che avvia un servizio di ascolto di messaggi.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md).  
  
 Per un esempio completo di come definire un contratto, implementarlo e ospitare un servizio all'interno di un'applicazione gestita, vedere [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md) e [Servizio indipendente](../../../../docs/framework/wcf/samples/self-host.md).  
  
 Nelle sezioni seguenti vengono descritti scenari comuni di utilizzo di questa opzione di hosting.  
  
## Applicazioni console  
 Tra gli scenari comuni di self\-hosting ci sono i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in esecuzione in applicazioni console. L'hosting di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] all'interno di un'applicazione console è in genere utile durante la fase di sviluppo del servizio. Agevola infatti il debug, l'ottenimento di informazioni di traccia per scoprire cosa accadde all'interno dell'applicazione e lo spostamento copiandole in nuove posizioni.  
  
## Applicazioni rich client  
 Altri scenari comuni di self\-hosting sono rappresentati dalle applicazioni rich client, quali quelle basate su [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] o Windows Form \(WinForm\). Questa opzione di hosting consente inoltre ad applicazioni rich client, quali quelle [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] e Windows Form, di comunicare più facilmente con l'esterno. Ne è un esempio un client di collaborazione peer\-to\-peer che utilizza [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] per l'interfaccia utente e che ospita anche un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che consente ad altri client di connettersi ad esso per condividere informazioni.  
  
## Vedere anche  
 [Servizi host](../../../../docs/framework/wcf/hosting-services.md)   
 [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md)