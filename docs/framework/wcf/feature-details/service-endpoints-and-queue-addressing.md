---
title: "Mapping fra gli endpoint di servizio e l&#39;indirizzamento delle code | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7d2d59d7-f08b-44ed-bd31-913908b83d97
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Mapping fra gli endpoint di servizio e l&#39;indirizzamento delle code
Questo argomento descrive come i client indirizzano i servizi che leggono da code e il mapping fra gli endpoint di servizio e le code.Come promemoria, l'illustrazione seguente mostra la distribuzione standard delle applicazioni [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in coda.  
  
 ![Diagramma delle applicazioni in coda](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Distributed\-Queue\-Figure")  
  
 Per inviare il messaggio al servizio, il client indirizza il messaggio alla coda di destinazione.Per leggere i messaggi da questa coda, il servizio imposta il proprio indirizzo di attesa sulla coda di destinazione.L'indirizzamento di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sugli URI \(Uniform Resource Identifier\), mentre i nomi di coda del sistema di accodamento dei messaggi \(MSMQ\) non si basano sugli URI.È pertanto essenziale comprendere come utilizzare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per indirizzare le code create in MSMQ.  
  
## Indirizzamento di MSMQ  
 Nel sistema MSMQ le code vengono identificate tramite nomi di percorso e di formato.I percorsi specificano un nome host e un elemento `QueueName`.Fra il nome host e l'elemento `QueueName` è inoltre previsto l'elemento facoltativo `Private$`. Tale elemento indica una coda privata non pubblicata nel servizio di directory Active Directory.  
  
 I nomi di percorso vengono associati a elementi "FormatNames" per determinare aspetti aggiuntivi dell'indirizzo, compresi il routing e il protocollo di trasferimento del servizio di gestione delle code.Questo servizio supporta due protocolli di trasferimento: il protocollo MSMQ nativo e il protocollo SOAP Reliable Messaging Protocol \(SRMP\).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sui nomi di percorso e di formato di MSMQ, vedere il [documento informativo sull'accodamento dei messaggi](http://go.microsoft.com/fwlink/?LinkId=94837) \(la pagina potrebbe essere in inglese\).  
  
## Associazione NetMsmqBinding e indirizzamento del servizio  
 Quando si indirizza un messaggio a un servizio, lo schema contenuto nell'URI viene scelto in base al trasporto utilizzato per le comunicazioni.Ogni trasporto in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] presenta uno schema univoco.Lo schema deve riflettere le caratteristiche del trasporto utilizzato per le comunicazioni,ad esempio net.tcp, net.pipe, HTTP e così via.  
  
 Il trasporto in coda del sistema MSMQ in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] espone uno schema net.msmq.Tutti i messaggi indirizzati utilizzando lo schema net.msmq vengono inviati utilizzando l'associazione `NetMsmqBinding` sul canale del trasporto in coda del sistema MSMQ.  
  
 L'indirizzamento di una coda in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sul modello seguente:  
  
 net.msmq: \/\/ \<*host\-name*\> \/ \[private\/\] \<*queue\-name*\>  
  
 Dove:  
  
-   \<*host\-name*\> è il nome del computer che ospita la coda di destinazione.  
  
-   L'elemento facoltativo \[private\]viene utilizzato quando si indirizza una coda di destinazione privata.Per indirizzare una coda pubblica è necessario non specificare \[private\].Si noti che, a differenza dei percorsi MSMQ, nel modello URI di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non è presente il simbolo "$".  
  
-   \<*queue\-name*\> è il nome della coda.Il nome della coda può riferirsi anche a una coda secondaria.Pertanto, \<*queue\-name*\> \= \<*name\-of\-queue*\>\[;*sub\-queue\-name*\].  
  
 Esempio 1: per indirizzare una coda privata PurchaseOrders ospitata nel computer abc presso adatum.com, l'URI da utilizzare è net.msmq:\/\/abc.adatum.com\/private\/PurchaseOrders.  
  
 Esempio 2: per indirizzare una coda pubblica AccountsPayable ospitata nel computer def presso adatum.com, l'URI da utilizzare è net.msmq:\/\/def.adatum.com\/AccountsPayable.  
  
 L'indirizzo della coda viene utilizzato dal listener come URI di ascolto da cui leggere i messaggi.In altre parole, l'indirizzo della coda è equivalente alla porta di ascolto del socket TCP.  
  
 Un endpoint che legge da una coda deve specificare l'indirizzo della coda utilizzando lo stesso schema specificato in precedenza per l'apertura di ServiceHost.Per alcuni esempi, vedere [Associazione Net MSMQ](../../../../docs/framework/wcf/samples/net-msmq-binding.md) e [Message Queuing Integration Binding Samples](http://msdn.microsoft.com/it-it/997d11cb-f2c5-4ba0-9209-92843d4d0e1a).  
  
### Contratti multipli in una coda  
 I messaggi di una coda possono implementare più contratti.In questo caso, per leggere ed elaborare tutti i messaggi, è essenziale applicare uno degli approcci seguenti:  
  
-   Specificare un endpoint per un servizio che implementa tutti i contratti.Si tratta dell'approccio consigliato.  
  
-   Specificare più endpoint con contratti diversi, garantendo tuttavia che tutti gli endpoint utilizzino lo stesso oggetto `NetMsmqBinding`.La logica di distribuzione di ServiceModel utilizza una message pump che legge i messaggi dal canale di trasporto e quindi li distribuisce. Questa procedura, una volta completata, consente di ottenere il demultiplexing dei messaggi verso vari endpoint in base al contratto.Una message pump viene creata per una coppia URI di ascolto\/associazione.L'indirizzo della coda viene utilizzato dal listener in coda come URI di ascolto.Se si configurano tutti gli endpoint in modo da utilizzare lo stesso oggetto di associazione è possibile garantire che il sistema utilizzi un'unica message pump per leggere il messaggio e quindi eseguirne il demultiplexing verso gli endpoint appropriati in base al contratto.  
  
### Messaggistica SRMP  
 Come già indicato, è possibile utilizzare il protocollo SRMP per i trasferimenti fra code.Questo approccio in genere viene utilizzato quando un trasporto HTTP trasmette i messaggi fra la coda di trasmissione e la coda di destinazione.  
  
 Per utilizzare il protocollo di trasferimento SRMP è necessario indirizzare i messaggi tramite lo schema degli URI net.msmq, come già menzionato, nonché impostare la proprietà `QueueTransferProtocol` dell'associazione `NetMsmqBinding` su SRMP o su SRMP protetto.  
  
 La specifica della proprietà `QueueTransferProtocol` è una funzionalità di solo invioe rappresenta un'indicazione del tipo di protocollo di trasferimento fra code da utilizzare nel client.  
  
### Utilizzo di Active Directory  
 MSMQ supporta l'integrazione con Active Directory.Quando si installa MSMQ con l'opzione di integrazione con Active Directory, il computer deve appartenere a un dominio Windows.Active Directory viene utilizzato per pubblicare code di individuazione, dette *code pubbliche*.Quando si indirizza una coda, il relativo indirizzo può essere risolto utilizzando Active Directory.Questo approccio è analogo all'utilizzo di Domain Name System \(DNS\) per risolvere l'indirizzo IP di un nome di rete.La proprietà `UseActiveDirectory` dell'associazione `NetMsmqBinding` è un valore booleano che indica se il canale in coda deve utilizzare Active Directory per risolvere l'URI della coda.Per impostazione predefinita, questa proprietà è impostata su `false`.Se la proprietà `UseActiveDirectory` è impostata su `true`, il canale in coda utilizza Active Directory per convertire l'URI net.msmq:\/\/ nel nome di formato.  
  
 La proprietà `UseActiveDirectory` è rilevante solo per i client che stanno inviando un messaggio, in quanto tale proprietà viene utilizzata per risolvere l'indirizzo della coda durante la fase di invio dei messaggi.  
  
### Mapping fra gli URI net.msmq e i nomi di formato di MSMQ  
 Il canale in coda gestisce il mapping fra i nomi degli URI net.msmq forniti al canale e i nomi di formato di MSMQ.La tabella seguente riepiloga le regole di mapping.  
  
|Indirizzo di coda basato sugli URI WCF|Impostazione della proprietà UseActiveDirectory|Impostazione della proprietà QueueTransferProtocol|Nomi di formato di MSMQ risultanti|  
|--------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|----------------------------------------|  
|Net.msmq:\/\/\<nome\-computer\>\/private\/abc|False \(impost. predef.\)|Native \(impost. predef.\)|DIRECT\=OS:nome\-computer\\private$\\abc|  
|Net.msmq:\/\/\<nome\-computer\>\/private\/abc|False|SRMP|DIRECT\=http:\/\/computer\/msmq\/private$\/abc|  
|Net.msmq:\/\/\<nome\-computer\>\/private\/abc|True|Native|PUBLIC\=guid \(GUID della coda\)|  
  
### Lettura dei messaggi dalla coda dei messaggi non recapitabili o dalla coda dei messaggi non elaborabili  
 Per leggere i messaggi da una coda di messaggi non elaborabili che è una coda secondaria della coda di destinazione, aprire l'elemento `ServiceHost` con l'indirizzo della coda secondaria.  
  
 Esempio: un servizio che legge dalla coda di messaggi non elaborabili della coda privata PurchaseOrders nel computer locale presenta l'indirizzo net.msmq:\/\/localhost\/private\/PurchaseOrders;poison.  
  
 Per leggere messaggi da una coda transazionale di sistema di messaggi non recapitabili, l'URI deve presentarsi nel formato: net.msmq:\/\/localhost\/system$;DeadXact.  
  
 Per leggere messaggi da una coda non transazionale di sistema di messaggi non recapitabili, l'URI deve presentarsi nel formato: net.msmq:\/\/localhost\/system$;DeadLetter.  
  
 Quando si utilizza una coda di messaggi non recapitabili personalizzata, si noti che questa coda deve trovarsi nel computer locale.Ne consegue che l'URI della coda deve attenersi al formato:  
  
 net.msmq: \/\/localhost\/ \[private\/\]  \<*custom\-dead\-letter\-queue\-name*\>.  
  
 Un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] verifica che tutti i messaggi che riceve siano stati indirizzati alla coda specifica su cui è in attesa.Se un messaggio viene rilevato in una coda a cui non era destinato, tale messaggio non viene elaborato dal servizio.Si tratta di un problema che i servizi in attesa di una coda di messaggi non recapitabili devono affrontare, poiché questo tipo di coda contiene messaggi che in realtà erano destinati altrove.Per leggere i messaggi di una coda di messaggi non recapitabili o non elaborabili occorre utilizzare un comportamento `ServiceBehavior` con il parametro <xref:System.ServiceModel.AddressFilterMode>.Per un esempio, vedere [Code di messaggi non recapitabili](../../../../docs/framework/wcf/samples/dead-letter-queues.md).  
  
## Associazione MsmqIntegrationBinding e indirizzamento del servizio  
 L'associazione `MsmqIntegrationBinding` viene utilizzata per comunicare con le applicazioni MSMQ tradizionali.Per facilitare l'interoperazione con le applicazioni MSMQ esistenti, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta solo l'indirizzamento del nome di formato.Di conseguenza, i messaggi inviati tramite questa associazione devono attenersi allo schema degli URI seguente:  
  
 msmq.formatname:\<*MSMQ\-format\-name*\>\>  
  
 Il nome\-formato\-MSMQ presenta il formato specificato da MSMQ nel [documento informativo sull'accodamento dei messaggi](http://go.microsoft.com/fwlink/?LinkId=94837) \(la pagina potrebbe essere in inglese\).  
  
 Si noti che quando si ricevono messaggi da una coda tramite l'associazione `MsmqIntegrationBinding` è possibile utilizzare soltanto i nomi di formato Direct e, se è stata scelta l'opzione di integrazione con Active Directory, i nomi di formato pubblici e privati.È tuttavia consigliabile utilizzare i nomi di formato Direct.In [!INCLUDE[wv](../../../../includes/wv-md.md)], ad esempio, l'utilizzo di qualsiasi altro nome di formato comporta un errore, poiché il sistema tenta di aprire una coda secondaria che tuttavia può essere aperta solo tramite i nomi di formato Direct.  
  
 Quando si esegue l'indirizzamento tramite il protocollo SRMP utilizzando l'associazione `MsmqIntegrationBinding` non occorre aggiungere \/msmq\/ nel nome di formato Direct per consentire ai servizi Internet Information Services \(IIS\) di eseguire la distribuzione.Esempio: quando si indirizza una coda abc utilizzando il protocollo SRMP, anziché DIRECT\=http:\/\/adatum.com\/msmq\/private$\/abc è necessario utilizzare DIRECT\=http:\/\/adatum.com\/private$\/abc.  
  
 Si noti che non è possibile utilizzare l'indirizzamento net.msmq:\/\/ con l'associazione `MsmqIntegrationBinding`.Poiché l'associazione `MsmqIntegrationBinding` supporta l'indirizzamento del nome di formato MSMQ in formato libero, è possibile utilizzare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizza questa associazione per utilizzare le funzionalità di multicast e di lista di distribuzione di MSMQ.Un'eccezione è la specifica dell'elemento `CustomDeadLetterQueue` quando si utilizza l'associazione `MsmqIntegrationBinding`.Analogamente al caso di specifica dell'elemento quando si utilizza l'associazione `NetMsmqBinding`, tale elemento deve presentare il formato net.msmq:\/\/.  
  
## Vedere anche  
 [Sito Web che ospita un'applicazione in coda](../../../../docs/framework/wcf/feature-details/web-hosting-a-queued-application.md)