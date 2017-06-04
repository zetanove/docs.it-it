---
title: "Estensione dei client | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "estensioni del proxy [WCF]"
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Estensione dei client
In un'applicazione chiamante, il livello del modello di servizio è responsabile della conversione delle chiamate ai metodi contenute nel codice dell'applicazione in messaggi in uscita, del loro inserimento nei canali sottostanti, della conversione dei risultati in valori restituiti e parametri out nel codice dell'applicazione e della restituzione dei risultati al chiamante.Le estensioni del modello di servizi modificano o implementano il comportamento e le funzioni dell'esecuzione o della comunicazione relativamente a funzionalità del client o del dispatcher, comportamenti personalizzati, intercettazione di messaggi e parametri e altre funzionalità di estensibilità.  
  
 In questo argomento viene illustrato come utilizzare le classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.ClientOperation> in un'applicazione client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per modificare il comportamento di esecuzione predefinito di un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] o per intercettare o modificare messaggi, parametri o valori restituiti prima o dopo il loro invio o recupero dal livello del canale.Per ulteriori informazioni sull'estensione della fase di esecuzione del servizio, vedere [Estensione di dispatcher](../../../../docs/framework/wcf/extending/extending-dispatchers.md).Per ulteriori informazioni sui comportamenti che modificano e inseriscono oggetti di personalizzazione nella fase di esecuzione del client, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## Client  
 In un client, un oggetto o un canale client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] converte le chiamate ai metodi in messaggi in uscita e i messaggi in ingresso in risultati di operazioni che vengono restituiti all'applicazione chiamante.Per ulteriori informazioni sui tipi di client, vedere [Architettura client WCF](../../../../docs/framework/wcf/feature-details/client-architecture.md).  
  
 I tipi di client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dispongono di tipi in fase di esecuzione che gestiscono questa funzionalità a livello di endpoint e di operazione.Quando in un'applicazione viene eseguita una chiamata a un'operazione, la classe <xref:System.ServiceModel.Dispatcher.ClientOperation> converte gli oggetti in uscita in un messaggio, elabora gli intercettori, conferma che la chiamata in uscita è conforme al contratto di destinazione e passa il messaggio in uscita alla classe <xref:System.ServiceModel.Dispatcher.ClientRuntime>, che è responsabile della creazione e della gestione dei canali in uscita \(e dei canali in ingresso in caso di servizi duplex\), della gestione dell'elaborazione supplementare dei messaggi in uscita \(ad esempio la modifica dell'intestazione\), dell'elaborazione degli intercettori del messaggio in entrambe le direzioni e dell'instradamento delle chiamate duplex in ingresso all'oggetto <xref:System.ServiceModel.Dispatcher.DispatchRuntime> sul lato client appropriato.Le classi <xref:System.ServiceModel.Dispatcher.ClientOperation> e <xref:System.ServiceModel.Dispatcher.ClientRuntime> forniscono servizi simili quando i messaggi \(compresi gli errori\) vengono restituiti al client.  
  
 Queste due classi di runtime costituiscono l'estensione principale per personalizzare l'elaborazione degli oggetti e dei canali client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].La classe <xref:System.ServiceModel.Dispatcher.ClientRuntime> consente agli utenti di intercettare ed estendere l'esecuzione del client in tutti i messaggi del contratto.La classe <xref:System.ServiceModel.Dispatcher.ClientOperation> consente agli utenti di intercettare ed estendere l'esecuzione del client per tutti i messaggi di una determinata operazione.  
  
 Per la modifica delle proprietà o l'inserimento di personalizzazioni, si utilizzano i comportamenti del contratto, dell'endpoint e dell'operazione.Per ulteriori informazioni su come utilizzare tali tipi di comportamenti per eseguire personalizzazioni del runtime del client, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## Scenari  
 Esistono vari motivi per estendere il sistema client, tra cui:  
  
-   Convalida di messaggi personalizzata.È possibile che un utente desideri imporre che un messaggio sia valido per un certo schema.A tale scopo, implementare l'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> e assegnare l'implementazione alla proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A>.Per alcuni esempi, vedere [Procedura: ispezionare o modificare i messaggi sul client](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md) e [Procedura: ispezionare o modificare i messaggi sul client](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
-   Registrazione di messaggi personalizzata.È possibile che un utente desideri controllare e registrare un set di messaggi dell'applicazione che passano attraverso un endpoint.Questa operazione può essere eseguita anche con le interfacce degli intercettori di messaggi.  
  
-   Trasformazioni di messaggi personalizzate.Anziché modificare il codice dell'applicazione, è possibile che l'utente desideri applicare determinate trasformazioni al messaggio nel runtime \(ad esempio per il controllo delle versioni\).Anche in questo caso, l'operazione può essere eseguita con le interfacce degli intercettori di messaggi.  
  
-   Modello di dati personalizzato.È possibile che un utente desideri un modello di dati o di serializzazione diverso da quelli supportati per impostazione predefinita in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(ovvero oggetti <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>, <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> e <xref:System.ServiceModel.Channels.Message?displayProperty=fullName>\).A questo scopo, è possibile implementare le interfacce dei formattatori di messaggi.Per ulteriori informazioni, vedere l'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=fullName> e la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=fullName>.  
  
-   Convalida di parametri personalizzata.È possibile che un utente desideri imporre che i parametri tipizzati siano validi \(a differenza di XML\).A questo scopo, è possibile utilizzare le interfacce di controllo dei parametri.Per un esempio, vedere [Procedura: controllare o modificare i parametri](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md) o [Convalida client](../../../../docs/framework/wcf/samples/client-validation.md).  
  
### Utilizzo della classe ClientRuntime  
 La classe <xref:System.ServiceModel.Dispatcher.ClientRuntime> è un punto di estensibilità a cui è possibile aggiungere oggetti di estensione che intercettano i messaggi ed estendono il comportamento del client.Gli oggetti di intercettamento possono elaborare tutti i messaggi di un contratto specifico, elaborare solo i messaggi di operazioni particolari, eseguire l'inizializzazione di un canale personalizzata e implementare altri comportamenti dell'applicazione client personalizzati.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> restituisce l'oggetto runtime di invio per i client di callback avviati dal servizio.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> accetta un oggetto selettore dell'operazione personalizzato.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> consente di aggiungere un inizializzatore del canale che può controllare o modificare il canale client.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> ottiene una raccolta di oggetti <xref:System.ServiceModel.Dispatcher.ClientOperation> alla quale è possibile aggiungere intercettatori di messaggi personalizzati che forniscono la funzionalità specifica ai messaggi di quell'operazione.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> consente a un'applicazione di disattivare alcune intestazioni di indirizzamento automatico per controllare direttamente l'indirizzamento.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> imposta il valore della destinazione del messaggio a livello di trasporto per supportare gli intermediari e altri scenari.  
  
-   La proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> ottiene una raccolta di oggetti <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> alla quale è possibile aggiungere intercettori di messaggi personalizzati per tutti i messaggi che passano attraverso un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Esistono inoltre altre proprietà che recuperano le informazioni del contratto:  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 Se il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] duplex, nelle proprietà seguenti vengono inoltre recuperate le informazioni del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sul callback:  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
-   <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 Per estendere l'esecuzione del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] attraverso un intero client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], esaminare le proprietà disponibili sulla classe <xref:System.ServiceModel.Dispatcher.ClientRuntime> per verificare se la modifica di una proprietà o l'implementazione di un'interfaccia e la relativa aggiunta a una proprietà crea la funzionalità desiderata.Una volta scelta una particolare estensione da compilare, inserirla nella proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime> appropriata implementando un comportamento del client che fornisca accesso alla classe <xref:System.ServiceModel.Dispatcher.ClientRuntime> quando viene richiamato.  
  
 Per inserire oggetti di estensione personalizzati in una raccolta, è possibile utilizzare un comportamento dell'operazione \(un oggetto che implementa <xref:System.ServiceModel.Description.IOperationBehavior>\), un comportamento del contratto \(un oggetto che implementa <xref:System.ServiceModel.Description.IContractBehavior>\) o un comportamento dell'endpoint \(un oggetto che implementa <xref:System.ServiceModel.Description.IEndpointBehavior>\).L'oggetto del comportamento da installare viene aggiunto alla raccolta appropriata di comportamenti a livello di codice, in modo dichiarativo \(implementando un attributo personalizzato\) o implementando un oggetto <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> personalizzato per consentire al comportamento di essere inserito utilizzando un file di configurazione dell'applicazione.Per informazioni dettagliate, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Per esempi che illustrano l'intercettazione in un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: ispezionare o modificare i messaggi sul client](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md).  
  
### Utilizzo della classe ClientOperation  
 Nella classe <xref:System.ServiceModel.Dispatcher.ClientOperation> è possibile eseguire modifiche della fase di esecuzione del client e questa classe rappresenta il punto di inserimento per le estensioni personalizzate nell'ambito di una sola operazione del servizio.\(Per modificare il comportamento della fase di esecuzione del client per tutti i messaggi di un contratto, utilizzare la classe <xref:System.ServiceModel.Dispatcher.ClientRuntime>\).  
  
 Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> per individuare l'oggetto <xref:System.ServiceModel.Dispatcher.ClientOperation> che rappresenta un'operazione specifica del servizio.Le proprietà seguenti consentono di inserire oggetti personalizzati nel sistema client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> per inserire un'implementazione personalizzata dell'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> di un'operazione o per modificare il formattatore corrente.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> per inserire un'implementazione personalizzata dell'interfaccia <xref:System.ServiceModel.Dispatcher.IParameterInspector> o per modificare l'interfaccia corrente.  
  
 Le proprietà seguenti consentono di modificare il sistema in interazione con il formattatore e i controlli del parametro personalizzati:  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> per controllare la serializzazione di un messaggio in uscita.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> per controllare la deserializzazione di un messaggio in entrata.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> per controllare l'azione WS\-Addressing del messaggio di richiesta.  
  
-   Utilizzare le proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A> e <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> per specificare quali metodi del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono associati a un'operazione asincrona.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> per ottenere una raccolta contenente i tipi che possono comparire negli errori SOAP come tipi di dettaglio.  
  
-   Utilizzare le proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> e <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> per controllare se una sessione viene rispettivamente avviata o eliminata quando viene chiamata l'operazione.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> per controllare se l'operazione è un'operazione unidirezionale.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> per ottenere l'oggetto contenitore <xref:System.ServiceModel.Dispatcher.ClientRuntime>.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> per ottenere il nome dell'operazione.  
  
-   Utilizzare la proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> per controllare quale metodo viene mappato all'operazione.  
  
 Per estendere l'esecuzione del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in una sola operazione del servizio, esaminare le proprietà disponibili sulla classe <xref:System.ServiceModel.Dispatcher.ClientOperation> per verificare se la modifica di una proprietà o l'implementazione di un'interfaccia e la relativa aggiunta a una proprietà crea la funzionalità desiderata.Una volta scelta una particolare estensione da compilare, inserirla nella proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation> appropriata implementando un comportamento del client che fornisca accesso alla classe <xref:System.ServiceModel.Dispatcher.ClientOperation> quando viene richiamato.All'interno di tale comportamento è quindi possibile modificare la proprietà <xref:System.ServiceModel.Dispatcher.ClientRuntime> in base alle esigenze.  
  
 In genere, è sufficiente l'implementazione di un comportamento dell'operazione \(un oggetto che implementa l'interfaccia <xref:System.ServiceModel.Description.IOperationBehavior>\), ma è anche possibile utilizzare comportamenti dell'endpoint e del contratto per ottenere lo stesso risultato individuando la classe <xref:System.ServiceModel.Description.OperationDescription> per una particolare operazione e allegandovi il comportamento.Per informazioni dettagliate, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Per utilizzare il comportamento personalizzato dalla configurazione, installare il comportamento utilizzando un gestore della sezione di configurazione dei comportamenti personalizzati.È inoltre possibile installare il comportamento creando un attributo personalizzato.  
  
 Per esempi che illustrano l'intercettazione in un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Procedura: controllare o modificare i parametri](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Dispatcher.ClientRuntime>   
 <xref:System.ServiceModel.Dispatcher.ClientOperation>   
 [Procedura: ispezionare o modificare i messaggi sul client](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-messages-on-the-client.md)   
 [Procedura: controllare o modificare i parametri](../../../../docs/framework/wcf/extending/how-to-inspect-or-modify-parameters.md)