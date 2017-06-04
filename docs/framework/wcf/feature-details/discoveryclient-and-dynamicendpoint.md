---
title: "DiscoveryClient e DynamicEndpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7cd418f0-0eab-48d1-a493-7eb907867ec3
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# DiscoveryClient e DynamicEndpoint
Gli oggetti <xref:System.ServiceModel.Discovery.DiscoveryClient> e <xref:System.ServiceModel.Discovery.DynamicEndpoint> sono due classi utilizzate sul lato client per cercare servizi.<xref:System.ServiceModel.Discovery.DiscoveryClient> fornisce un elenco di servizi che soddisfano un set di criteri specifico e consente di connettersi ai servizi.<xref:System.ServiceModel.Discovery.DynamicEndpoint> esegue la stessa operazione e si connette inoltre a uno dei servizi trovati in modo automatico.È possibile trasformare qualsiasi endpoint in un oggetto <xref:System.ServiceModel.Discovery.DynamicEndpoint>. È inoltre possibile aggiungere criteri di ricerca alla configurazione, pertanto un oggetto <xref:System.ServiceModel.Discovery.DynamicEndpoint> è utile se l'individuazione è necessaria nella soluzione, ma non si desidera modificare la logica client: a tale scopo è sufficiente modificare gli endpoint.D'altro canto, è possibile utilizzare l'oggetto <xref:System.ServiceModel.Discovery.DiscoveryClient> per ottenere un livello di controllo più preciso sull'operazione di ricerca.Gli utilizzi e i vantaggi di ogni classe vengono indicati di seguito.  
  
## DiscoveryClient  
 <xref:System.ServiceModel.Discovery.DiscoveryClient> definisce metodi Find sincroni e asincroni, eventi <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> e <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged>.Definisce inoltre metodi Resolve sincroni e asincroni, nonché un evento <xref:System.ServiceModel.Discovery.DiscoveryClient.ResolveCompleted>.Utilizzare i metodi <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> o <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> per cercare servizi.Entrambi i metodi utilizzano un'istanza <xref:System.ServiceModel.Discovery.FindCriteria> che consente di specificare nomi di tipi di contratto, ambiti, numero massimo di risultati richiesti e regole di corrispondenza dell'ambito.Gli eventi <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> e <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> possono essere utilizzati in caso di chiamata del metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A>.L'evento <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> viene generato ogni qualvolta l'oggetto <xref:System.ServiceModel.Discovery.DiscoveryClient> riceve una risposta da un servizio.Può essere utilizzato per visualizzare un indicatore di stato relativo all'operazione di ricerca,nonché per agire sulle risposte di ricerca nel momento in cui vengono ricevute.L'evento <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> si verifica nel momento in cui l'operazione di ricerca viene completato.Ciò potrebbe verificarsi poiché è stato ricevuto il numero massimo di risposte o se è trascorso il valore relativo a <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A>.Se l'operazione di ricerca viene completata, i risultati vengono restituiti in un'istanza <xref:System.ServiceModel.Discovery.FindResponse>.<xref:System.ServiceModel.Discovery.FindResponse> contiene una raccolta di <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> che contiene gli indirizzi, i nomi dei tipi di contratto, le estensioni, gli URI di ascolto e gli ambiti dei servizi corrispondenti.È quindi possibile utilizzare queste informazioni per connettersi e chiamare uno dei servizi corrispondenti.Nell'esempio seguente viene indicato come chiamare il metodo [the M:System.ServiceModel.Discovery.DiscoveryClient.Find\(System.ServiceModel.Discovery.FindCriteria\)](assetId:///the M:System.ServiceModel.Discovery.DiscoveryClient.Find(System.ServiceModel.Discovery.FindCriteria)?qualifyHint=False&autoUpgrade=True) e utilizzare i metadati restituiti per chiamare il servizio rilevato.Un vantaggio derivante dall'utilizzo di <xref:System.ServiceModel.Discovery.DiscoveryClient> consiste nel fatto che è possibile memorizzare nella cache l'elenco di endpoint trovati e utilizzarli in un secondo momento.Con questa cache è possibile compilare una logica personalizzata per gestire le varie condizioni di errore.  
  
```  
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
FindCriteria criteria = new FindCriteria(typeof(ICalculatorService));  
FindResponse fr = dc.Find(criteria);  
  
if (fr.Endpoints.Count > 0)  
{  
   EndpointAddress ep = fr.Endpoints[0].Address;  
   CalculatorServiceClient client = new CalculatorServiceClient();  
  
    // Connect to the discovered service endpoint  
   client.Endpoint.Address = endpointAddress;  
   Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
   double value1 = 100.00D;  
   double value2 = 15.99D;  
  
   // Call the Add service operation.  
   double result = client.Add(value1, value2);  
   Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
}  
else  
   Console.WriteLine(“No matching endpoints found”);  
  
```  
  
 Nell'esempio seguente viene mostrato come eseguire in modo asincrono un'operazione di ricerca.  
  
```  
static void FindServiceAsync()  
{  
   DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());   
   dc.FindCompleted += new EventHandler<FindCompletedEventArgs>( discoveryClient_FindCompleted);  
   dc.FindProgressChanged += new EventHandler<FindProgressChangedEventArgs>(discoveryClient_FindProgressChanged);  
   dc.FindAsync(new FindCriteria(typeof(ICalculatorService)));   
}   
static void discoveryClient_FindProgressChanged(object sender, FindProgressChangedEventArgs e)  
{  
   Console.WriteLine("Found service at: " + e.EndpointDiscoveryMetadata.Address  
}   
  
static void discoveryClient_FindCompleted(object sender, FindCompletedEventArgs e)  
{    
      if (e.Result.Endpoints.Count > 0)  
            {  
                EndpointAddress ep = e.Result.Endpoints[0].Address;  
                CalculatorServiceClient client = new CalculatorServiceClient();  
  
                // Connect to the discovered service endpoint  
                client.Endpoint.Address = ep;  
                Console.WriteLine("Invoking CalculatorService at {0}", ep);  
  
                double value1 = 100.00D;  
                double value2 = 15.99D;  
  
                double result = client.Add(value1, value2);  
                Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
            }  
            else  
                Console.WriteLine("No matching endpoints found");  
  
        }  
  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come effettuare chiamate di ricerca asincrone, vedere [Ricerca asincrona](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md).  
  
 Utilizzare i metodi <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> e <xref:System.ServiceModel.Discovery.ResolveAsync%28System.ServiceModel.Discovery.ResolveCriteria%29> per individuare un servizio in base al relativo indirizzo endpoint.Ciò risulta utile nel caso in cui l'indirizzo endpoint non è indirizzabile alla rete.I metodi Resolve utilizzano un'istanza di <xref:System.ServiceModel.Discovery.ResolveCriteria> che consente di specificare l'indirizzo endpoint del servizio in fase di risoluzione, la durata massima dell'operazione di risoluzione e un set di estensioni.Nell'esempio riportato di seguito viene mostrato come utilizzare il metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> per risolvere un servizio.  
  
```  
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
ResolveCriteria criteria = new ResolveCriteria(endpointAddress);  
ResolveResponse response = dc.Resolve(criteria);  
EndpointAddress newEp = response.EndpointDiscoveryMetadata.Address;  
  
```  
  
## DynamicEndpoint  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint> è un endpoint standard \([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Endpoint standard](../../../../docs/framework/wcf/feature-details/standard-endpoints.md)\) che esegue l'individuazione e seleziona in modo automatico un servizio corrispondente.È sufficiente creare un <xref:System.ServiceModel.Discovery.DynamicEndpoint> che passa il contratto da cercare e l'associazione da utilizzare e passare l'istanza <xref:System.ServiceModel.Discovery.DynamicEndpoint> al client WCF.Nell'esempio seguente viene illustrato come creare e utilizzare un <xref:System.ServiceModel.Discovery.DynamicEndpoint> per chiamare il servizio di calcolo.L'individuazione viene eseguita a ogni apertura del client.Anche qualsiasi endpoint definito nella configurazione può essere trasformato in un <xref:System.ServiceModel.Discovery.DynamicEndpoint> aggiungendo l'attributo `kind =”dynamicEndpoint”` all'elemento di configurazione dell'endpoint.  
  
```  
  
DynamicEndpoint dynamicEndpoint = new DynamicEndpoint(ContractDescription.GetContract(typeof(ICalculatorService)), new WSHttpBinding());  
CalculatorServiceClient client = new CalculatorServiceClient(dynamicEndpoint);  
  
Console.WriteLine("Invoking CalculatorService");  
Console.WriteLine();  
  
double value1 = 100.00D;  
double value2 = 15.99D;  
  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
```  
  
## Vedere anche  
 [Individuazione con ambiti](../../../../docs/framework/wcf/samples/discovery-with-scopes-sample.md)   
 [Ricerca asincrona](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md)   
 [Di base](../../../../docs/framework/wcf/samples/basic-sample.md)