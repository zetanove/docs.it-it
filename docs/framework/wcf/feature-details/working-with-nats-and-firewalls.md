---
title: "Utilizzo di conversioni NAT e firewall | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "firewall [WCF]"
  - "NAT [WCF]"
ms.assetid: 74db0632-1bf0-428b-89c8-bd53b64332e7
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Utilizzo di conversioni NAT e firewall
Fra il client e il server di una connessione di rete spesso non esiste un percorso diretto di comunicazione.I pacchetti vengono filtrati, instradati, analizzati e trasformati sia nei computer endpoint sia nei computer intermedi della rete.Le conversioni Network Address Translation \(NAT\) e i firewall sono esempi di applicazioni intermedie che in genere partecipano a una comunicazione di rete.  
  
 La presenza di conversioni NAT e di firewall influisce sul funzionamento dei trasporti e dei modelli di scambio dei messaggi \(MEP, Message Exchange Pattern\) di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questo argomento descrive il funzionamento delle conversioni NAT e dei firewall nelle topologie di rete più comuni.Vengono inoltre forniti consigli su come rendere le applicazioni più affidabili quando si utilizzano determinate combinazioni di trasporti e di modelli MEP di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] qualora nella rete siano presenti conversioni NAT e firewall.  
  
## Effetti delle conversioni NAT sulle comunicazioni  
 Il protocollo NAT è stato creato per consentire a più computer di condividere un solo indirizzo IP esterno.Un protocollo NAT di nuovo mapping di porta associa un indirizzo IP interno e la relativa porta di una connessione a un indirizzo IP esterno avente un nuovo un numero di porta.Il nuovo numero di porta consente al protocollo NAT di correlare il traffico di ritorno alla comunicazione originale.Molti utenti privati attualmente dispongono di un indirizzo IP a cui è possibile instradare pacchetti solo privatamente e che utilizza una conversione NAT per svolgere l'instradamento globale dei pacchetti.  
  
 Benché le conversioni NAT non costituiscano un limite di sicurezza,le configurazioni NAT più comuni impediscono che i computer interni vengano indirizzati in modo diretto.Oltre a proteggere i computer interni da connessioni indesiderate, questo meccanismo rende difficile la scrittura di applicazioni server che devono restituire dati al client in modo asincrono.Il protocollo NAT riscrive gli indirizzi contenuti nei pacchetti in modo che le connessioni sembrino provenire dal computer NAT.Ciò impedisce al server di aprire una connessione di ritorno al client.Se il server utilizza l'indirizzo percepito del client, la connessione non riesce perché l'indirizzo client non può essere oggetto di routing pubblico.Se il server utilizza l'indirizzo NAT, la connessione non riesce perché non esiste alcuna applicazione in attesa sul computer associato a tale indirizzo.  
  
 Alcune conversioni NAT supportano la configurazione di regole di inoltro per consentire ai computer esterni di connettersi a un determinato computer interno.Le istruzioni per configurare le regole di inoltro variano a seconda della conversione NAT utilizzata e, per la maggior parte delle applicazioni, è consigliabile evitare di chiedere agli utenti finali di modificare le configurazioni NAT.Molti utenti finali non possono né desiderano modificare la propria configurazione NAT per un'applicazione specifica.  
  
## Effetti dei firewall sulle comunicazioni  
 Un *firewall* è un software o un dispositivo hardware che consente o impedisce il passaggio di un flusso di dati in base a regole specifiche.I firewall possono essere configurati in modo da esaminare flussi di traffico in ingresso e\/o in uscita.Inoltre, i firewall forniscono un limite di sicurezza per la rete a livello perimetrale oppure a livello di host endpoint.Gli utenti aziendali in genere utilizzano un firewall per proteggere i propri server da attacchi dannosi.Da quando in [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] è stata introdotta la funzionalità di firewall personale, l'utilizzo di firewall si è rapidamente diffuso anche fra gli utenti privati.È di conseguenza molto probabile che una determinata connessione presenti un firewall su una o su entrambe le estremità allo scopo di controllare i flussi di pacchetti.  
  
 Esiste una vasta gamma di tipi di firewall, ognuno avente livelli specifici di complessità e di efficienza di analisi.I firewall meno complessi applicano regole basate sugli indirizzi e sulle porte di origine e di destinazione dei pacchetti.I firewall più intelligenti possono prendere decisioni anche in base al contenuto dei pacchetti.I firewall di questo tipo presentano una notevole flessibilità di configurazione e pertanto vengono spesso utilizzati per proteggere applicazioni aventi funzionalità specifiche.  
  
 I firewall utilizzati nei computer degli utenti privati vengono in genere configurati in modo da accettare soltanto le connessioni in ingresso provenienti dai computer con cui l'utente ha precedentemente stabilito una connessione in uscita.I firewall utilizzati nei computer aziendali vengono in genere configurati in modo da accettare soltanto le connessioni in ingresso a un determinato gruppo di porte.Ad esempio, un firewall può essere configurato in modo da accettare soltanto le connessioni in ingresso alle porte 80 e 443 allo scopo di consentire il funzionamento dei servizi basati su HTTP e HTTPS.Sia per gli utenti aziendali sia per gli utenti privati sono disponibili firewall gestiti che consentono agli utenti o ai processi attendibili del computer di modificare la configurazione del firewall.I firewall gestiti sono più diffusi fra gli utenti privati, in quanto in questo caso non esiste alcun criterio aziendale di controllo dell'utilizzo di rete.  
  
## Utilizzo di Teredo  
 Teredo è una tecnologia di transizione IPv6 che consente l'indirizzabilità diretta dei computer protetti tramite NAT.Questa tecnologia si basa sull'utilizzo di un server che può essere oggetto di routing pubblico e globale allo scopo di segnalare le connessioni potenzialmente disponibili.Il server Teredo offre al client e al server dell'applicazione un punto comune di incontro presso il quale poter scambiare informazioni relative alla connessione.I computer richiedono quindi un indirizzo Teredo temporaneo da utilizzare per il tunneling dei pacchetti attraverso la rete esistente.Affinché Teredo sia supportato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è necessario abilitare il supporto per IPv6 e Teredo nel sistema operativo.In [!INCLUDE[wxp](../../../../includes/wxp-md.md)] e nei sistemi operativi successivi Teredo è supportato.In [!INCLUDE[wv](../../../../includes/wv-md.md)] e nei sistemi operativi successivi IPv6 è supportato per impostazione predefinita, pertanto è sufficiente abilitare Teredo.In [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] e [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] è necessario che l'utente abiliti il supporto per IPv6 e Teredo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la pagina relativa alla [panoramica di Teredo](http://go.microsoft.com/fwlink/?LinkId=87571).  
  
## Scelta di un trasporto e di un MEP  
 La scelta di un trasporto e di un MEP prevede tre passaggi:  
  
1.  Analisi dell'indirizzabilità dei computer endpoint:a differenza dei server aziendali, gli utenti finali in genere non sono indirizzabili in modo diretto. Ciò è dovuto alla presenza di meccanismi NAT.Se entrambi gli endpoint sono protetti da una conversione NAT, ad esempio nel caso di scenari peer\-to\-peer tra utenti finali, l'utilizzo di una tecnologia quale Teredo per fornire l'indirizzabilità potrebbe risultare particolarmente utile.  
  
2.  Analisi del protocollo e dei vincoli di porta dei computer endpoint:i server aziendali sono in genere protetti da firewall avanzati che bloccano molte porte.Tuttavia, spesso la porta 80 è aperta per consentire il traffico HTTP e la porta 443 è aperta per consentire il traffico HTTPS.Per gli utenti finali è meno probabile che esistano vincoli di porta. È tuttavia possibile che tali utenti siano protetti da un firewall che consenta solo connessioni in uscita.Alcuni firewall consentono alle applicazioni dell'endpoint di gestire l'apertura selettiva delle connessioni.  
  
3.  Determinazione dei trasporti e dei MEP consentiti dai vincoli di indirizzabilità e di porta della rete.  
  
 Una topologia comune per le applicazioni client\-server prevede client protetti tramite NAT senza Teredo, un firewall che controlla solo i flussi in uscita e un server direttamente indirizzabile tramite un firewall avanzato.In questo scenario è opportuno scegliere un trasporto TCP con un MEP duplex oppure un trasporto HTTP con un MEP request\/reply.Una topologia comune per le applicazioni peer\-to\-peer prevede la protezione di entrambi gli endpoint tramite NAT e firewall.In questo scenario e negli scenari in cui non si conosce la topologia di rete, tenere presente i seguenti consigli:  
  
-   Evitare di utilizzare trasporti duali.Un trasporto duale apre più connessioni, il che riduce le probabilità di riuscire a stabilire una connessione.  
  
-   Supportare la creazione di canali di ritorno per le connessioni di origine.L'utilizzo dei canali di ritorno, che ad esempio caratterizza il trasporto TCP duplex, comporta l'apertura di meno connessioni, il che aumenta le probabilità di riuscire a stabilire una connessione.  
  
-   Utilizzare un servizio raggiungibile per la registrazione degli endpoint oppure per l'inoltro del traffico.L'utilizzo di un servizio di connessione globalmente raggiungibile, ad esempio un server Teredo, aumenta notevolmente le probabilità di riuscire a stabilire una connessione quando la topologia di rete presenta vincoli oppure non è nota.  
  
 Nelle tabelle seguenti vengono riportati i MEP unidirezionale, request\/reply e duplex nonché i trasporti TCP standard, TCP con Teredo e HTTP standard e duale in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
|Indirizzabilità|Diretta server|Diretta server con attraversamento NAT|NAT server|NAT server con attraversamento NAT|  
|---------------------|--------------------|--------------------------------------------|----------------|----------------------------------------|  
|Diretta client|Qualsiasi trasporto e MEP|Qualsiasi trasporto e MEP|Non supportato.|Non supportato.|  
|Diretta client con attraversamento NAT|Qualsiasi trasporto e MEP.|Qualsiasi trasporto e MEP.|Non supportato.|TCP con Teredo e qualsiasi MEP.In [!INCLUDE[wv](../../../../includes/wv-md.md)] è disponibile un'opzione di configurazione a livello di computer per supportare HTTP con Teredo.|  
|NAT client|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Non supportato.|Non supportato.|  
|NAT client con attraversamento NAT|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Tutti tranne HTTP duale e qualsiasi MEP.I modelli MEP duplex richiedono il trasporto TCP.Il trasporto TCP duale richiede Teredo.In [!INCLUDE[wv](../../../../includes/wv-md.md)] è disponibile un'opzione di configurazione a livello di computer per supportare HTTP con Teredo.|Non supportato.|TCP con Teredo e qualsiasi MEP.In [!INCLUDE[wv](../../../../includes/wv-md.md)] è disponibile un'opzione di configurazione a livello di computer per supportare HTTP con Teredo.|  
  
|Restrizioni del firewall|Server aperto|Server con firewall gestito|Server con firewall solo per HTTP|Server con firewall solo per flussi in uscita|  
|------------------------------|-------------------|---------------------------------|---------------------------------------|---------------------------------------------------|  
|Client aperto|Qualsiasi trasporto e MEP.|Qualsiasi trasporto e MEP.|Qualsiasi trasporto HTTP e MEP.|Non supportato.|  
|Client con firewall gestito|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Qualsiasi trasporto HTTP e MEP.|Non supportato.|  
|Client con firewall solo per HTTP|Qualsiasi trasporto HTTP e MEP.|Qualsiasi trasporto HTTP e MEP.|Qualsiasi trasporto HTTP e MEP.|Non supportato.|  
|Client con firewall solo per flussi in uscita|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Qualsiasi trasporto non duale e MEP.I modelli MEP duplex richiedono il trasporto TCP.|Qualsiasi trasporto HTTP e qualsiasi MEP non duplex.|Non supportato.|