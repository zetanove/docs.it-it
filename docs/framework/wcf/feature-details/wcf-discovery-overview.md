---
title: "Panoramica di WCF Discovery | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 84fad0e4-23b1-45b5-a2d4-c9cdf90bbb22
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Panoramica di WCF Discovery
Le API di individuazione offrono un modello di programmazione unificato per la pubblicazione dinamica e l'individuazione di servizi Web utilizzando il protocollo WS\-Discovery.Queste API consentono la pubblicazione dei servizi e l'individuazione di tali servizi da parte dei client.Una volta reso individuabile un servizio, quest'ultimo è in grado di inviare messaggi di annuncio nonché di essere in ascolto e di rispondere alle richieste di individuazione.I servizi individuabili possono inviare messaggi Hello per annunciare la propria presenza in rete e messaggi Bye per annunciare la propria uscita dalla rete.Per trovare un servizio, i client inviano una richiesta `Probe` contenente criteri specifici quali il tipo di contratto servizio, le parole chiave e l'ambito nella rete.I servizi ricevono la richiesta `Probe` e determinano se corrisponde ai criteri.Se un servizio corrisponde, risponde restituendo un messaggio `ProbeMatch` al client con le informazioni necessarie per contattare il servizio.I client possono inoltre inviare richieste `Resolve` che consentono loro di individuare i servizi che hanno modificato il relativo indirizzo endpoint.I servizi corrispondenti rispondono alle richieste `Resolve` restituendo al client un messaggio `ResolveMatch`.  
  
## Modalità ad hoc e gestita  
 L'API di individuazione supporta due diverse modalità, ovvero gestita \(Managed\) e ad hoc \(Adhoc\).Nella modalità gestita è presente un server centralizzato denominato proxy di individuazione che gestisce le informazioni relative ai servizi disponibili.Il proxy di individuazione può essere popolato con le informazioni sui servizi in diversi modi.I servizi possono ad esempio inviare al proxy di individuazione messaggi di annuncio in fase di avvio oppure il proxy può leggere i dati da un database o da un file di configurazione per determinare i servizi disponibili.La modalità di popolamento di un proxy di individuazione viene scelta dallo sviluppatore.I client utilizzano il proxy di individuazione per recuperare informazioni sui servizi disponibili.Quando un client cerca un servizio, invia un messaggio `Probe` al proxy di individuazione il quale determina se sono disponibili servizi noti corrispondenti a quello richiesto dal client.Se vengono individuate corrispondente il proxy di individuazione restituisce una risposta `ProbeMatch` al client.Il client può quindi contattare il servizio utilizzando direttamente le apposite informazioni restituite dal proxy.Il principio chiave per quanto concerne la modalità gestite consiste nel fatto che le richieste di individuazione vengono inviate in modo unicast a un'autorità, ovvero il proxy di individuazione..NET Framework contiene componenti chiave che consentono di compilare un proxy personalizzato.I client e i servizi possono individuare il proxy in diversi modi:  
  
-   Il proxy può rispondere a messaggi ad hoc.  
  
-   Il proxy può inviare un messaggio di annuncio in fase di avvio.  
  
-   I client e i servizi possono essere progettati in modo da cercare un endpoint noto specifico.  
  
 Nella modalità ad hoc non è presente alcun server centralizzato.Tutti i messaggi di individuazione, quali gli annunci dei servizi e le richieste dei client, vengono inviati in modalità multicast.Per impostazione predefinita .NET Framework supporta l'individuazione ad hoc su protocollo UDP.Se ad esempio un servizio è configurato per inviare un annuncio Hello all'avvio, il messaggio viene inviato a un indirizzo multicast noto mediante il protocollo UDP.I client devono essere attivamente in ascolto degli annunci ed elaborarli in modo appropriato.I messaggi `Probe` inviati da un client per un servizio vengono inviati sulla rete mediante il protocollo multicast.Ogni servizio che riceve la richiesta determina se sussiste la corrispondenza con i criteri del messaggio `Probe` e risponde direttamente al client con un messaggio `ProbeMatch` in caso di effettiva corrispondenza con i criteri del messaggio `Probe`.  
  
## Vantaggi dell'utilizzo WCF Discovery  
 Poiché WCF Discovery viene implementato mediante il protocollo WS\-Discovery è interoperativo con altri client, servizi e proxy che implementano tale protocollo.WCF Discovery si basa sulle API WCF esistenti che semplificano l'aggiunta della funzionalità di individuazione ai servizi e ai client esistenti.È possibile rendere i servizi individuabili tramite le impostazioni di configurazione dell'applicazione.WCF Discovery supporta inoltre l'utilizzo del protocollo di individuazione su trasporti quali rete peer, sovrapposizione della denominazione e HTTP.WCF Discovery offre supporto per la modalità di funzionamento gestita in cui viene utilizzato un proxy di individuazione.Ciò consente di ridurre il traffico di rete poiché i messaggi vengono inviati direttamente al proxy di individuazione invece che tramite multicast all'intera rete.WCF Discovery assicura inoltre maggiore flessibilità per l'utilizzo dei servizi Web.È ad esempio possibile modificare l'indirizzo di un servizio senza dovere riconfigurare il client o il servizio.Quando un client deve accedere al servizio può inviare un messaggio `Probe` tramite una richiesta `Find` e attendere che il servizio risponda con il relativo indirizzo corrente.WCF Discovery consente a un client di cercare un servizio in base a diversi criteri tra cui i tipi di contratto, gli elementi di associazione, lo spazio dei nomi, l'ambito, le parole chiave o i numeri di versione.WCF Discovery consente l'individuazione in fase di esecuzione e di progettazione.L'aggiunta della funzionalità di individuazione all'applicazione rende possibili altri scenari quali la tolleranza di errore e la configurazione automatica.  
  
## Pubblicazione di un servizio  
 Per rendere individuabile un servizio, è necessario aggiungere <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> all'host del servizio nonché un endpoint di individuazione per specificare dove essere in ascolto dei messaggi di individuazione.Nell'esempio di codice seguente viene illustrato come modificare un servizio indipendente per renderlo individuabile.  
  
```  
Uri baseAddress = new Uri(string.Format("http://{0}:8000/discovery/scenarios/calculatorservice/{1}/",  
        System.Net.Dns.GetHostName(), Guid.NewGuid().ToString()));  
  
// Create a ServiceHost for the CalculatorService type.  
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))  
{  
    // add calculator endpoint  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), string.Empty);  
  
    // ** DISCOVERY ** //  
    // make the service discoverable by adding the discovery behavior  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
  
    // ** DISCOVERY ** //  
    // add the discovery endpoint that specifies where to publish the services  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
  
    // Open the ServiceHost to create listeners and start listening for messages.  
    serviceHost.Open();  
  
    // The service can now be accessed.  
    Console.WriteLine("Press <ENTER> to terminate service.");  
    Console.ReadLine();  
}  
```  
  
 È necessario aggiungere un'istanza di <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior> a una descrizione del servizio da rendere individuabile.È necessario aggiungere un'istanza di <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> all'host del servizio per indicare al servizio dove essere in ascolto delle richieste di individuazione.In questo esempio, viene aggiunto un oggetto <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> \(derivato da <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>\) per specificare che il servizio deve essere in ascolto delle richieste di individuazione sul trasporto multicast UDP.<xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> viene utilizzato per l'individuazione ad hoc poiché tutti i messaggi vengono inviati in modalità multicast.  
  
## Annuncio  
 Per impostazione predefinita, la pubblicazione del servizio non implica l'invio di messaggi di annuncio.È necessario configurare il servizio affinché invii tali messaggi.Ciò assicura ulteriore flessibilità agli sviluppatori dei servizi, in quanto questi ultimi possono essere annunciati separatamente rispetto all'ascolto dei messaggi di individuazione.L'annuncio del servizio può essere inoltre utilizzato come meccanismo per la registrazione dei servizi in un proxy di individuazione o altri registri di servizi.Nel codice seguente viene illustrato come configurare un servizio affinché invii messaggi di annuncio tramite un'associazione UDP.  
  
```  
Uri baseAddress = new Uri(string.Format("http://{0}:8000/discovery/scenarios/calculatorservice/{1}/",  
        System.Net.Dns.GetHostName(), Guid.NewGuid().ToString()));  
  
// Create a ServiceHost for the CalculatorService type.  
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))  
{  
    // add calculator endpoint  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), string.Empty);  
  
    // ** DISCOVERY ** //  
    // make the service discoverable by adding the discovery behavior  
    ServiceDiscoveryBehavior discoveryBehavior = new ServiceDiscoveryBehavior();  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
  
    // send announcements on UDP multicast transport  
    discoveryBehavior.AnnouncementEndpoints.Add(  
      new UdpAnnouncementEndpoint());  
  
    // ** DISCOVERY ** //  
    // add the discovery endpoint that specifies where to publish the services  
    serviceHost.Description.Endpoints.Add(new UdpDiscoveryEndpoint());  
  
    // Open the ServiceHost to create listeners and start listening for messages.  
    serviceHost.Open();  
  
    // The service can now be accessed.  
    Console.WriteLine("Press <ENTER> to terminate service.");  
    Console.ReadLine();  
}  
```  
  
## Individuazione dei servizi  
 Le applicazioni client possono utilizzare la classe <xref:System.ServiceModel.Discovery.DiscoveryClient> per individuare i servizi.Lo sviluppatore crea un'istanza della classe <xref:System.ServiceModel.Discovery.DiscoveryClient> che passa un endpoint di individuazione che specifica dove inviare messaggi `Probe` o `Resolve`.Il client chiama quindi <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> che specifica i criteri di ricerca all'interno di un'istanza di <xref:System.ServiceModel.Discovery.FindCriteria>.Se vengono individuati servizi corrispondenti, <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> restituisce una raccolta di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata>.Nel codice seguente viene illustrato come chiamare il metodo `Find` e connettersi quindi ad un servizio individuato.  
  
```  
class Client  
{  
    static EndpointAddress serviceAddress;  
  
    static void Main()  
    {  
        if (FindService()) InvokeService();  
    }  
  
    // ** DISCOVERY ** //  
    static bool FindService()  
    {  
        Console.WriteLine("\nFinding Calculator Service ..");  
        DiscoveryClient discoveryClient =   
            new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
        Collection<EndpointDiscoveryMetadata> calculatorServices =   
            discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
  
        discoveryClient.Close();  
  
        if (calculatorServices.Count == 0)  
        {  
            Console.WriteLine("\nNo services are found.");  
            return false;  
        }  
        else  
        {  
            serviceAddress = calculatorServices[0].EndpointAddress;  
            return true;  
        }  
    }  
  
    static void InvokeService()  
    {  
        Console.WriteLine("\nInvoking Calculator Service at {0}\n", serviceAddress);  
  
        // Create a client  
        CalculatorClient client = new CalculatorClient();  
        client.Endpoint.Address = serviceAddress;  
        client.Add(10,3);  
}  
```  
  
## Sicurezza a livello di individuazione e messaggio  
 Quando si utilizza la sicurezza a livello di messaggio è necessario specificare un oggetto <xref:System.ServiceModel.EndpointIdentity> nell'endpoint di individuazione del servizio e un oggetto <xref:System.ServiceModel.EndpointIdentity> corrispondente nell'endpoint di individuazione del client.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sicurezza a livello di messaggio, vedere [Protezione dei messaggi](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).  
  
## Individuazione e servizi ospitati su Web  
 I servizi WCF per essere individuabili devono essere in esecuzione.I servizi WCF ospitati in IIS o WAS non vengono eseguiti fino a quando IIS\/WAS non riceve un messaggio associato per il servizio, quindi non possono essere individuabili per impostazione predefinita.Per rendere i servizi ospitati su Web individuabili esistono due opzioni:  
  
1.  Utilizzare la funzionalità di avvio automatico di Windows Server AppFabric  
  
2.  Utilizzare un proxy di individuazione per comunicare per conto del servizio  
  
 Windows Server AppFabric dispone di una funzionalità di avvio automatico che consente al servizio di essere avviato prima di ricevere qualsiasi messaggio.Con l'impostazione della funzionalità di avvio automatico, un servizio ospitato in IIS\/WAS può essere configurato per essere individuabile.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] funzionalità di avvio automatico, vedere [Funzionalità di avvio automatico di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=205545).Oltre ad abilitare la funzionalità di avvio automatico, è necessario configurare il servizio per l'individuazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: aggiungere capacità di individuazione a un client e un servizio WCF a livello di codice](../../../../docs/framework/wcf/feature-details/how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)[Configurazione dell'individuazione in un file di configurazione](../../../../docs/framework/wcf/feature-details/configuring-discovery-in-a-configuration-file.md).  
  
 Un proxy di individuazione può essere utilizzato per comunicare per conto del servizio WCF quando tale servizio non è in esecuzione.Il proxy può mettersi in ascolto del probe o risolvere i messaggi e rispondere al client.Il client può quindi inviare i messaggi direttamente al servizio.Quando il client invia un messaggio al servizio, verrà creata un'istanza di tale servizio per rispondere al messaggio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] implementazione del proxy di individuazione, vedere [Implementazione di un proxy di individuazione](../../../../docs/framework/wcf/feature-details/implementing-a-discovery-proxy.md).