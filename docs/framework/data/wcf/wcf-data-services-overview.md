---
title: "Cenni preliminari su WCF Data Services | Microsoft Docs"
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
  - "WCF Data Services"
  - "WCF Data Services, informazioni"
ms.assetid: 7924cf94-c9a6-4015-afc9-f5d22b1743bb
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Cenni preliminari su WCF Data Services
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente la creazione e l'uso di servizi dati per il Web o una Intranet tramite [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)].  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] consente di esporre i dati come risorse indirizzabili tramite URI.  Consente di accedere e modificare i dati tramite la semantica di trasferimento dello stato rappresentativo \(REST\), in particolare i verbi HTTP standard GET, PUT, POST e DELETE. In questo argomento viene fornita una panoramica dei modelli e delle procedure definite da [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] nonché le funzionalità fornite da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per usare [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] nelle applicazioni basate su .NET Framework.  
  
## Indirizzare i dati come risorse  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] espone i dati come risorse indirizzabili dagli URI. I percorsi delle risorse sono costruiti sulla base delle convenzioni delle relazioni delle entità di Entity Data Model \(EDM\).  In questo modello le entità rappresentano unità operative di dati in un dominio di applicazione, ad esempio clienti, ordini, elementi e prodotti.  Per altre informazioni, vedere [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md).  
  
 In [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] le risorse di entità vengono indirizzate come set di entità contenenti istanze dei tipi di entità.  L'URI `http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders` restituisce ad esempio tutti gli ordini del servizio dati `Northwind` correlati al cliente con valore `CustomerID` corrispondente a `ALFKI.`  
  
 Le espressioni di query consentono di eseguire operazioni di query tradizionali, quali filtro, ordinamento e paging, sulle risorse.  L'URI `http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$filter=Freight gt 50` filtra ad esempio le risorse in modo da restituire solo gli ordini con un costo di spedizione superiore a 50 dollari.  Per altre informazioni, vedere [Accesso alle risorse del servizio dati](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md).  
  
## Accesso ai dati interoperativo  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] sfrutta i protocolli Internet standard per creare servizi dati che interoperano con le applicazioni che non usano .NET Framework.  La possibilità di usare URI standard per l'indirizzamento di dati consente all'applicazione di accedere ai dati e di modificarli usando la semantica REST \(Representational State Transfer\), in particolare i verbi GET, PUT, POST e DELETE.  In questo modo è possibile accedere a questi servizi da qualsiasi client in grado di analizzare e di accedere ai dati trasmessi su protocolli HTTP standard.  
  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] definisce un set di estensioni del protocollo di pubblicazione Atom \(AtomPub\). Per soddisfare le esigenze di applicazioni e piattaforme client diverse, supporta richieste e risposte HTTP in più formati di dati.  Un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] può rappresentare i dati nei formati Atom e JSON \(JavaScript Object Notation\), nonché come XML semplice.  Sebbene Atom sia il formato predefinito, il formato del feed è specificato nell'intestazione della richiesta HTTP.  Per altre informazioni, vedere [OData: formato Atom](http://go.microsoft.com/fwlink/?LinkID=185794) e [OData: formato JSON](http://go.microsoft.com/fwlink/?LinkID=185795).  
  
 In caso di pubblicazione di dati come feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si basa sulle funzioni Internet esistenti per operazioni come la memorizzazione nella cache e l'autenticazione.  A tale scopo, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si integra con i servizi e le applicazioni di hosting esistenti, ad esempio ASP.NET, Windows Communication Foundation \(WCF\) e Internet Information Services \(IIS\).  
  
## Indipendenza dall'archiviazione  
 Anche se le risorse vengono indirizzate in base a un modello entità\-relazione, in [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] i feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] vengono esposti indipendentemente dall'origine dati sottostante. Dopo che in [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] viene accettata una richiesta HTTP per una risorsa identificata da un URI, la richiesta viene deserializzata e una rappresentazione di tale richiesta viene passata a un provider [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  Questo provider traduce la richiesta in un formato dello specifico dell'origine dati ed esegue la richiesta sull'origine dati sottostante. In [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] viene realizzata l'indipendenza di archiviazione separando il modello concettuale per l'indirizzamento delle risorse previste da [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] dallo schema specifico dell'origine dati sottostante.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] si integra con ADO.NET Entity Framework per consentire la creazione di servizi dati che espongono dati relazionali.  È possibile usare gli strumenti di Entity Data Model per creare un modello di dati contenente risorse indirizzabili come entità e definire contemporaneamente il mapping tra questo modello e le tabelle nel database sottostante.  Per altre informazioni, vedere [Provider di Entity Framework](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md).  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente inoltre di creare servizi dati che espongono strutture di dati che restituiscono un'implementazione dell'interfaccia <xref:System.Linq.IQueryable%601>.  In questo modo è possibile creare servizi dati che espongono dati di tipi di .NET Framework.  Le operazioni di creazione, aggiornamento ed eliminazione sono supportate quando si implementa anche l'interfaccia <xref:System.Data.Services.IUpdatable>.  Per altre informazioni, vedere [Provider di reflection](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md).  
  
 Per un'illustrazione dell'integrazione di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] con questi provider di dati, vedere il diagramma dell'architettura più avanti in questo argomento.  
  
## Logica di business personalizzata  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] semplifica l'aggiunta della logica di business personalizzata a un servizio dati tramite operazioni del servizio e intercettori.  Le operazioni del servizio sono metodi definiti nel server che possono essere indirizzati tramite URI allo stesso modo delle risorse di dati.  Le operazioni del servizio possono inoltre usare la sintassi dell'espressione di query per filtrare, ordinare ed eseguire il paging dei dati restituiti da un'operazione. Ad esempio, l'URI `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$orderby=OrderDate&$top=10&$skip=10` rappresenta una chiamata a un'operazione di servizio denominata `GetOrdersByCity` sul servizio dati Northwind che restituisce ordini per i clienti da Londra, con i risultati di cui è stato eseguito il paging e l'ordinamento per `OrderDate`.  Per altre informazioni, vedere [Operazioni del servizio](../../../../docs/framework/data/wcf/service-operations-wcf-data-services.md).  
  
 Gli intercettori consentono l'integrazione della logica delle applicazioni personalizzata nell'elaborazione dei messaggi di richiesta o di risposta da parte di un servizio dati.  Gli intercettori vengono chiamati quando si verifica un'azione di query, inserimento, aggiornamento o eliminazione nel set di entità specificato.  Un intercettore può modificare i dati, applicare criteri di autorizzazione o anche terminare l'operazione.  I metodi dell'intercettore devono essere registrati in modo esplicito per un determinato set di entità esposto da un servizio dati.  Per altre informazioni, vedere [Intercettori](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md).  
  
## Librerie client  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] definisce un set di modelli uniformi per l'interazione con i servizi dati.  In questo modo viene offerta la possibilità di creare componenti riusabili in base ai servizi, quali librerie lato client che rendono più semplice l'uso dei servizi dati.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include librerie client sia per le applicazioni client basate su .NET Framework che su Silverlight.  Queste librerie client consentono di interagire con i servizi dati usando oggetti di .NET Framework.  Supportano inoltre query basate su oggetto e query LINQ, caricamento di oggetti correlati, rilevamento di modifiche e risoluzione di identità. Per altre informazioni, vedere [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md).  
  
 Oltre alle librerie client [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] incluse in .NET Framework e Silverlight, sono disponibili altre librerie client che consentono di usare un feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] in applicazioni client, quali le applicazioni PHP, AJAX e Java.  Per altre informazioni, vedere la pagina relativa a [OData SDK](http://go.microsoft.com/fwlink/?LinkID=185796).  
  
## Panoramica dell'architettura  
 Nel diagramma seguente vengono illustrati l'architettura di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per l'esposizione dei feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e l'uso di tali feed nelle librerie client con supporto [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]:  
  
 ![Diagramma architettura WCF Data Services](../../../../docs/framework/data/wcf/media/astoriaservicearch.gif "AstoriaServiceArch")  
  
## Vedere anche  
 [WCF Data Services 4.5](../../../../docs/framework/data/wcf/index.md)   
 [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)   
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Accessing a Data Service \(WCF Data Services\)](http://msdn.microsoft.com/it-it/1e54a2b9-2ec6-4002-b8f8-c1d8df37c350)   
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [Representational State Transfer \(REST\)](http://go.microsoft.com/fwlink/?LinkId=113919)