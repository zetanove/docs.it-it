---
title: "Cache PNRP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 270068d9-1b6b-4eb9-9e14-e02326bb88df
caps.latest.revision: 4
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 4
---
# Cache PNRP
I peer cache \(PNRP\) di protocollo di risoluzione dei nomi sono raccolte locali dell'endpoint peer in modo algoritmico selezionati gestiti sul peer.  
  
## Inizializzazione della cache di PNRP  
 Per inizializzare la cache di PNRP, o del record del nome del peer, quando un nodo peer viene avviata, un nodo può utilizzare i metodi seguenti:  
  
-   Le voci della cache persistente che erano presenti quando il nodo è stato interrotto vengono caricate dall'archivio del disco rigido.  
  
-   Se un'applicazione utilizza l'infrastruttura di collaborazione P2P, le informazioni di collaborazione sono disponibili in gestione del contatto per tale nodo.  
  
## Ridimensionare risoluzione dei nomi peer con una cache a più livelli  
 Per mantenere le dimensioni della cache di PNRP piccole, i nodi peer utilizzano una cache a più livelli, in cui ogni livello contiene un numero massimo di voci.  Ogni livello nella cache rappresenta una un decimo di più piccolo parte dello spazio del numero ID di PNRP \(2<sup>256</sup>\).  Il livello più basso nella cache contiene un PNRP localmente registrato ID e altri PNRP ID che sono numericamente da.  Mentre un livello della cache viene riempito con un massimo di 20 voci, un nuovo livello inferiore viene creato.  Il numero massimo di livelli nella cache è l'ordine del10registro \(numero totale di PNRP ID di cloud computing\).  Ad esempio, per un cloud globale con 100 milioni di PNRP ID, esiste un massimo di 8 \(\=log10\(100.000.000\) livelli nella cache e in un simile numero di hop per risolvere un PNRP ID durante la risoluzione dei nomi.  Questo meccanismo consente un hash distribuito alla tabella per il quale un PNRP arbitrario ID può essere risolta inoltrando i messaggi di richiesta di PNRP al peer seguente\- più vicino fino a trovare il peer con CPA corrispondente.  
  
 Per assicurarsi che la soluzione possa essere completata, ogni volta che un nodo aggiunge una voce al livello inferiore della cache, sommerge una copia della voce a tutti i nodi nel livello della cache.  
  
 Le voci della cache vengono aggiornate nel tempo.  Le voci della cache che non sono aggiornate vengono rimossi dalla cache.  Il risultato è che l'hash distribuito alla tabella di PNRP ID è basata sugli endpoint attivi, a differenza del DNS in cui indirizzi i record e il protocollo DNS non fornisce alcuna garanzia che il nodo associato all'indirizzo sia attivamente in rete.  
  
## Altri cache di PNRP  
 Un altro archivio persistente è la cache locale.  Oltre agli altri oggetti necessari per attività di PNRP, può includere i record associati a una sessione di cloud o di collaborazione di PNRP che in modo sicuro viene pubblicata e sincronizzata tra tutti i membri di cloud.  Questo archivio replicato rappresenta la visualizzazione dei dati di gruppo, che devono essere identici per tutti i membri del gruppo.  Tecnicamente, questi oggetti sono non record di per sé, bensì applicazione, presenza e dati dell'oggetto destinati della cache locale.  L'utilizzo di cloud di PNRP garantisce che gli oggetti siano propagati a tutti i nodi in sessione di collaborazione o cloud di PNRP.  La replica record tra i membri di tipo cloud utilizza SSL per fornire la crittografia e l'integrità dei dati.  
  
 Quando un peer unisce un cloud, automaticamente non ricevono i dati locali della cache dal peer host che si connettono; è necessario sottoscrivere il peer host per ottenere gli aggiornamenti dell'applicazione, in presenza e i dati dell'oggetto.  Dopo la sincronizzazione iniziale, i peer resynchronize periodicamente i relativi file ripiegati per assicurarsi che tutti i membri del gruppo hanno sempre la stessa visualizzazione.  La sessione o applicazioni di collaborazione all'interno della sessione di collaborazione è possibile eseguire la stessa funzione.  
  
 Dopo che una sessione di collaborazione ha iniziato a un cloud, le applicazioni possono registrare i peer e iniziare eseguendo le informazioni utilizzando la sicurezza dall'ambito cloud.  Quando un peer unisce un cloud, i meccanismi di sicurezza per il cloud si applicano al peer, offrendo un ambito in cui includere.  I record possono quindi essere pubblicati correttamente nel cloud.  Si noti che l'ambito di cloud non può essere uguale all'ambito di applicazione di collaborazione.  
  
 I peer possono registrare un interesse nella ricezione di oggetti da altri peer.  Quando un oggetto viene aggiornato, l'applicazione di collaborazione viene trasmessa e il nuovo oggetto viene passato a tutti i sottoscrittori dell'applicazione.  Ad esempio, un peer in un'applicazione di chat di gruppo può registrare un interesse nella ricezione di informazioni di applicazione, che lo invieranno tutti i record di chat come dati dell'applicazione.  Ciò consente alle attività di chat del monitor all'interno di cloud.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer>