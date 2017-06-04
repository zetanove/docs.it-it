---
title: "Panoramica delle sessioni affidabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: a7fc4146-ee2c-444c-82d4-ef6faffccc2d
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Panoramica delle sessioni affidabili
La messaggistica affidabile SOAP di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] garantisce l'affidabilità del trasferimento di messaggi end\-to\-end tra endpoint SOAP.Svolge questa funzione su reti inaffidabili risolvendo gli errori del trasporto e gli errori a livello di messaggio SOAP.In particolare, assicura il recapito basato sulla sessione, singolo e \(facoltativamente\) ordinato dei messaggi inviati su intermediari SOAP o del trasporto.Il recapito basato sulla sessione raggruppa i messaggi in una sessione con ordinamento facoltativo dei messaggi.  
  
 Di seguito vengono descritte le caratteristiche di una sessione affidabile, viene indicato come e quando utilizzarla e come assicurarne la protezione.  
  
## Sessioni affidabili WCF  
 Le sessioni affidabili [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono un'implementazione della messaggistica affidabile SOAP, nel modo definito dal protocollo WS\-ReliableMessaging.  
  
 La messaggistica affidabile SOAP di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce una sessione end\-to\-end affidabile tra due endpoint, indipendentemente dal numero o dal tipo di intermediari che separano gli endpoint di messaggistica.In questo modo vengono inclusi tutti gli intermediari del trasporto che non utilizzano SOAP \(ad esempio proxy HTTP\) o gli intermediari che utilizzano SOAP \(ad esempio bridge o router basati su SOAP\) necessari per il flusso dei messaggi tra gli endpoint.Un canale di sessione affidabile supporta la comunicazione "interattiva", in modo che i servizi connessi da tale canale vengano eseguiti simultaneamente e possano scambiare ed elaborare messaggi in condizioni di bassa latenza, ovvero con intervalli di tempo relativamente brevi.Questo accoppiamento implica l'avanzamento o l'errore di tutti i componenti, tra cui non esiste isolamento.  
  
 Una sessione affidabile maschera due tipi di errori:  
  
-   Gli errori a livello di messaggio SOAP, che includono messaggi persi o duplicati e messaggi che arrivano in un ordine diverso da quello di invio.  
  
-   Gli errori del trasporto.  
  
 Una sessione affidabile implementa il protocollo WS\-ReliableMessaging e una finestra di trasferimento in memoria, per mascherare gli errori a livello di messaggio SOAP, e ristabilisce le connessioni in caso di errori del trasporto.  
  
 Una sessione affidabile assicura per i messaggi SOAP ciò che TCP assicura per i pacchetti IP.Una connessione socket TCP garantisce il trasferimento singolare in ordine dei pacchetti IP tra i nodi.Il canale affidabile garantisce lo stesso tipo di trasferimento affidabile, ma differisce dall'affidabilità del socket TCP nei modi seguenti:  
  
-   L'affidabilità è a livello di messaggio SOAP e non è relativa a un pacchetto di byte di dimensioni arbitrarie.  
  
-   L'affidabilità si realizza in modo neutro rispetto al trasporto e non solo per il trasferimento tramite TCP.  
  
-   L'affidabilità non è legata a una particolare sessione del trasporto \(ad esempio, la sessione fornita da una connessione TCP\) e può utilizzare contemporaneamente o in sequenza più sessioni del trasporto per tutta la durata della sessione affidabile.  
  
-   La sessione affidabile viene stabilita tra gli endpoint SOAP mittente e destinatario, indipendentemente dal numero di connessioni del trasporto necessarie per la connettività tra di essi.In breve, l'affidabilità TCP termina dove termina la connessione del trasporto, mentre una sessione affidabile offre affidabilità end\-to\-end.  
  
## Sessioni affidabili e associazioni  
 Come menzionato in precedenza, una sessione affidabile è neutra rispetto al trasporto e come tale può essere implementata su molti trasporti.Inoltre, una sessione affidabile può essere stabilita su molti modelli di scambio di messaggi, quali, ad esempio, quello request\/reply o quello duplex.La sessione affidabile [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene quindi esposta come proprietà di un set di associazioni.  
  
 È possibile utilizzare una sessione affidabile su endpoint che utilizzano:  
  
-   Associazioni standard del trasporto basate su HTTP:  
  
    -   `WsHttpBinding` e contratti unidirezionali o request\/reply di esposizione.  
  
    -   Utilizzabili quando si utilizza una sessione affidabile su un contratto di servizio semplice unidirezionale o request\/reply.  
  
    -   `WsDualHttpBinding` e contratti unidirezionali, request\/reply o duplex di esposizione.  
  
    -   `WsFederationHttpBinding` e contratti unidirezionali o request\/reply di esposizione.  
  
-   Associazioni standard del trasporto basate su TCP:  
  
    -   `NetTcpBinding` e contratti unidirezionali, request\/reply o duplex di esposizione.  
  
 È inoltre possibile utilizzare una sessione affidabile su qualsiasi altra associazione creando un'associazione personalizzata, ad esempio un'associazione HTTPS \(per ulteriori informazioni sui problemi, vedere la sezione "Sessioni affidabili e protezione" più avanti in questo argomento\) o named pipe.  
  
 Una sessione affidabile può essere impilata su diversi tipi di canali sottostanti con conseguente variazione della forma del canale della sessione affidabile risultante.Sul client e sul server, il tipo di canale di sessione affidabile supportato dipende dal tipo di canale sottostante utilizzato.Nella tabella seguente sono elencati i tipi di canale di sessione supportati sul client come funzione del canale sottostante.  
  
|Tipi di canale di sessione affidabile supportati \(valori supportati di `TChannel` per un determinato tipo di canale sottostante\)|`IRequestChannel`|`IRequestSessionChanne`l|`IDuplexChannel`|`IDuplexSessionChannel`|  
|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------|------------------------------|----------------------|-----------------------------|  
|`IOutputSessionChannel`|Sì|Sì|Sì|Sì|  
|`IRequestSessionChannel`|Sì|Sì|No|No|  
|`IDuplexSessionChannel`|No|No|Sì|Sì|  
  
 I tipi di canale supportati sono i valori disponibili per il valore del parametro generico `TChannel` passato nel metodo <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelFactory%60%601%28System.ServiceModel.Channels.BindingContext%29>.  
  
 Nella tabella seguente sono elencati i tipi di canale di sessione supportati sul server come funzione del canale sottostante.  
  
|Tipi di canale di sessione affidabile supportati \(valori supportati di `TChannel` per un determinato tipo di canale sottostante\)|`IReplyChannel`|`IReplySessionChannel`|`IDuplexChannel`|`IDuplexSessionChannel`|  
|----------------------------------------------------------------------------------------------------------------------------------------|---------------------|----------------------------|----------------------|-----------------------------|  
|`IInputSessionChannel`|Sì|Sì|Sì|Sì|  
|`IReplySessionChannel`|Sì|Sì|No|No|  
|`IDuplexSessionChannel`|No|No|Sì|Sì|  
  
 I tipi di canale supportati sono i valori disponibili per il valore del parametro generico `TChannel` passato nel metodo <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelListener%60%601%28System.ServiceModel.Channels.BindingContext%29>.  
  
## Sessioni affidabili e protezione  
 La protezione di una sessione affidabile è importante per assicurare che le parti che comunicano \(servizio e client\) vengano autenticate e che i messaggi scambiati nella sessione non vengano manomessi.Inoltre, è importante assicurare l'integrità di ogni singola sessione affidabile.Una sessione affidabile viene protetta mediante l'associazione a un contesto di sicurezza rappresentato e gestito da un canale di sessione di sicurezza.Il canale di sicurezza fornisce una sessione di sicurezza.Per proteggere il messaggio nella sessione affidabile vengono quindi utilizzati i token di sicurezza scambiati durante la creazione della sessione.  
  
 Quando la sessione affidabile viene stabilita su TCP\-S, la sessione TCP viene associata alla sessione affidabile e la protezione del trasporto assicura che anche la protezione sia associata alla sessione affidabile.In questo caso, la riesecuzione della connessione viene disattivata.  
  
 L'unica eccezione si verifica in caso di utilizzo di HTTPS.La sessione SSL \(Secure Sockets Layer\) non è associata alla sessione affidabile.Questo rappresenta una minaccia, poiché le sessioni che condividono un contesto di sicurezza \(la sessione SSL\) non sono protette le une alle altre; l'effettiva incidenza di tale minaccia dipende però dall'applicazione.  
  
## Utilizzo di sessioni affidabili  
 Per utilizzare sessioni affidabili [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], creare un endpoint con un'associazione che supporti una sessione affidabile.Utilizzare una delle associazioni fornite dal sistema che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] offre con la sessione affidabile attivata o creare un'associazione personalizzata con questa funzione.Le associazioni definite dal sistema che supportano e attivano una sessione affidabile per impostazione predefinita includono:  
  
-   <xref:System.ServiceModel.WSDualHttpBinding>  
  
 Le associazioni fornite dal sistema che supportano una sessione affidabile come opzione ma non ne attivano una per impostazione predefinita includono:  
  
-   <xref:System.ServiceModel.WSHttpBinding>  
  
-   <xref:System.ServiceModel.WSFederationHttpBinding>  
  
-   <xref:System.ServiceModel.NetTcpBinding>  
  
 Per un esempio di creazione di un'associazione personalizzata, vedere [Procedura: creare un'associazione di sessione affidabile personalizzata con HTTPS](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md).  
  
 Per una descrizione delle associazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che supportano sessioni affidabili, vedere [Associazioni fornite dal sistema](../../../../docs/framework/wcf/system-provided-bindings.md).  
  
## Situazioni relative all'utilizzo di sessioni affidabili  
 È importante capire quando utilizzare sessioni affidabili nell'applicazione.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta sessioni affidabili tra endpoint che sono contemporaneamente attive e operative.Se l'applicazione richiede che uno degli endpoint non sia disponibile per un periodo di tempo, è possibile utilizzare code per realizzare l'affidabilità.  
  
 Se lo scenario richiede la connessione di due endpoint tramite TCP, quest'ultimo può risultare sufficiente a garantire lo scambio affidabile dei messaggi, sebbene non sia necessario utilizzare una sessione affidabile; TCP assicura che i pacchetti arrivino in ordine e una sola volta.  
  
 Se lo scenario ha una qualsiasi delle caratteristiche seguenti, è necessario considerare seriamente l'utilizzo di una sessione affidabile:  
  
-   Intermediari SOAP, ad esempio router SOAP.  
  
-   Intermediari proxy o bridge di trasporto.  
  
-   Connettività intermittente.  
  
-   Sessioni su HTTP.  
  
## Vedere anche  
 [Uso di associazioni per configurare servizi e client](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Sessioni affidabili WS](../../../../docs/framework/wcf/samples/ws-reliable-session.md)