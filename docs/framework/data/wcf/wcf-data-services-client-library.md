---
title: "Libreria client WCF Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "HTML"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "classe DataServiceContext, informazioni sulla classe DataServiceContext"
  - "classe DataServiceQuery, informazioni sulla classe DataServiceQuery"
  - "WCF Data Services, libreria client"
ms.assetid: 21075e50-8917-413e-a8ea-35a0f6e65aa5
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Libreria client WCF Data Services
Un'applicazione può interagire con un servizio dati basato su [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] quando è in grado di inviare una richiesta HTTP e di elaborare il feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] restituito da un servizio dati. Questa interoperabilità consente di accedere ai servizi basati su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] da un'ampia gamma di applicazioni Web.  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include librerie client che forniscono un'esperienza di programmazione avanzata quando usano i feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] da .NET Framework o da applicazioni basate su Silverlight.  
  
 Le due classi principali della libreria client sono <xref:System.Data.Services.Client.DataServiceContext> e <xref:System.Data.Services.Client.DataServiceQuery%601>.  La classe <xref:System.Data.Services.Client.DataServiceContext> incapsula operazioni supportate su un servizio dati specificato.  Sebbene i servizi [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] siano senza stato, non lo è il contesto.  È pertanto possibile usare la classe <xref:System.Data.Services.Client.DataServiceContext> per mantenere lo stato nel client tra le interazioni con il servizio dati in modo da supportare funzionalità quali la gestione dei cambiamenti.  Questa classe consente inoltre di gestire le identità e di rilevare le modifiche.  La classe <xref:System.Data.Services.Client.DataServiceQuery%601> rappresenta una query su un set di entità specifico.  
  
 Questa sezione descrive come usare le librerie client per accedere ai dati di un'applicazione client .NET Framework e modificarli.  Per altre informazioni sull'utilizzo della libreria client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] con un'applicazione basata su Silverlight, vedere [WCF Data Services \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkId=186016).  Altre librerie client sono disponibili per consentire l'uso di un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] in altri tipi di applicazione.  Per altre informazioni, vedere la pagina relativa a [OData SDK](http://go.microsoft.com/fwlink/?LinkID=185796).  
  
## In questa sezione  
 [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)  
 Viene descritto come generare una libreria client e classi del servizio dati client basate su feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
 [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
 Viene descritto come eseguire una query su un servizio dati da un'applicazione basata su Framework .NET usando le librerie client.  
  
 [Caricamento di contenuto posticipato](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)  
 Viene descritto come caricare contenuto aggiuntivo non incluso nella risposta alla query iniziale.  
  
 [Aggiornamento del servizio dati](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)  
 Viene descritto come creare, modificare ed eliminare entità e relazioni usando le librerie client.  
  
 [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)  
 Vengono descritte le funzionalità fornite dalle librerie client per l'uso di un servizio dati in modo asincrono.  
  
 [Invio in batch di operazioni](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)  
 Viene descritto come inviare più richieste al servizio dati in un unico batch usando le librerie client.  
  
 [Associazione di dati a controlli](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)  
 Viene descritto come associare controlli a un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] restituito da un servizio dati.  
  
 [Operazioni del servizio di chiamata](../../../../docs/framework/data/wcf/calling-service-operations-wcf-data-services.md)  
 Viene descritto come usare la libreria client per chiamare le operazioni del servizio.  
  
 [Gestione del contesto del servizio dati](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)  
 Vengono descritte le opzioni per la gestione del comportamento della libreria client.  
  
 [Utilizzo di dati binari](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)  
 Viene descritto come accedere e apportare modifiche ai dati binari restituiti dal servizio dati come flusso di dati.  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)