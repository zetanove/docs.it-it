---
title: "Accesso ai servizi tramite client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8329832-bf66-4064-9034-bf39f153fc2d
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Accesso ai servizi tramite client
Le applicazioni client devono creare, configurare e usare oggetti client o canale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per comunicare con i servizi.  Nell'argomento [Panoramica dei client WCF](../../../../docs/framework/wcf/wcf-client-overview.md) viene fornita una panoramica degli oggetti e dei passaggi coinvolti nella creazione e nell'utilizzo di oggetti client e canale.  
  
 In questo argomento vengono fornite informazioni dettagliate su alcuni dei problemi relativi ad applicazioni client e oggetti client e canale, che possono essere utili a seconda dello scenario.  
  
## Panoramica  
 In questo argomento vengono descritti il comportamento e i problemi relativi a:  
  
-   Durata di canali e sessioni.  
  
-   Gestione delle eccezioni.  
  
-   Problemi che causano blocchi.  
  
-   Inizializzazione interattiva dei canali.  
  
### Durata di canali e sessioni  
 Le applicazioni [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] includono due categorie di canali, ovvero i canali di datagramma e quelli con sessione.  
  
 Si definisce di *datagramma* un canale in cui tutti i messaggi non sono correlati.  Con un canale di datagramma, l'eventuale esito negativo di un'operazione di input o di output non ha di norma alcun effetto sulla successiva operazione ed è possibile riutilizzare lo stesso canale.   Ne consegue che i canali di datagramma non hanno in genere esito negativo.  
  
 I canali *con sessione* sono invece canali con una connessione all'altro endpoint.  I messaggi in una sessione su uno dei lati vengono sempre correlati alla stessa sessione sull'altro lato.  Inoltre, perché una sessione possa essere considerata riuscita, entrambi i partecipanti a essa devono concordare sul fatto che i requisiti della conversazione siano stati soddisfatti.  In caso contrario, il canale con sessione può avere esito negativo.  
  
 Aprire i client in modo esplicito o implicito chiamando la prima operazione.  
  
> [!NOTE]
>  Tentare di rilevare esplicitamente i canali con sessione in errore non è in genere utile, poiché il momento in cui si riceve la notifica dipende dall'implementazione della sessione.  Poiché, ad esempio, la classe <xref:System.ServiceModel.NetTcpBinding?displayProperty=fullName> \(con la sessione affidabile disattivata\) fa emergere la sessione della connessione TCP, se si è in ascolto dell'evento <xref:System.ServiceModel.ICommunicationObject.Faulted?displayProperty=fullName> sul servizio o sul client, è probabile che si riceva una notifica immediata in caso di errore di rete.  Le sessioni affidabili \(stabilite da associazioni in cui la classe <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=fullName> è attivata\) sono però progettate per isolare i servizi da piccoli errori di rete.  Se la sessione può essere ristabilita entro un periodo di tempo ragionevole, la stessa associazione, configurata per sessioni affidabili, potrebbe non generare errori fino a quando l'interruzione non dura per un periodo di tempo più lungo.  
  
 La maggior parte delle associazioni fornite dal sistema \(che espongono canali al livello di applicazione\) usa sessioni per impostazione predefinita, diversamente dall'associazione <xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName>.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Uso di sessioni](../../../../docs/framework/wcf/using-sessions.md).  
  
### Utilizzo corretto delle sessioni  
 Le sessioni offrono un modo per sapere se l'intero scambio di messaggi è completo e se entrambi i lati lo considerano riuscito.  È consigliabile che un'applicazione chiamante apra il canale, lo utilizzi e lo chiuda all'interno di un unico blocco try.  Se un canale di sessione è aperto, il metodo <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=fullName> viene chiamato una volta e la chiamata viene restituita correttamente, la sessione ha esito positivo.  Per esito positivo si intende, in questo caso, che tutto il recapito garantisce che l'associazione specificata è stata soddisfatta e che l'altro lato non ha chiamato <xref:System.ServiceModel.ICommunicationObject.Abort%2A?displayProperty=fullName> sul canale prima di chiamare <xref:System.ServiceModel.ICommunicationObject.Close%2A>.  
  
 Nella sezione seguente viene fornito un esempio di tale approccio client.  
  
### Gestione delle eccezioni  
 La gestione di eccezioni nelle applicazioni client è semplice.  Se un canale viene aperto, usato e chiuso all'interno di un blocco try, la conversazione ha avuto esito positivo, a meno che non venga generata un'eccezione.  In genere, se viene generata un'eccezione, la conversazione viene interrotta.  
  
> [!NOTE]
>  Non è consigliabile usare l'istruzione `using` \(`Using` in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\),  poiché la fine dell'istruzione `using` può causare eccezioni che possono mascherare altre eccezioni che potrebbe essere necessario conoscere.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Prevenzione dei problemi con l'istruzione Using](../../../../docs/framework/wcf/samples/avoiding-problems-with-the-using-statement.md).  
  
 Nell'esempio di codice seguente viene illustrato il modello client consigliato usando un blocco try\/catch e non l'istruzione `using`.  
  
 [!code-csharp[FaultContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
 [!code-vb[FaultContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]  
  
> [!NOTE]
>  La verifica del valore della proprietà <xref:System.ServiceModel.ICommunicationObject.State%2A?displayProperty=fullName> è una race condition e non è consigliabile per determinare se riutilizzare o chiudere un canale.  
  
 I canali di datagramma non hanno mai esito negativo anche se si verificano eccezioni quando vengono chiusi.  Inoltre, i client non duplex la cui autenticazione mediante conversazione protetta non riesce generano di norma un'eccezione <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=fullName>.  Tuttavia, se il client duplex che usa una conversazione protetta non viene autenticato, riceve un'eccezione <xref:System.TimeoutException?displayProperty=fullName>.  
  
 Per altre informazioni sull'utilizzo di informazioni sugli errori a livello di applicazione, vedere [Specifica e gestione di errori in contratti e servizi](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).  In [Eccezioni previste](../../../../docs/framework/wcf/samples/expected-exceptions.md) vengono descritte le eccezioni previste e viene illustrato in che modo gestirle.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come gestire gli errori durante lo sviluppo di canali, vedere [Gestione di eccezioni ed errori](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md).  
  
### Blocco dei client e prestazioni  
 Quando un'applicazione chiama in modo sincrono un'operazione request\-reply, il client si blocca fino a quando non viene ricevuto un valore restituito o non viene generata un'eccezione \(ad esempio, <xref:System.TimeoutException?displayProperty=fullName>\).  Si tratta di un comportamento simile al comportamento locale.  Quando un'applicazione richiama in modo sincrono un'operazione su un oggetto client o un canale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], il client non viene restituito fino a quando il livello del canale non riesce a scrivere i dati nella rete o fino a quando non viene generata un'eccezione.  Sebbene il modello di scambio di messaggi unidirezionale \(specificato contrassegnando un'operazione con la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=fullName> impostata su `true`\) possa aumentare la capacità di risposta di alcuni client, le operazioni unidirezionali possono anche creare blocchi, a seconda dell'associazione e dei messaggi già inviati.  Le operazioni unidirezionali riguardano esclusivamente lo scambio di messaggi.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Servizi unidirezionali](../../../../docs/framework/wcf/feature-details/one-way-services.md).  
  
 I grandi blocchi di dati possono rallentare l'elaborazione dei client, indipendentemente dal modello di scambio di messaggi.  Per informazioni su come gestire questi problemi, vedere [Dati di grandi dimensioni e flussi](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md).  
  
 Se l'applicazione deve eseguire altre operazioni durante il completamento di un'operazione, è consigliabile creare una coppia di metodi asincroni sull'interfaccia di contratto del servizio implementata dal client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Il modo più semplice per ottenere questo risultato consiste nell'usare l'opzione `/async` nell'[Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  Per un esempio, vedere [Procedura: chiamare operazioni del servizio in modo asincrono](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sul miglioramento delle prestazioni dei client, vedere [Applicazioni client di livello intermedio](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md).  
  
### Abilitazione dell'utente alla selezione dinamica di credenziali  
 L'interfaccia <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> consente alle applicazioni di visualizzare un'interfaccia utente che consente all'utente di scegliere le credenziali con cui viene creato un canale prima dell'avvio dei timer di timeout.  
  
 Gli sviluppatori di applicazioni possono usare un'interfaccia <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> inserita in due modi.  L'applicazione client può chiamare il metodo <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=fullName> o <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=fullName> \(o una versione asincrona\) prima di aprire il canale \(approccio *esplicito*\) o chiamare la prima operazione \(approccio *implicito*\).  
  
 Se si usa l'approccio implicito, l'applicazione deve chiamare la prima operazione su un'estensione <xref:System.ServiceModel.ClientBase%601> o <xref:System.ServiceModel.IClientChannel>.  Se chiama un elemento diverso dalla prima operazione, viene generata un'eccezione.  
  
 Se si usa l'approccio esplicito, l'applicazione deve eseguire i passaggi seguenti nell'ordine rappresentato:  
  
1.  Chiamare <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=fullName> o <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=fullName> \(o una versione asincrona\).  
  
2.  Quando gli inizializzatori restituiscono un valore, chiamare il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A> sull'oggetto <xref:System.ServiceModel.IClientChannel> o sull'oggetto <xref:System.ServiceModel.IClientChannel> restituito dalla proprietà <xref:System.ServiceModel.ClientBase%601.InnerChannel%2A?displayProperty=fullName>.  
  
3.  Chiamare le operazioni.  
  
 È consigliabile che le applicazioni di alta qualità controllino il processo dell'interfaccia utente adottando l'approccio esplicito.  
  
 Le applicazioni che usano l'approccio implicito richiamano gli inizializzatori dell'interfaccia utente, ma se l'utente dell'applicazione non risponde entro il periodo di timeout di invio dell'associazione, viene generata un'eccezione quando viene restituita l'interfaccia utente.  
  
## Vedere anche  
 [Servizi duplex](../../../../docs/framework/wcf/feature-details/duplex-services.md)   
 [Procedura: accedere a servizi con un contratto unidirezionale o request\/reply](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)   
 [Procedura: accedere ai servizi con un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)   
 [Procedura: accedere a WSE 3.0 Service](../../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)   
 [Procedura: usare ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)   
 [Procedura: chiamare operazioni del servizio in modo asincrono](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)   
 [Applicazioni client di livello intermedio](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)