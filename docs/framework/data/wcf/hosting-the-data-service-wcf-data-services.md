---
title: "Hosting del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, configurazione"
  - "WCF Data Services, Windows Communication Foundation"
ms.assetid: b48f42ce-22ce-4f8d-8f0d-f7ddac9125ee
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Hosting del servizio dati (WCF Data Services)
Grazie a [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile creare un servizio che esponga i dati come feed [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)].  Questo servizio dati è definito come una classe che eredita da <xref:System.Data.Services.DataService%601>.  Questa classe fornisce la funzionalità necessaria per elaborare messaggi di richiesta, eseguire aggiornamenti sull'origine dati e generare messaggi di risposta, come richiesto da [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]. Un servizio dati non può tuttavia essere associato a un socket di rete delle richieste HTTP in ingresso ed essere in attesa su di esso.  Per questa funzionalità obbligatoria, il servizio dati si basa su un componente di hosting.  
  
 L'host del servizio dati esegue le attività seguenti per conto del servizio dati:  
  
-   È in attesa delle richieste e le indirizza al servizio dati.  
  
-   Crea un'istanza del servizio dati per ogni richiesta.  
  
-   Richiede che il servizio dati elabori la richiesta in ingresso.  
  
-   Invia la risposta per conto del servizio dati.  
  
 Per semplificare l'hosting di un servizio dati, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] viene progettato per l'integrazione con Windows Communication Foundation \(WCF\).  Il servizio dati fornisce un'implementazione WCF predefinita che funge da host del servizio dati in un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  È pertanto possibile ospitare un servizio dati in uno dei modi seguenti:  
  
-   In un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
-   In un'applicazione gestita che supporta servizi WCF indipendenti.  
  
-   In un altro host del servizio dati personalizzato.  
  
## Hosting di un servizio dati in un'applicazione ASP.NET  
 Quando si usa la finestra di dialogo **Aggiungi nuovo elemento** in Visual Studio per definire un servizio dati in un'applicazione ASP.NET, lo strumento genera due nuovi file nel progetto.  Il primo file presenta un'estensione `.svc` e indica al runtime WCF come creare un'istanza del servizio dati.  Di seguito viene riportato un esempio di questo file per il servizio dati di esempio di Northwind creato al completamento della [guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md):  
  
```  
<%@ ServiceHost Language="C#"   
    Factory="System.Data.Services.DataServiceHostFactory,   
            System.Data.Services, Version=4.0.0.0,   
            Culture=neutral, PublicKeyToken=b77a5c561934e089"   
    Service="NorthwindService.Northwind" %>   
```  
  
 Questa direttiva richiede all'applicazione la creazione dell'host del servizio per la classe di servizi dati denominata tramite la classe <xref:System.Data.Services.DataServiceHostFactory>.  
  
 La pagina code\-behind per il file `.svc` contiene la classe che corrisponde all'implementazione del servizio dati stesso, definita come segue per il servizio dati di esempio di Northwind:  
  
 [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#servicedefinition)]
 [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#servicedefinition)]  
  
 Poiché un servizio dati si comporta come un servizio WCF, si integra con [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e segue il modello di programmazione Web di WCF. Per altre informazioni, vedere [Servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md) e [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md).  
  
## Servizi WCF indipendenti  
 Poiché incorpora un'implementazione WCF, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta il self\-hosting di un servizio dati come servizio WCF.  Un servizio può essere indipendente in tutte le applicazioni [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], quale un'applicazione console.  La classe <xref:System.Data.Services.DataServiceHost>, che eredita da <xref:System.ServiceModel.Web.WebServiceHost>, viene usata per creare un'istanza del servizio dati in un indirizzo specifico.  
  
 Il self\-hosting può essere usato per lo sviluppo e il test in quanto semplifica la distribuzione del servizio e la risoluzione dei relativi problemi.  Questo tipo di hosting non fornisce tuttavia le funzionalità avanzate di gestione e hosting offerte da [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] o da Internet Information Services \(IIS\). Per altre informazioni, vedere [Hosting in un'applicazione gestita](../../../../docs/framework/wcf/feature-details/hosting-in-a-managed-application.md).  
  
## Definizione di un host del servizio dati personalizzato  
 Per i casi in cui l'implementazione dell'host WCF è troppo restrittiva, è anche possibile definire un host personalizzato per un servizio dati.  Qualsiasi classe che implementi l'interfaccia <xref:System.Data.Services.IDataServiceHost> può essere usata come host di rete per un servizio dati.  Un host personalizzato deve implementare l'interfaccia <xref:System.Data.Services.IDataServiceHost> e deve essere in grado di gestire le responsabilità di base seguenti dell'host del servizio dati:  
  
-   Fornire al servizio dati il percorso radice del servizio.  
  
-   Elaborare le informazioni delle intestazioni di richieste e risposte per l'implementazione del membro <xref:System.Data.Services.IDataServiceHost> appropriato.  
  
-   Gestire le eccezioni generate dal servizio dati.  
  
-   Convalidare i parametri contenuti nella stringa di query.  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Esposizione dei dati come servizio](../../../../docs/framework/data/wcf/exposing-your-data-as-a-service-wcf-data-services.md)   
 [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)