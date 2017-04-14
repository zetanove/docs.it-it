---
title: "Provider di servizi dati (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, provider"
ms.assetid: a0160b1b-3d9c-4cc8-8391-cb0986a60a41
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Provider di servizi dati (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta più modelli di provider per l'esposizione dei dati come feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)].  In questo argomento vengono fornite le informazioni che consentono di scegliere il provider di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] più adatto all'origine dati usata.  
  
## Provider di origini dati  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta i provider riportati di seguito per la definizione del modello di dati di un servizio dati.  
  
|Provider|Descrizione|  
|--------------|-----------------|  
|Provider di Entity Framework|Questo provider usa ADO.NET Entity Framework per consentire l'uso di dati relazionali con un servizio dati mediante la definizione di un modello di dati che esegue il mapping ai dati relazionali.  L'origine dati può essere SQL Server o qualsiasi altra origine dati con supporto di provider di terze parti per Entity Framework.  È necessario usare il provider di Entity Framework quando si dispone di un'origine dati relazionale, ad esempio un database di SQL Server.  Per altre informazioni, vedere [Provider di Entity Framework](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md).|  
|Provider di reflection|Questo provider usa la reflection per consentire la definizione di un modello di dati basato su classi di dati esistenti che possono essere esposte come istanze dell'interfaccia <xref:System.Linq.IQueryable%601>.  Gli aggiornamenti vengono abilitati mediante l'implementazione dell'interfaccia <xref:System.Data.Services.IUpdatable>.  È necessario usare questo provider quando si dispone di classi di dati statiche definite in fase di esecuzione, ad esempio quelle generate da LINQ to SQL o definite da un set di dati tipizzato.  Per altre informazioni, vedere [Provider di reflection](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md).|  
|Provider di servizi dati personalizzati|[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include un set di provider che consentono di definire in modo dinamico un modello di dati basato su tipi di dati ad associazione tardiva.  È necessario implementare queste interfacce quando i dati esposti non sono noti al momento della progettazione dell'applicazione o quando il provider di reflection o il provider di Entity Framework non è sufficiente.  Per altre informazioni, vedere [Provider di servizi dati personalizzati](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md).|  
  
## Altri provider di servizi dati  
 In [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è inoltre disponibile il provider del servizio dati seguente che migliora le prestazioni di un'origine dati definita usando uno degli altri provider.  
  
|Provider|Descrizione|  
|--------------|-----------------|  
|Provider di flusso|Questo provider consente di esporre tipi di dati per oggetti binari di grandi dimensioni tramite [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Un provider di flusso viene creato mediante l'implementazione dell'interfaccia <xref:System.Data.Services.Providers.IDataServiceStreamProvider>.  È possibile implementare questo provider insieme a qualsiasi provider dell'origine dati.  Per altre informazioni, vedere [Provider di flusso](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md).|  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)   
 [Hosting del servizio dati](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)