---
title: "Esposizione dei dati come servizio (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "guida introduttiva, WCF Data Services"
  - "WCF Data Services, configurazione"
  - "WCF Data Services, guida introduttiva"
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Esposizione dei dati come servizio (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si integra con Visual Studio per consentire di definire con facilità i servizi per l'esposizione dei dati come feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)].  La creazione di un servizio dati che espone un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] implica l'esecuzione dei passaggi di base seguenti:  
  
1.  **Definizione** **del modello di dati**.  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta in modo nativo i modelli di dati basati su [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md).  Per altre informazioni, vedere [Procedura: creare un servizio dati utilizzando un'origine dati ADO.NET Entity Framework](../../../../docs/framework/data/wcf/create-a-data-service-using-an-adonet-ef-data-wcf.md).  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta inoltre i modelli di dati basati su oggetti CLR \(Common Language Runtime\) che restituiscono un'istanza dell'interfaccia <xref:System.Linq.IQueryable%601>.  In questo modo è possibile distribuire servizi dati basati su elenchi, matrici e raccolte di .NET Framework. Per consentire l'esecuzione di operazioni di creazione, aggiornamento ed eliminazione su queste strutture di dati, è inoltre necessario implementare l'interfaccia <xref:System.Data.Services.IUpdatable>.  Per altre informazioni, vedere [Procedura: creare un servizio dati utilizzando il provider di reflection](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md).  
  
     Per gli scenari più avanzati [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include un set di provider che consentono di definire un modello di dati basato su tipi di dati ad associazione tardiva.  Per altre informazioni, vedere [Provider di servizi dati personalizzati](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md).  
  
2.  **Creare il servizio dati.** La maggior parte dei servizi di base espone una classe che eredita dalla classe <xref:System.Data.Services.DataService%601>, con un tipo `T` che corrisponde al nome completo dello spazio dei nomi del contenitore di entità.  Per altre informazioni, vedere [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md).  
  
3.  **Configurazione del servizio dati.**Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] disabilita l'accesso alle risorse esposte da un contenitore di entità. L'interfaccia <xref:System.Data.Services.DataServiceConfiguration> consente di configurare l'accesso a risorse e operazioni del servizi, di specificare la versione supportata di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e di definire altri comportamenti a livello di server, ad esempio i comportamenti di invio in batch o il numero massimo di entità che è possibile restituire in un'unica risposta. Per altre informazioni, vedere [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md).  
  
 Per un esempio relativo alla modalità di creazione di un servizio dati semplice basato sul database Northwind di esempio, vedere [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Vedere anche  
 [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)   
 [Cenni preliminari](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)