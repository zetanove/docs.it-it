---
title: "Accesso alle risorse del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "esecuzione di query sul servizio dati [WCF Data Services]"
  - "WCF Data Services, accesso ai dati"
  - "WCF Data Services, guida introduttiva"
  - "WCF Data Services, esecuzione di query"
ms.assetid: 9665ff5b-3e3a-495d-bf83-d531d5d060ed
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Accesso alle risorse del servizio dati (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] per esporre dati come feed con le risorse indirizzabili tramite URI.  Queste risorse sono rappresentate in base alle convenzioni entità\-relazione di [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md).  In questo modello le entità rappresentano unità operative di dati che corrispondono a tipi di dati in un dominio di applicazione, ad esempio clienti, ordini, elementi e prodotti.  L'accesso ai dati di entità e la relativa modifica sono possibili mediante la semantica REST \(Representational State Transfer\), in particolare i verbi GET, PUT, POST e DELETE standard HTTP.  
  
## Indirizzamento di risorse  
 In [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] i dati esposti vengono indirizzati dal modello di dati tramite un URI.  L'URI seguente restituisce ad esempio un feed, ovvero il set di entità Customers, che contiene le voci per tutte le istanze del tipo di entità Customer:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers  
```  
  
 Le entità dispongono di proprietà speciali denominate chiavi di entità.  Una chiave di entità viene usata per identificare in modo univoco una singola entità in un set di entità.  In questo modo è possibile indirizzare un'istanza specifica di un tipo di entità nel set di entità.  L'URI seguente restituisce ad esempio una voce per un'istanza specifica del tipo di entità Customer che presenta un valore chiave corrispondente ad `ALFKI`:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')  
```  
  
 Le proprietà primitive e complesse di un'istanza di entità possono anche essere indirizzate singolarmente.  L'URI seguente restituisce ad esempio un elemento XML che contiene il valore della proprietà `ContactName` per un cliente \(Customer\) specifico:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName  
```  
  
 Se si include l'endpoint `$value` nell'URI precedente, nel messaggio di risposta viene restituito solo il valore della proprietà primitiva.  Nell'esempio seguente viene restituita solo la stringa "Maria Anders" senza l'elemento XML:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName/$value  
```  
  
 Le relazioni tra entità vengono definite mediante associazioni nel modello di dati.  Queste associazioni consentono di indirizzare entità correlate usando le proprietà di navigazione di un'istanza di entità.  Una proprietà di navigazione può restituire una sola entità correlata, nel caso di una relazione molti\-a\-uno, o un set di entità correlate, nel caso di una relazione uno\-a\-molti.  L'URI seguente restituisce ad esempio un feed che corrisponde al set di tutte le entità Order correlate a un cliente specifico:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders  
```  
  
 Le relazioni, che in genere sono bidirezionali, sono rappresentate da una coppia di proprietà di navigazione.  Al contrario della relazione mostrata nell'esempio precedente, l'URI seguente restituisce un riferimento all'entità Customer alla quale appartiene un'entità Order specifica:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Orders(10643)/Customer  
```  
  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] consente inoltre di indirizzare le risorse in base ai risultati di espressioni di query.  In questo modo è possibile filtrare i set di risorse in base a un'espressione valutata.  L'URI seguente consente ad esempio di filtrare le risorse per restituire solo gli ordini per il cliente specificato inviati dal 22 settembre 1997:  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$filter=ShippedDate gt datetime'1997-09-22T00:00:00'  
```  
  
 Per altre informazioni, vedere [OData: Convenzioni URI](http://go.microsoft.com/fwlink/?LinkId=185564).  
  
## Opzioni di query di sistema  
 In [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] viene definito un set di opzioni query del sistema che consentono di eseguire sulle risorse operazioni di query tradizionali quali filtro, ordinamento e paging.  L'URI seguente restituisce ad esempio il set di tutte le entità `Order` insieme alle entità `Order_Detail` correlate, in cui i codici di avviamento postale non terminano con `100`.  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Orders?$filter=not endswith(ShipPostalCode,'100')&$expand=Order_Details&$orderby=ShipCity  
```  
  
 Le voci del feed restituito vengono inoltre ordinate in base al valore della proprietà ShipCity degli ordini.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta le opzioni query del sistema [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] seguenti:  
  
|Opzione query|Descrizione|  
|-------------------|-----------------|  
|`$orderby`|Definisce un tipo di ordinamento predefinito per le entità del feed restituito.  Nella query seguente il feed restituito dei clienti viene ordinato in base al paese e alla città:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Customers?$orderby=Country,City`<br /><br /> Per altre informazioni, vedere la pagina relativa all'[opzione query di sistema OrderBy \($orderby\) in OData](http://go.microsoft.com/fwlink/?LinkId=186968).|  
|`$top`|Specifica il numero di entità da includere nel feed restituito.  Nell'esempio seguente vengono ignorati i primi 10 clienti, quindi vengono restituiti i successivi 10:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10`<br /><br /> Per altre informazioni, vedere [OData: Opzione query del sistema Top \($top\)](http://go.microsoft.com/fwlink/?LinkId=186969).|  
|`$skip`|Specifica il numero di entità da ignorare prima di avviare la restituzione delle entità nel feed.  Nell'esempio seguente vengono ignorati i primi 10 clienti, quindi vengono restituiti i successivi 10:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10`<br /><br /> Per altre informazioni, vedere [OData: Opzione query del sistema Skip \($top\)](http://go.microsoft.com/fwlink/?LinkId=186971).|  
|`$filter`|Definisce un'espressione che filtra le entità restituite nel feed in base a criteri specifici.  Questa opzione query supporta un set di operatori di confronto logici, di operatori aritmetici e di funzioni di query predefinite che consentono di valutare l'espressione di filtro.  Nell'esempio seguente vengono restituiti tutti gli ordini in cui i codici di avviamento postale non terminano con 100:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Orders?$filter=not endswith(ShipPostalCode,'100')`<br /><br /> Per altre informazioni, vedere [OData: Opzione query del sistema Filter \($filter\)](http://go.microsoft.com/fwlink/?LinkId=186972).|  
|`$expand`|Specifica quali entità correlate vengono restituite dalla query.  Le entità correlate vengono incluse come feed o voce inline con l'entità restituita dalla query.  Nell'esempio seguente viene restituito l'ordine per il cliente "ALFKI" insieme ai dettagli relativi agli elementi di ogni ordine:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$expand=Order_Details`<br /><br /> Per altre informazioni, vedere la pagina relativa all'[opzione query di sistema Expand \($expand\) in OData](http://go.microsoft.com/fwlink/?LinkId=186973).|  
|`$select`|Indica che le proprietà dell'entità devono essere restituite nella proiezione.  Per impostazione predefinita, tutte le proprietà di un'entità vengono restituite in un feed.  Nella query seguente vengono restituite solo tre proprietà dell'entità `Customer`:<br /><br /> `http://services.odata.org/Northwind/Northwind.svc/Customers?$select=CustomerID,CompanyName,City`<br /><br /> Per altre informazioni, vedere la pagina relativa all'[opzione query di sistema Select \($select\) in OData](http://go.microsoft.com/fwlink/?LinkID=186076).|  
|`$inlinecount`|Richiede l'inclusione nel feed di un conteggio del numero di entità restituite nel feed stesso.  Per altre informazioni, vedere la pagina relativa all'[opzione query di sistema Inlinecount \($inlinecount\) in OData](http://go.microsoft.com/fwlink/?LinkId=186975).|  
  
## Indirizzamento delle relazioni  
 Oltre all'indirizzamento di set e istanze di entità, [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] consente di indirizzare le associazioni che rappresentano le relazioni tra le entità.  Questa funzionalità è necessaria per creare o modificare una relazione tra due istanze di entità, ad esempio lo spedizioniere correlato a un determinato ordine nel database Northwind di esempio.  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supporta l'operatore `$link` che consente di indirizzare in modo specifico le associazioni tra entità.  L'URI seguente viene ad esempio specificato in un messaggio di richiesta PUT HTTP per modificare lo spedizioniere per l'ordine specificato in un nuovo spedizioniere.  
  
```  
http://services.odata.org/Northwind/Northwind.svc/Orders(10643)/$links/Shipper  
```  
  
 Per altre informazioni, vedere [OData: Indirizzamento di collegamenti tra voci](http://go.microsoft.com/fwlink/?LinkId=187351).  
  
## Utilizzo del feed restituito  
 L'URI di una risorsa [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] consente di indirizzare i dati di entità esposti dal servizio.  Quando si immette un URI nel campo dell'indirizzo di un browser, viene restituita una rappresentazione del feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] della risorsa richiesta.  Per altre informazioni, vedere la [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  Sebbene l'uso di un browser possa risultare utile per verificare che una risorsa del servizio dati restituisca i dati previsti, l'accesso ai servizi dati di produzione che sono inoltre in grado di creare, aggiornare ed eliminare dati viene in genere eseguito tramite linguaggi di codice delle applicazioni o di script in una pagina Web.  Per altre informazioni, vedere [Utilizzo di un servizio dati in un'applicazione client](../../../../docs/framework/data/wcf/using-a-data-service-in-a-client-application-wcf-data-services.md).  
  
## Vedere anche  
 [Sito Web Open Data Protocol](http://go.microsoft.com/fwlink/?LinkID=182204)