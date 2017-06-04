---
title: "Limitazione della distribuzione di messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b5ec4b8-1ce9-45ef-bb90-2c840456bcc1
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Limitazione della distribuzione di messaggi
In base alla progettazione, il canale peer è una rete di trasmissione.Il relativo modello di flooding di base prevede la distribuzione di ogni messaggio inviato da qualsiasi membro di una rete a tutti gli altri membri di quella stessa rete.Questa soluzione è ideale nelle situazioni in cui tutti i messaggi generati da un membro sono attinenti e utili a tutti gli altri membri, ad esempio in una chat.Tuttavia, molte applicazioni hanno occasionalmente la necessità di limitare la distribuzione dei messaggi.Ad esempio, se un nuovo membro si aggiunge a una rete e desidera recuperare l'ultimo messaggio inviato attraverso di essa, non è necessario che questa richiesta venga propagata a ogni membro della rete.È possibile limitare la richiesta ai router adiacenti oppure applicare un filtro ai messaggi generati in locale.I messaggi possono anche essere inviati a un singolo nodo della rete.In questo argomento viene illustrato come utilizzare il conteggio hop, un filtro di propagazione dei messaggi, un filtro locale o una connessione diretta per controllare il modo in cui i messaggi vengono inoltrati attraverso la rete. Vengono inoltre fornite linee guida generali per la scelta dell'approccio più appropriato.  
  
## Conteggi hop  
 Il concetto di `PeerHopCount` è simile a quello di durata \(TTL, Time\-To\-Live\) utilizzato nel protocollo IP.Il valore di `PeerHopCount` viene collegato a un'istanza del messaggio e specifica il numero di volte in cui un messaggio deve essere inoltrato prima di essere eliminato.Ogni volta che un messaggio viene ricevuto da un client del canale peer, il client esamina il messaggio per verificare se `PeerHopCount` è specificato.In caso affermativo, il client diminuisce il valore del conteggio hop di uno prima di inoltrare il messaggio ai nodi adiacenti.Quando un client riceve un messaggio con un valore del conteggio hop pari a zero, il client elabora il messaggio, ma non lo inoltra ai router adiacenti.  
  
 Il conteggio hop può essere inserito in un messaggio aggiungendo `PeerHopCount` come attributo alla proprietà o al campo pertinente nell'implementazione della classe del messaggio.È possibile impostarlo su un valore specifico prima di inviare il messaggio nella rete.Il conteggio hop consente quindi di limitare la distribuzione dei messaggi nella rete in caso di necessità, evitando potenzialmente la duplicazione non necessaria dei messaggi.Ciò si rivela utile nei casi in cui la rete contiene una quantità elevata di dati ridondanti oppure per l'invio di un messaggio a router immediatamente adiacenti o all'interno di un numero ridotto di hop.  
  
-   Per frammenti di codice e informazioni correlate, vedere [Blog sul canale peer](http://go.microsoft.com/fwlink/?LinkID=114531) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=114531\).  
  
## Filtro di propagazione dei messaggi  
 `MessagePropagationFilter` può essere utilizzato per il controllo personalizzato del flood di messaggi, in particolare quando il contenuto del messaggio o altri scenari specifici determinano una propagazione.Il filtro è responsabile delle decisioni sulla propagazione di ogni messaggio che passa attraverso il nodo.Questa situazione si verifica sia per i messaggi creati in altri punti della rete e ricevuti dal nodo sia per i messaggi creati dall'applicazione.Il filtro accede sia al messaggio che alla sua origine, pertanto le decisioni relative all'inoltro o all'eliminazione del messaggio possono basarsi sulle informazioni complete disponibili.  
  
 <xref:System.ServiceModel.PeerMessagePropagationFilter> è una classe astratta di base con una sola funzione, <xref:System.ServiceModel.PeerMessagePropagationFilter.ShouldMessagePropagate%2A>.Il primo argomento della chiamata al metodo passa una copia completa del messaggio.Qualsiasi modifica apportata al messaggio non influisce sul messaggio effettivo.L'ultimo argomento della chiamata al metodo identifica l'origine del messaggio \(`PeerMessageOrigination.Local` o `PeerMessageOrigination.Remote`\).Le implementazioni concrete di questo metodo devono restituire una costante dall'enumerazione <xref:System.ServiceModel.PeerMessagePropagation> che indica che il messaggio deve essere inoltrato all'applicazione locale \(`Local`\), a client remoti \(`Remote`\), a entrambi \(`LocalAndRemote`\) o a nessuna delle parti \(`None`\).È possibile applicare questo filtro accedendo all'oggetto `PeerNode` corrispondente e specificando un'istanza della classe del filtro di propagazione derivata nella proprietà `PeerNode.MessagePropagationFilter`.Assicurarsi che il filtro di propagazione sia collegato prima di aprire il canale peer.  
  
-   Per frammenti di codice e informazioni correlate, vedere [Blog sul canale peer](http://go.microsoft.com/fwlink/?LinkID=114532) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=114532\).  
  
## Contatto di un singolo nodo nella rete  
 È possibile contattare un singolo nodo in una rete configurando un filtro locale o una connessione diretta.  
  
 Se ogni nodo di una rete dispone di un ID singolo, è possibile specificare un ID di destinazione nell'implementazione del messaggio.È possibile configurare un filtro locale scrivendo una funzione nel contratto di messaggio che consenta la visualizzazione del messaggio solo al nodo corrente se l'ID corrisponde a all'ID di destinazione specificato.La rete trasporta il messaggio, di conseguenza è possibile evitare il sovraccarico della configurazione di una nuova connessione.Viene tuttavia registrata una perdita di efficienza poiché il messaggio viene inviato molte volte attraverso la rete.Questa soluzione è adeguata per l'invio di messaggi a singoli membri di una rete, a condizione che i messaggi non siano di dimensioni eccessive o troppo frequenti.  
  
 Per connessioni durevoli e a larghezza di banda elevata, sono preferibili le connessioni dirette.È possibile inviare informazioni sulla connessione sulla rete e successivamente configurare una connessione diretta a scelta per inviare e ricevere messaggi.  
  
## Scelta di un approccio per limitare la distribuzione di messaggi  
 Quando si rileva uno scenario in cui è necessario limitare la distribuzione di messaggi, è opportuno porsi le seguenti domande:  
  
-   **Chi** deve ricevere il messaggio?Solo un nodo adiacente?Un nodo in un'altra posizione della rete?Metà della rete?  
  
-   **Con quale frequenza** verrà inviato questo messaggio?  
  
-   Che tipo di **larghezza di banda** verrà utilizzata da questo messaggio?  
  
 Le risposte a queste domande possono essere utili per stabilire se utilizzare un conteggio hop, un filtro di propagazione dei messaggi, un filtro locale o una connessione diretta.Si considerino le seguenti linee guida generali:  
  
-   **Chi**  
  
    -   *Nodo singolo*: filtro locale o connessione diretta.  
  
    -   *Router adiacenti entro una determinata distanza*: PeerHopCount.  
  
    -   *Sottoinsieme complesso della rete*: MessagePropagationFilter.  
  
-   **Con quale frequenza**  
  
    -   *Frequenza elevata*: connessione diretta, PeerHopCount, MessagePropagationFilter.  
  
    -   *Frequenza occasionale*: filtro locale.  
  
-   **Utilizzo della larghezza di banda**  
  
    -   *Elevato*: connessione diretta, meno consigliabile l'utilizzo di MessagePropagationFilter o di un filtro locale.  
  
    -   *Limitato*: qualsiasi soluzione, probabilmente la connessione diretta non è necessaria.  
  
## Vedere anche  
 [Creazione di un'applicazione del canale peer](../../../../docs/framework/wcf/feature-details/building-a-peer-channel-application.md)