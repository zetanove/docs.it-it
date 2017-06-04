---
title: "Ricerca di individuazione e FindCriteria | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99016fa4-1778-495b-b4cc-0e22fbec42c6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Ricerca di individuazione e FindCriteria
Un'operazione di ricerca dell'individuazione viene inizializzata da un client per individuare uno o più servizi ed è una delle azioni principali nell'ambito dell'individuazione.L'esecuzione di una ricerca invia un messaggio WS\-Discovery Probe sulla rete.I servizi che corrispondono ai criteri specificati inviano una risposta con i messaggi WS\-Discovery ProbeMatch.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] messaggi di individuazione, vedere il documento relativo alla [specifica WS\-Discovery](http://go.microsoft.com/fwlink/?LinkID=122347).  
  
## DiscoveryClient  
 La classe <xref:System.ServiceModel.Discovery.DiscoveryClient> fornisce il meccanismo necessario per eseguire operazioni di ricerca e agevola l'esecuzione delle operazioni del client di individuazione.Contiene un metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> che esegue una ricerca sincrona \(bloccante\) scoperta e un metodo <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> che viene inizializzato con una ricerca asincrona non bloccante.Entrambi i metodi utilizzano un parametro <xref:System.ServiceModel.Discovery.FindCriteria> e forniscono risultati all'utente tramite un oggetto <xref:System.ServiceModel.Discovery.FindResponse>.  
  
## FindCriteria  
 <xref:System.ServiceModel.Discovery.FindCriteria> dispone di varie proprietà, raggruppabili in criteri di ricerca, che specificano i servizi ricercati e cercano criteri di terminazione \(durata della ricerca\).Un elemento <xref:System.ServiceModel.Discovery.FindCriteria> può contenere più criteri di ricerca.Per impostazione predefinita, il servizio deve individuare corrispondenze per tutti i componenti. In caso contrario, non viene considerato un servizio corrispondente.Se si desidera cercare servizi che corrispondono solo a determinati criteri, è possibile implementare la logica di ricerca personalizzata nel servizio oppure utilizzare più query.  
  
 I criteri di ricerca includono:  
  
-   <xref:System.ServiceModel.Discovery.ContractTypeNames%2A> \- Facoltativo.Nome del contratto del servizio cercato e criteri in genere utilizzati in fase di ricerca di un servizio.Se viene specificato più di un nome di contratto, verrà inviata una risposta solo dagli endpoint del servizio corrispondenti a TUTTI i contratti.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] un endpoint può supportare un solo contratto.  
  
-   <xref:System.ServiceModel.Discovery.Scopes%2A> \- Facoltativo.Gli ambiti sono URI assoluti utilizzati per suddividere in categorie singoli endpoint servizio.Potrebbe risultare opportuno utilizzare questo ambito negli scenari in cui più endpoint espongono lo stesso contratto e si desidera un metodo di ricerca di un subset degli endpoint.Se viene specificato più di un ambito, verrà inviata una risposta solo dagli endpoint del servizio corrispondenti a TUTTI gli ambiti.  
  
-   <xref:System.ServiceModel.Discovery.ScopeMatchBy%2A> \- Specifica l'algoritmo di corrispondenza da utilizzare per individuare la corrispondenza tra l'ambito nel messaggio del Probe e quello dell'endpoint.Sono supportate cinque regole di corrispondenza degli ambiti:  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByExact%2A> esegue un confronto di base tra le stringhe con distinzione tra maiuscole e minuscole.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix%2A> individua la corrispondenza in base a segmenti separati da "\/".Una ricerca di http:\/\/contoso\/building1 corrisponde a un servizio con ambito http:\/\/contoso\/building\/floor1.Non corrisponde a http:\/\/contoso\/building100, perché gli ultimi due segmenti non corrispondono.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByLdap%2A> individua la corrispondenza degli ambiti in base ai segmenti utilizzando un URL LDAP.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByUuid%2A> individua la corrispondenza esatta degli ambiti utilizzando una stringa UUID.  
  
    -   <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByNone%2A> individua la corrispondenza con i soli servizi che non specificano un ambito.  
  
     Se non si specifica una regola di corrispondenza degli ambiti, verrà utilizzato <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix%2A>.  
  
 I criteri di terminazione includono:  
  
1.  <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> \- Tempo massimo di attesa di risposte dai servizi in una rete.La durata predefinita è 20 secondi.  
  
2.  <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> \- Numero massimo di risposte da attendere.Se le risposte <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> vengono ricevute prima della scadenza specificata dalla proprietà <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A>, l'operazione di ricerca termina.  
  
## FindResponse  
 <xref:System.ServiceModel.Discovery.FindResponse> dispone di una proprietà della raccolta <xref:System.ServiceModel.Discovery.FindResponse.Endpoints%2A> che contiene qualsiasi replica inviata da servizi corrispondenti sulla rete.Se nessun servizio invia una risposta, la raccolta è vuota.Se uno o più servizi inviano una risposta, ogni replica viene archiviata in un oggetto <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> che contiene l'indirizzo, il contratto e alcune informazioni aggiuntive sul servizio.  
  
 Nell'esempio seguente viene mostrato come eseguire un'operazione di ricerca nel codice.  
  
```  
// Create DiscoveryClient  
DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
// Create FindCriteria  
FindCriteria findCriteria = new FindCriteria(typeof(IPrinterService));  
findCriteria.Scopes.Add(new Uri("http://www.contoso.com/building1/floor1"));  
findCriteria.Duration = TimeSpan.FromSeconds(10);   
  
// Find ICalculatorService endpoints              
FindResponse findResponse = discoveryClient.Find(findCriteria);  
  
Console.WriteLine("Found {0} ICalculatorService endpoint(s).", findResponse.Endpoints.Count)  
  
```  
  
## Vedere anche  
 [Panoramica di WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Utilizzo del canale client di individuazione](../../../../docs/framework/wcf/feature-details/using-the-discovery-client-channel.md)   
 [Individuazione con ambiti](../../../../docs/framework/wcf/samples/discovery-with-scopes-sample.md)   
 [Ricerca asincrona](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md)   
 [Di base](../../../../docs/framework/wcf/samples/basic-sample.md)