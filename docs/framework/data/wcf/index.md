---
title: "WCF Data Services 4.5 | Microsoft Docs"
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
  - "Astoria"
  - "WCF Data Services, introduzione"
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# WCF Data Services 4.5
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], noto in precedenza come "ADO.NET Data Services", è un componente di .NET Framework che consente di creare servizi che usano [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] per esporre e usare dati sul Web o su una rete Intranet tramite la semantica [REST \(Representational State Transfer\)](http://go.microsoft.com/fwlink/?LinkId=113919). [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] espone dati come risorse indirizzabili da URI.  L'accesso ai dati e la relativa modifica vengono eseguiti tramite verbi HTTP standard di GET, PUT, POST e DELETE. Per esporre risorse come set di entità correlate da associazioni, in [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] vengono usate le convenzioni entità\-relazione di [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md).  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] usa il protocollo [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] per l'indirizzamento e l'aggiornamento delle risorse.  In questo modo, è possibile accedere ai servizi da qualsiasi client che supporti [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] consente di richiedere e scrivere dati nelle risorse usando formati di trasferimento noti, ovvero Atom, un set di standard per lo scambio e l'aggiornamento di dati come XML, e JSON \(JavaScript Object Notation\), un formato per lo scambio di dati basati su testo ampiamente usato nelle applicazioni AJAX.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di esporre i dati che hanno origine da vari scenari come feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  Gli strumenti di Visual Studio semplificano la creazione di un servizio basato su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] tramite un modello di dati di ADO.NET Entity Framework. È inoltre possibile creare feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] basati sulle classi CLR \(Common Language Runtime\), nonché dati ad associazione tardiva o senza tipo.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include inoltre un set di librerie client: una per le applicazioni client .NET Framework in generale e un'altra specifica per le applicazioni basate su Silverlight.  Queste librerie client forniscono un modello di programmazione basato su oggetti per l'accesso a un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] da ambienti quali .NET Framework e Silverlight.  
  
## Da dove iniziare  
 A seconda degli argomenti di maggiore interesse, si consiglia di iniziare a usare [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] in uno degli argomenti seguenti.  
  
 Passare subito a...  
 -   [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)  
  
-   [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)  
  
-   [Guida rapida di Silverlight](http://go.microsoft.com/fwlink/?LinkID=192782)  
  
-   [Guida rapida di Silverlight per lo sviluppo di Windows Phone](http://go.microsoft.com/fwlink/?LinkID=214535)  
  
 Codice di esempio...  
 -   [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)  
  
-   [Procedura: eseguire query sul servizio dati](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
-   [Procedura: associare dati a elementi Windows Presentation Foundation](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)  
  
 Ulteriori informazioni su [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]  
 -   [Whitepaper: Introduzione a OData](http://go.microsoft.com/fwlink/?LinkId=220867)  
  
-   [Sito Web Open Data Protocol](http://go.microsoft.com/fwlink/?LinkID=184554)  
  
-   [OData: SDK](http://go.microsoft.com/fwlink/?LinkID=185248)  
  
-   [OData: Domande frequenti](http://go.microsoft.com/fwlink/?LinkId=185867)  
  
 Vedere alcuni video...  
 -   [Guida per i principianti di WCF Data Services](http://go.microsoft.com/fwlink/?LinkId=220864)  
  
-   [Video per sviluppatori di WCF Data Services](http://go.microsoft.com/fwlink/?LinkId=220861)  
  
-   [OData: Sito Web degli sviluppatori](http://go.microsoft.com/fwlink/?LinkId=185866)  
  
 Vedere esempi end\-to\-end  
 -   [Esempi di documentazione di WCF Data Services nella raccolta di esempi MSDN](http://go.microsoft.com/fwlink/?LinkID=220865)  
  
-   [Altri esempi di WCF Data Services nella raccolta di esempi MSDN](http://go.microsoft.com/fwlink/?LinkId=220866)  
  
-   [OData: SDK](http://go.microsoft.com/fwlink/?LinkID=185248)  
  
 Integrazione con Visual Studio  
 -   [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)  
  
-   [Creazione del servizio dati](../../../../docs/framework/data/wcf/creating-the-data-service.md)  
  
-   [Provider di Entity Framework](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)  
  
 Attività possibili  
 -   [Cenni preliminari](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)  
  
-   [Whitepaper: Introduzione a OData](http://go.microsoft.com/fwlink/?LinkId=220867)  
  
-   [Scenari delle applicazioni](../../../../docs/framework/data/wcf/application-scenarios-wcf-data-services.md)  
  
 Uso di Silverlight  
 -   [Guida rapida di Silverlight](http://go.microsoft.com/fwlink/?LinkID=192782)  
  
-   [WCF Data Services \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkID=143149)  
  
-   [Guida introduttiva a Silverlight](http://go.microsoft.com/fwlink/?LinkId=148366)  
  
 Creazione di un'applicazione Windows Phone  
 -   [Guida rapida di Silverlight per lo sviluppo di Windows Phone](http://go.microsoft.com/fwlink/?LinkID=214535)  
  
-   [Client OData \(Open Data Protocol\) per Windows Phone](http://go.microsoft.com/fwlink/?LinkID=208749)  
  
 Uso di LINQ...  
 -   [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
  
-   [Considerazioni su LINQ](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md)  
  
-   [Procedura: eseguire query sul servizio dati](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
 Ulteriori informazioni  
 -   [Blog del team di WCF Data Services](http://go.microsoft.com/fwlink/?LinkID=150511)  
  
-   [Risorse](../../../../docs/framework/data/wcf/wcf-data-services-resources.md)  
  
-   [Centro per sviluppatori di WCF Data Services](http://go.microsoft.com/fwlink/?LinkId=220868)  
  
-   [Sito Web Open Data Protocol](http://go.microsoft.com/fwlink/?LinkID=184554)  
  
## Contenuto della sezione  
 [Cenni preliminari](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)  
 Viene fornita una panoramica delle caratteristiche e delle funzionalità introdotte in [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  
  
 [What's New in WCF Data Services](http://msdn.microsoft.com/it-it/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)  
 Vengono descritti le nuove funzionalità [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] e il supporto delle nuove caratteristiche di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
 [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)  
 Viene illustrato come esporre e usare feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] tramite [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  
  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)  
 Viene illustrato come creare e configurare un servizio dati che espone feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)  
 Viene descritto come servirsi delle librerie client per usare i feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] di un'applicazione client .NET Framework.  
  
## Vedere anche  
 [Representational State Transfer \(REST\)](http://go.microsoft.com/fwlink/?LinkId=113919)