---
title: "Utilizzo di azioni per implementare il comportamento lato server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11a372db-7168-498b-80d2-9419ff557ba5
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Utilizzo di azioni per implementare il comportamento lato server
Le azioni OData consentono di implementare un comportamento che agisce su una risorsa recuperata da un servizio OData.  Ad esempio, se si considera come risorsa un filmato digitale, sono diverse le operazioni che è possibile eseguire, ad esempio l'estrazione, la valutazione, l'aggiunta di commenti o l'archiviazione.  Sono tutti esempi di azioni che possono essere implementate da un servizio di WCF Data Services che gestisce i filmati digitali.  Le azioni vengono descritte in una risposta OData che contiene una risorsa in cui l'azione può essere richiamata.  Quando un utente richiede una risorsa che rappresenta un filmato digitale, la risposta restituita da un servizio di WCF Data Services contiene le informazioni sulle azioni disponibili per tale risorsa.  La disponibilità di un'azione può dipendere dallo stato del servizio dati o della risorsa.  Ad esempio, una volta estratto, un filmato digitale non può essere estratto da un altro utente.  I client possono richiamare un'azione semplicemente specificando un URL.  Ad esempio http:\/\/MyServer\/MovieService.svc\/Movies\(6\) identifica un filmato digitale specifico e http:\/\/MyServer\/MovieService.svc\/Movies\(6\)\/Checkout richiama l'azione sul filmato specifico.  Le azioni consentono di esporre il modello di servizio senza esporre il modello di dati.  Continuando con l'esempio del servizio del filmato, è possibile che si desideri consentire a un utente di valutare un filmato ma non di esporre direttamente i dati della valutazione come risorsa.  È possibile implementare un'azione Rate per consentire all'utente di valutare un filmato ma non di accedere direttamente ai dati della valutazione come risorsa.  
  
 Per un esempio completo dell'implementazione un'azione di WCF Data Services, vedere [Provider di azioni di WCF Data Services per Entity Framework](http://efactionprovider.codeplex.com/)  
  
## Implementazione di un'azione  
 Per implementare un'azione di servizio, è necessario implementare le interfacce <xref:System.IServiceProvider>, <xref:System.Data.Services.Providers.IDataServiceActionProvider> e <xref:System.Data.Services.Providers.IDataServiceInvokable>.  <xref:System.IServiceProvider> consente a WCF Data Services di ottenere l'implementazione di <xref:System.Data.Services.Providers.IDataServiceActionProvider>.  <xref:System.Data.Services.Providers.IDataServiceActionProvider> consente a WCF Data Services di creare, trovare, descrivere e richiamare le azioni di servizio.  <xref:System.Data.Services.Providers.IDataServiceInvokable> consente di richiamare il codice che implementa il comportamento delle azioni di servizio e di ottenere i risultati, se disponibili.  Tenere presente che WCF Data Services contiene servizi WCF "per chiamata", ovvero ogni volta che viene chiamato il servizio, verrà creata una nuova istanza del servizio.  Assicurarsi che non vengano eseguite operazioni non necessarie quando viene creato il servizio.  
  
### IServiceProvider  
 <xref:System.IServiceProvider> contiene un metodo denominato <xref:System.IServiceProvider.GetService%2A>.  Questo metodo viene chiamato da WCF Data Services per recuperare diversi provider di servizi, tra cui provider di servizi di metadati e provider di azioni di servizio dati.  Quando viene richiesto un provider di azioni di servizio dati, viene restituita l'implementazione di <xref:System.Data.Services.Providers.IDataServiceActionProvider>.  
  
### IDataServiceActionProvider  
 <xref:System.Data.Services.Providers.IDataServiceActionProvider> contiene i metodi che consentono di recuperare le informazioni sulle azioni disponibili.  Quando si implementa <xref:System.Data.Services.Providers.IDataServiceActionProvider>, ai metadati del servizio definito dall'implementazione del servizio di <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> vengono aggiunte le azioni. Viene inoltre gestita la distribuzione a tali azioni, se necessario.  
  
#### AdvertiseServiceAction  
 <xref:System.Data.Services.Providers.IDataServiceActionProvider.AdvertiseServiceAction%2A> viene chiamato per determinare le azioni disponibili per la risorsa specificata.  Questo metodo viene chiamato solo per le azioni che non sono sempre disponibili.  Viene usato per verificare se l'azione deve essere inclusa nella risposta OData in base allo stato della risorsa richiesta o allo stato del servizio.  La modalità con cui viene eseguita tale verifica viene scelta dall'utente.  Se calcolare la disponibilità richiede tempo e la risorsa corrente è presente in un feed, è possibile ignorare la verifica e annunciare l'azione.  Il parametro `inFeed` viene impostato su `true` se la risorsa corrente da restituire fa parte di un feed.  
  
#### CreateInvokable  
 [M:System.Data.Services.Providers.IDataServiceActionProvider.CreateInvokable\(System.Data.Services.DataServiceOperationContext,System.Data.Services.Providers.ServiceAction,System.Object\<xref:System.Data.Services.Providers.IDataServiceActionProvider.CreateInvokable%2A> viene chiamato per creare un oggetto <xref:System.Data.Services.Providers.IDataServiceInvokable> che contiene un delegato che incapsula il codice che implementa il comportamento dell'azione.  Questo metodo crea l'istanza di <xref:System.Data.Services.Providers.IDataServiceInvokable> ma non richiama l'azione.  Le azioni di WCF Data Services hanno effetti collaterali e devono essere usate insieme al provider di aggiornamento per salvare le modifiche su disco.  Il metodo <xref:System.Data.Services.Providers.IDataServiceInvokable.Invoke%2A> viene chiamato dal metodo SaveChanges\(\) del provider di aggiornamento.  
  
#### GetServiceActions  
 Questo metodo restituisce una raccolta di istanze di <xref:System.Data.Services.Providers.ServiceAction> che rappresentano tutte le azioni esposte da un servizio di WCF Data Services.  <xref:System.Data.Services.Providers.ServiceAction> è la rappresentazione dei metadati di un'azione che include informazioni quali il nome dell'azione, i relativi parametri e il relativo tipo restituito.  
  
#### GetServiceActionsByBindingParameterType  
 Questo metodo restituisce una raccolta di tutte le istanze di <xref:System.Data.Services.Providers.ServiceAction> che possono essere associate al tipo di parametro di associazione specificato.  In altre parole, tutti gli oggetti <xref:System.Data.Services.Providers.ServiceAction> che possono agire sul tipo di risorsa specificato, detto anche tipo di parametro di associazione. Viene usato quando il servizio restituisce una risorsa per includere le informazioni sulle azioni che possono essere richiamate sulla risorsa.  Questo metodo deve restituire solo le azioni che è possibile associare al tipo di parametro di associazione esatto \(nessun tipo derivato\).  Il metodo viene chiamato una volta per ogni richiesta per tipo rilevato e il risultato viene memorizzato nella cache da WCF Data Services.  
  
#### TryResolveServiceAction  
 Questo metodo cerca un oggetto <xref:System.Data.Services.Providers.ServiceAction> specificato e restituisce `true` se l'oggetto <xref:System.Data.Services.Providers.ServiceAction> viene trovato.  Se trovato, <xref:System.Data.Services.Providers.ServiceAction> viene restituito nel parametro `serviceAction` `out`.  
  
### IDataServiceInvokable  
 Questa interfaccia consente di eseguire un'azione di WCF Data Services.  Quando si implementa IDataServiceInvokable, si è responsabili di tre operazioni:  
  
1.  Acquisizione e marshalling potenziale dei parametri  
  
2.  Distribuzione dei parametri nel codice che implementa effettivamente l'azione quando viene chiamato Invoke\(\)  
  
3.  Archiviazione dei risultati restituiti da Invoke\(\) in modo da poter essere recuperati mediante GetResult\(\)  
  
 I parametri possono essere passati come token  poiché è possibile scrivere un provider di servizi dati da usare con i token che rappresentano le risorse. In tal caso, potrebbe essere necessario convertire \(effettuare il marshalling\) i token in risorse effettive prima della distribuzione all'azione effettiva.  Dopo il marshalling del parametro, è necessario che venga impostato uno stato modificabile in modo tale che tutte le modifiche alla risorsa, che si verificano quando l'azione viene richiamata, vengano salvate e scritte su disco.  
  
 Questa interfaccia richiede due metodi: Invoke e GetResult.  Invoke richiama il delegato che implementa il comportamento dell'azione e GetResult restituisce il risultato dell'azione.  
  
## Richiamo di un'azione di WCF Data Services  
 Le azioni vengono richiamate mediante una richiesta HTTP POST.  L'URL specifica la risorsa seguita dal nome dell'azione.  I parametri vengono passati nel corpo della richiesta.  Se ad esempio è presente un servizio denominato MovieService che espone un'azione denominata Rate,  è possibile usare l'URL seguente per richiamare l'azione Rate in un filmato specifico:  
  
 http:\/\/MovieServer\/MovieService.svc\/Movies\(1\)\/Rate  
  
 Movies\(1\) specifica il filmato che si desidera valutare e Rate specifica l'azione di valutazione.  Il valore effettivo della valutazione sarà presente nel corpo della richiesta HTTP come mostrato nell'esempio seguente:  
  
```  
POST http://MovieServer/MoviesService.svc/Movies(1)/Rate HTTP/1.1   
Content-Type: application/json   
Content-Length: 20   
Host: localhost:15238  
{   
   "rating": 4   
}  
  
```  
  
> [!WARNING]
>  Il codice di esempio precedente funzionerà solo con WCF Data Services 5.2 e versioni successive che supportano la versione light di JSON.  Se si usa una versione precedente di WCF Data Services, è necessario specificare il tipo di contenuto json verbose come segue: `application/json;odata=verbose`.  
  
 In alternativa, è possibile richiamare un'azione mediante il client di WCF Data Services come mostrato nel frammento di codice seguente.  
  
```  
MoviesModel context = new MoviesModel (new Uri("http://MyServer/MoviesService.svc/"));  
            //...  
            context.Execute(new Uri("http://MyServer/MoviesService.svc/Movies(1)/Rate"), "POST", new BodyOperationParameter("rating",4) );           
```  
  
 Nel frammento di codice precedente la classe `MoviesModel` è stata generata mediante la procedura per aggiungere il riferimento a un servizio WCF Data Services in Visual Studio.  
  
## Vedere anche  
 [WCF Data Services 4.5](../../../../docs/framework/data/wcf/index.md)   
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)   
 [Sviluppo e distribuzione di WCF Data Services](../../../../docs/framework/data/wcf/developing-and-deploying-wcf-data-services.md)   
 [Provider di servizi dati personalizzati](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)