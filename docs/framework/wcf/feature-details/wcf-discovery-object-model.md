---
title: "Modello a oggetti WCF Discovery | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8365a152-eacd-4779-9130-bbc48fa5c5d9
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Modello a oggetti WCF Discovery
WCF Discovery è costituito da un set di tipi che forniscono un modello di programmazione unificato che consente di scrivere servizi individuabili al runtime e client in grado di trovare e utilizzare tali servizi.  
  
## Come rendere individuabile un servizio e trovare i servizi  
 Per rendere individuabile un servizio WCF, aggiungere un elemento <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> all'oggetto <xref:System.ServiceModel.Description.ServiceDescription> dell'host del servizio e aggiungere un endpoint di individuazione.Se un servizio è configurato per inviare messaggi di annuncio \(con <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>\), l'annuncio viene inviato quando l'host del servizio viene aperto e chiuso.  
  
 Per essere in ascolto dei messaggi di annuncio del servizio, un client ospita un servizio annunci e aggiunge uno o più endpoint annunci.Il servizio annunci riceve i messaggi di annuncio e genera eventi di annuncio.  
  
 Il client utilizza la classe <xref:System.ServiceModel.Discovery.DiscoveryClient> per cercare i servizi disponibili.L'applicazione client crea un'istanza della classe <xref:System.ServiceModel.Discovery.DiscoveryClient>, passando un endpoint di individuazione che specifica dove inviare i messaggi di individuazione.Il client chiama il metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> che invia una richiesta `Probe`.I servizi in ascolto dei messaggi di individuazione ricevono la richiesta `Probe`.Se il servizio corrisponde ai criteri specificati in `Probe`, al client viene restituito il messaggio `ProbeMatch`.  
  
## Modello a oggetti  
 L'API di WCF Discovery definisce le classi seguenti:  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementClient>  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementService>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryClient>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator>  
  
-   <xref:System.ServiceModel.Discovery.ServiceDiscoveryMode>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryProxy>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryService>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryVersion>  
  
-   <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>  
  
-   <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>  
  
-   <xref:System.ServiceModel.Discovery.FindCriteria>  
  
-   <xref:System.ServiceModel.Discovery.FindRequestContext>  
  
-   <xref:System.ServiceModel.Discovery.FindResponse>  
  
-   <xref:System.ServiceModel.Discovery.ResolveCriteria>  
  
-   <xref:System.ServiceModel.Discovery.ResolveResponse>  
  
-   <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>  
  
-   <xref:System.ServiceModel.Discovery.ServiceDiscoveryExtension>  
  
-   <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
## AnnouncementClient  
 La classe <xref:System.ServiceModel.Discovery.AnnouncementClient> include metodi sincroni e asincroni per l'invio di messaggi di annuncio.Esistono due tipi di messaggi di annuncio, Hello e Bye.Il messaggio Hello viene inviato per indicare che un servizio è diventato disponibile, mentre il messaggio Bye viene inviato per indicare che un servizio esistente non è più disponibile.Lo sviluppatore crea un'istanza di <xref:System.ServiceModel.Discovery.AnnouncementClient>, passando un'istanza di <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> come parametro costruttore.  
  
## AnnouncementEndpoint  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> rappresenta un endpoint standard con un contratto annuncio fisso.È utilizzato da un servizio o da un client per inviare e ricevere messaggi di annuncio.Per impostazione predefinita, la classe <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> è impostata per utilizzare la versione del protocollo WS\_Discovery 11.  
  
## AnnouncementService  
 <xref:System.ServiceModel.Discovery.AnnouncementService> è un'implementazione fornita dal sistema di un servizio annunci che riceve ed elabora messaggi di annuncio.Quando viene ricevuto un messaggio Hello o Bye, l'istanza di <xref:System.ServiceModel.Discovery.AnnouncementService> chiama il metodo virtuale appropriato <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOnlineAnnouncement%2A> o <xref:System.ServiceModel.Discovery.AnnouncementService.OnBeginOfflineAnnouncement%2A>, il quale genera un evento di annuncio.  
  
## DiscoveryClient  
 La classe <xref:System.ServiceModel.Discovery.DiscoveryClient> viene utilizzata da un'applicazione client per trovare e risolvere i servizi disponibili.Fornisce metodi sincroni e asincroni per individuare e risolvere i servizi rispettivamente in base agli elementi <xref:System.ServiceModel.Discovery.FindCriteria> e <xref:System.ServiceModel.Discovery.ResolveCriteria> specificati.Lo sviluppatore crea un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryClient> e fornisce un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> come parametro costruttore.  
  
 Per trovare un servizio, lo sviluppatore richiama il metodo `Find` sincrono o asincrono che fornisce un'istanza di <xref:System.ServiceModel.Discription.FindCriteria> che contiene i criteri di ricerca da utilizzare.<xref:System.ServiceModel.Discovery.DiscoveryClient> crea un messaggio `Probe` con le intestazioni appropriate ed invia la richiesta di individuazione.Poiché possono essere presenti più richieste `Find` in attesa in un determinato momento, il client correla le risposte ricevute e convalida la risposta.Recapita quindi i risultati al chiamante dell'operazione `Find` utilizzando <xref:System.ServiceModel.Discovery.FindResponse>.  
  
 Per risolvere un servizio noto, lo sviluppatore richiama il metodo `Resolve` sincrono o asincrono che fornisce un'istanza di <xref:System.ServiceModel.ResolveCriteria> contenente l'elemento <xref:System.ServiceModel.EndpointAddress> del servizio noto.<xref:System.ServiceModel.Discovery.DiscoveryClient> crea il messaggio `Resolve` con le intestazioni appropriate ed invia la richiesta di risoluzione.La risposta ricevuta viene correlata rispetto alle richieste di risoluzione in attesa ed il risultato viene recapitato al chiamante dell'operazione `Resolve` utilizzando <xref:System.ServiceModel.Discovery.ResolveResponse>.  
  
 Se in rete è presente un proxy di individuazione e <xref:System.ServiceModel.Discover.DiscoveryClient> invia la richiesta di individuazione in modo multicast, il proxy di individuazione può rispondere con il messaggio Hello di eliminazione multicast.<xref:System.ServiceModel.Discover.DiscoveryClient> genera l'evento `ProxyAvailable` quando riceve messaggi Hello in risposta alle richieste `Find` o `Resolve` in attesa.L'evento `ProxyAvailable` contiene i dati <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> relativi al proxy di individuazione.A seconda delle esigenze, lo sviluppatore può decidere se utilizzare queste informazioni per passare dalla modalità ad hoc a quella gestita.  
  
## DiscoveryEndpoint  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> rappresenta un endpoint standard con un contratto di individuazione fisso.È utilizzato da un servizio o da un client per inviare o ricevere messaggi di individuazione.Per impostazione predefinita, <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> è impostato per utilizzare la modalità <xref:System.ServiceModel.Discovery.DiscoveryMode.Managed> e la versione del protocollo WS\_Discovery 11.  
  
## DiscoveryMessageSequenceGenerator  
 <xref:System.ServiceModel.Discovery.DiscoveryMessageSequenceGenerator> è utilizzato per generare un oggetto <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence> quando il servizio invia messaggi di individuazione o di annuncio.  
  
## DiscoveryService  
 La classe astratta <xref:System.ServiceModel.Discovery.DiscoveryService> offre un framework per ricevere ed elaborare messaggi `Probe` e `Resolve`.Quando viene ricevuto un messaggio `Probe`, <xref:System.ServiceModel.Discovery.DiscoveryService> crea un'istanza di <xref:System.ServiceModel.Discovery.FindRequestContext> in base al messaggio in ingresso e richiama il metodo virtuale <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A>.Quando viene ricevuto un messaggio `Resolve`, <xref:System.ServiceModel.Discovery.DiscoveryService> richiama il metodo virtuale <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginResolve%2A>.È possibile ereditare da questa classe per fornire un'implementazione personalizzata del servizio di individuazione.  
  
## DiscoveryProxy  
 La classe astratta <xref:System.ServiceModel.Discovery.DiscoveryProxy> offre un framework per ricevere ed elaborare messaggi di individuazione e di annuncio.È possibile ereditare da questa classe quando si implementa un proxy di individuazione personalizzato.Quando un messaggio `Probe` viene ricevuto tramite multicast, la classe <xref:System.ServiceModel.Discovery.DiscoveryProxy> chiama il metodo virtuale `BeginShouldRedirectFind` per determinare se deve essere inviato un messaggio di eliminazione multicast.Se lo sviluppatore decide di non inviare un messaggio di eliminazione multicast o se il messaggio `Probe` è ricevuto tramite unicast, crea un'istanza della classe <xref:System.ServiceModel.Discovery.FindRequestContext> basata sul messaggio in arrivo e richiama il metodo virtuale `OnBeginFind`.Quando un messaggio `Resolve` viene ricevuto tramite multicast, la classe <xref:System.ServiceModel.Discovery.DiscoveryProxy> chiama il metodo virtuale `ShouldRedirectResolve` per determinare se deve essere inviato un messaggio di eliminazione multicast.Se lo sviluppatore decide di non inviare un messaggio di eliminazione multicast o se il messaggio `Resolve` è ricevuto tramite unicast, crea un'istanza della classe <xref:System.ServiceModel.Discovery.ResolveCriteria> basata sul messaggio in arrivo e richiama il metodo virtuale `OnBeginResolve`.Quando viene ricevuto un messaggio Hello o Bye, <xref:System.ServiceModel.Discovery.DiscoveryProxy> chiama il metodo virtuale appropriato \(`OnBeginOnlineAnnouncement` o `OnBeingOfflineAnnouncement`\), il quale genera un evento di annuncio.  
  
## DiscoveryVersion  
 La classe <xref:System.ServiceModel.Discovery.DiscoveryVersion> rappresenta la versione del protocollo di individuazione da utilizzare.  
  
## EndpointDiscoveryBehavior  
 La classe <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> è utilizzata per controllare l'individuabilità di un endpoint, specificare le estensioni, i nomi dei tipi di contratto aggiuntivie gli ambiti associati all'endpoint.Questo comportamento viene aggiunto a un endpoint applicazione per configurare i relativi dati di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.Quando <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> viene aggiunto all'host del servizio, tutti gli endpoint applicazione ospitati dall'host del servizio diventano individuabili per impostazione predefinita.Lo sviluppatore può disabilitare l'individuazione per uno specifico endpoint impostando la proprietà <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Enable%2A> su `false`.  
  
## EndpointDiscoveryMetadata  
 La classe <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> fornisce una rappresentazione indipendente dalla versione di un endpoint pubblicato dal servizio.Contiene indirizzi endpoint, URI di ascolto, nomi di tipo di contratto, ambiti, versione dei metadati ed estensioni specificati dallo sviluppatore del servizio.L'oggetto <xref:System.ServiceModel.Discovery.FindCriteria> inviato dal client durante un'operazione `Probe` viene confrontato con <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.Se i criteri corrispondono, al client viene restituito <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.L'indirizzo dell'endpoint in <xref:System.ServiceModel.Discovery.ResolveCriteria> viene confrontato con l'indirizzo dell'endpoint di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.Se i criteri corrispondono, al client viene restituito <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.  
  
## FindCriteria  
 La classe <xref:System.ServiceModel.Discovery.FindCriteria> è una classe indipendente dalla versione utilizzata per specificare i criteri utilizzati per trovare un servizio.Supporta completamente i criteri definiti da WS\-Discovery per individuare le corrispondenze con i servizi.Dispone inoltre di estensioni che gli sviluppatori possono specificare valori personalizzati utilizzabili durante il processo di individuazione delle corrispondenze.Lo sviluppatore può specificare i criteri di chiusura per l'operazione `Find` impostando <xref:System.ServiceModel.Discovery.FindCriteria.MaxResult%2A>, che specifica il numero complessivo di servizi che lo sviluppatore cerca oppure <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A>, ovvero il valore che indica la durata dell'attesa delle risposte nel client.  
  
## FindRequestContext  
 L'istanza della classe <xref:System.ServiceModel.Discovery.FindRequestContext> viene creata dal servizio di individuazione in base al messaggio `Probe` ricevuto quando un client avvia l'operazione `Find`.Contiene un'istanza di <xref:System.ServiceModel.Discovery.FindCriteria> specificata dal client.  
  
## FindResponse  
 La classe <xref:System.ServiceModel.Discovery.FindResponse> viene restituita al chiamante di <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> con le risposte dell'operazione `Find`.È inoltre presente in <xref:System.ServiceModel.Discovery.FindCompletedEventArgs>.Contiene una raccolta di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>, ovvero la raccolta degli endpoint individuati e un dizionario di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> e <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence>.  
  
## ResolveCriteria  
 La classe <xref:System.ServiceModel.Discovery.ResolveCriteria> è indipendente dalla versione e viene utilizzata per specificare i criteri utilizzati per la risoluzione di un servizio già noto.Contiene l'indirizzo dell'endpoint del servizio noto.Lo sviluppatore può specificare i criteri di chiusura per l'operazione di risoluzione impostando <xref:System.ServiceModel.Discovery.ResolveCriteria.Duration%2A>, che indica la durata dell'attesa delle risposte da parte del client.  
  
## ResolveResponse  
 La classe <xref:System.ServiceModel.Discovery.ResolveResponse> viene restituita al chiamante del metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> con la risposta dell'operazione `Resolve`.È inoltre presente in <xref:System.ServiceModel.Discovery.ResolveCompletedEventArgs>.Contiene un'istanza di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>, ovvero degli endpoint individuati e un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryMessageSequence>.  
  
## ServiceDiscoveryBehavior  
 La classe <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> consente allo sviluppatore di aggiungere la funzionalità di individuazione a un servizio.Questo comportamento viene aggiunto a <xref:System.ServiceModel.ServiceHost>.La classe <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> esegue iterazioni sugli endpoint applicazione aggiunti all'host del servizio e crea una raccolta di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> dagli endpoint individuabili.Tutti gli endpoint sono individuabili per impostazione predefinita.L'individuabilità di un determinato endpoint può essere controllata aggiungendo <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior> a un determinato endpoint.Se gli endpoint annunci vengono aggiunti a <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>, l'annuncio di tutti gli endpoint individuabili viene inviato tramite ognuno degli endpoint annunci quando l'host del servizio è aperto o chiuso.  
  
## ServiceDiscoveryExtension  
 La classe <xref:System.ServiceModel.Discovery.ServiceDiscoveryExtension> viene creata dalla classe <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>.È possibile ottenere gli endpoint resi individuabili da <xref:System.ServiceModel.Discovery.ServiceDiscoveryExtension>.Questa classe è inoltre utilizzata per specificare un'implementazione del servizio di individuazione personalizzato.  
  
## UdpAnnouncementEndpoint  
 La classe <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> è un endpoint annuncio standard preconfigurato per l'annuncio tramite un'associazione multicast UDP.Per impostazione predefinita, <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> viene impostato per utilizzare la versione WSApril2005 di WS\_Discovery.  
  
## UdpDiscoveryEndpoint  
 La classe <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> è un endpoint di individuazione standard preconfigurata per l'individuazione tramite l'associazione multicast UDP.Per impostazione predefinita, <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> è impostato per utilizzare la versione WSDiscovery11 di WS\-Discovery e la modalità <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint.Adhoc>.