---
title: "Performance Counters in the .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "performance, .NET Framework applications"
  - "performance counters"
  - "performance monitoring, counters"
ms.assetid: 06a4ae8c-eeb2-4d5a-817e-b1b95c0653e1
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Performance Counters in the .NET Framework
Questo argomento fornisce un elenco di contatori delle prestazioni disponibili in [Performance Monitor](http://technet.microsoft.com/library/cc749249.aspx).  
  
-   [Contatori delle prestazioni per le eccezioni](#exception)  
  
-   [Contatori delle prestazioni per l'interoperabilità](#interop)  
  
-   [JIT (contatori delle prestazioni)](#jit)  
  
-   [Contatori delle prestazioni di caricamento](#loading)  
  
-   [Contatori delle prestazioni di blocchi e thread](#lockthread)  
  
-   [Contatori delle prestazioni di memoria](#memory)  
  
-   [Contatori delle prestazioni della rete](#networking)  
  
-   [Contatori delle prestazioni di sicurezza](#security)  
  
<a name="exception"></a>   
## Contatori delle prestazioni per le eccezioni  
 La categoria delle eccezioni CLR .NET della console Prestazioni include contatori che forniscono informazioni sulle eccezioni generate dall'applicazione.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di eccezioni generate.**|Visualizza il numero totale di eccezioni generate dall'avvio dell'applicazione.  Include sia le eccezioni .NET che quelle non gestite convertite in eccezioni .NET.  Ad esempio, HRESULT restituito dal codice non gestito viene convertito in un eccezione nel codice gestito.<br /><br /> Questo contatore include sia le eccezioni gestite che non gestite.  Le eccezioni rigenerate vengono conteggiate di nuovo.|  
|**N. di eccezioni generate\/sec.**|Visualizza il numero di eccezioni generate al secondo.  Include sia le eccezioni .NET che quelle non gestite convertite in eccezioni .NET.  Ad esempio, HRESULT restituito dal codice non gestito viene convertito in un eccezione nel codice gestito.<br /><br /> Questo contatore include sia le eccezioni gestite che non gestite.  Non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.  Questo contatore è un indicatore di potenziali problemi di prestazioni se viene generato un numero elevato di eccezioni \(\>100\).|  
|**N. di filtri\/sec.**|Visualizza il numero di filtri eccezioni .NET eseguiti al secondo.  Un filtro eccezioni esegue la valutazione a prescindere che l'eccezione sia gestita o meno.<br /><br /> Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**N. di finally\/sec.**|Visualizza il numero di blocchi finally eseguiti al secondo.  Un blocco finally viene eseguito in qualsiasi caso, a prescindere dal modo in cui è stato terminato il blocco try.  Vengono conteggiati solo i blocchi finally eseguiti per un'eccezione. I blocchi finally nei normali percorsi di codice non vengono conteggiati da questo contatore.<br /><br /> Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Throw per profondità catch\/sec.**|Visualizza il numero di stack frame attraversati al secondo, dal frame che ha generato l'eccezione al frame che l'ha gestita.  Il contatore viene reimpostato su zero quando viene immesso un gestore di eccezioni, quindi le eccezioni annidate visualizzano la profondità di stack da gestore a gestore.<br /><br /> Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
  
<a name="interop"></a>   
## Contatori delle prestazioni per l'interoperabilità  
 La categoria di interoperabilità CLR .NET della console Prestazioni include contatori che forniscono informazioni sull'interazione dell'applicazione con i componenti COM, i servizi COM\+ e le librerie dei tipi esterne.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di CCW**|Visualizza il numero corrente di COM Callable Wrapper \(CCW\).  Un CCW è un proxy per un oggetto gestito a cui fa riferimento un client COM non gestito.  Questo contatore indica il numero di oggetti gestiti a cui fa riferimento un codice COM non gestito.|  
|**N. di marshalling**|Visualizza il numero totale di volte in cui è stato eseguito il marshalling di argomenti e valori restituiti dal codice gestito a quello non gestito e viceversa dall'avvio dell'applicazione.  Questo contatore non viene incrementato se gli stub vengono impostati come inline.  Gli stub sono responsabili del marshalling degli argomenti e dei valori restituiti.  In genere gli stub vengono impostati come inline se il sovraccarico del marshalling è ridotto.|  
|**N. di stub**|Visualizza il numero corrente di stub creati da Common Language Runtime.  Gli stub sono responsabili del marshalling di argomenti e valori restituiti dal codice gestito a quello non gestito e viceversa durante una chiamata di interoperabilità COM o una chiamata di pInvoke.|  
|**N. di esportazioni TLB\/sec.**|Riservato per usi futuri.|  
|**N. di importazioni TLB\/sec.**|Riservato per usi futuri.|  
  
<a name="jit"></a>   
## JIT \(contatori delle prestazioni\)  
 La categoria JIT CLR .NET della console Prestazioni include contatori che forniscono informazioni sul codice con compilazione JIT.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di byte IL compilati Just\-In\-Time**|Visualizza il numero totale di byte Microsoft Intermediate Language \(MSIL\) compilati dal compilatore Just\-In\-Time \(JIT\) dall'avvio dell'applicazione.  Questo contatore è equivalente al contatore **N. totale di byte IL compilati Just\-In\-Time**.|  
|**N. di metodi compilati Just\-In\-Time**|Visualizza il numero totale di metodi con compilazione JIT dall'avvio dell'applicazione.  Questo contatore non include metodi con precompilazione JIT.|  
|**% tempo in JIT**|Visualizza la percentuale di tempo trascorso nella compilazione JIT dall'ultima fase di compilazione JIT.  Questo contatore viene aggiornato alla fine di ogni fase di compilazione JIT.  Una fase di compilazione JIT si verifica quando viene compilato un metodo e le relative dipendenze.|  
|**Byte IL compilati Just\-In\-Time\/sec.**|Visualizza il numero di byte MSIL con compilazione JIT al secondo.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Errori JIT standard**|Visualizza il numero massimo di metodi che il compilatore JIT non è riuscito a compilare dall'avvio dell'applicazione.  Questo errore può verificarsi se non è possibile verificare MSIL o se si verifica un errore interno del compilatore JIT.|  
|**N. totale di byte IL compilati Just\-In\-Time**|Visualizza i byte MSIL totali con compilazione JIT dall'avvio dell'applicazione.  Questo contatore è equivalente al contatore **N. di byte IL compilati Just\-In\-Time**.|  
  
<a name="loading"></a>   
## Contatori delle prestazioni di caricamento  
 La categoria di caricamento CLR .NET della console Prestazioni include contatori che forniscono informazioni su assembly, classi e domini applicazione caricati.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**% tempo di caricamento**|Riservato per usi futuri.|  
|**Lunghezza ricerca assembly**|Riservato per usi futuri.|  
|**Byte nell'heap del caricatore**|Visualizza le dimensioni correnti, in byte, della memoria di cui il caricatore di classe esegue il commit in tutti i domini applicazione.  Memoria con commit è lo spazio fisico riservato nel file di paging su disco.|  
|**AppDomain correnti**|Visualizza il numero corrente di domini applicazione caricati nell'applicazione.|  
|**Assembly correnti**|Visualizza il numero corrente di assembly caricati in tutti i domini applicazione dell'applicazione attualmente in esecuzione.  Se l'assembly viene caricato come indipendente dal dominio da più domini applicazione, questo contatore viene incrementato una sola volta.|  
|**Classi attualmente caricate**|Visualizza il numero corrente di classi caricate in tutti gli assembly.|  
|**Frequenza degli AppDomain**|Visualizza il numero di domini applicazione caricati al secondo.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Frequenza degli AppDomain scaricati**|Visualizza il numero di domini applicazione scaricati al secondo.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Frequenza degli assembly**|Visualizza il numero di assembly caricati al secondo in tutti i domini applicazione.  Se l'assembly viene caricato come indipendente dal dominio da più domini applicazione, questo contatore viene incrementato una sola volta.<br /><br /> Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Frequenza delle classi caricate**|Visualizza il numero di classi caricate al secondo in tutti gli assembly.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Frequenza degli errori di caricamento**|Visualizza il numero di classi che non è stato possibile caricare al secondo.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.<br /><br /> Gli errori di caricamento possono verificarsi per diversi motivi, ad esempio un livello di sicurezza non adeguato o un formato non valido.  Per informazioni dettagliate, vedere la guida sulla profilatura di servizi.|  
|**N. totale di errori di caricamento**|Visualizza il numero massimo di classi che non è stato caricato dall'avvio dell'applicazione.<br /><br /> Gli errori di caricamento possono verificarsi per diversi motivi, ad esempio un livello di sicurezza non adeguato o un formato non valido.  Per informazioni dettagliate, vedere la guida sulla profilatura di servizi.|  
|**AppDomain totali**|Visualizza il numero massimo di domini applicazione caricati dall'avvio dell'applicazione.|  
|**AppDomain totali scaricati**|Visualizza il numero totale di domini applicazione scaricati dall'avvio dell'applicazione.  Se un dominio applicazione viene caricato e scaricato più volte, questo contatore viene incrementato ogni volta che viene scaricato il dominio applicazione.|  
|**Assembly totali**|Visualizza il numero totale di assembly caricati dall'avvio dell'applicazione.  Se l'assembly viene caricato come indipendente dal dominio da più domini applicazione, questo contatore viene incrementato una sola volta.|  
|**Totale classi caricate**|Visualizza il numero cumulativo di classi caricate in tutti gli assembly dall'avvio dell'applicazione.|  
  
<a name="lockthread"></a>   
## Contatori delle prestazioni di blocchi e thread  
 La categoria LocksAndThreads CLR .NET della console Prestazioni include contatori che forniscono informazioni sui blocchi e i thread gestiti usati da un'applicazione.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di thread logici correnti**|Visualizza il numero di oggetti thread attualmente gestiti nell'applicazione.  Questo contatore mantiene il conteggio sia dei thread in esecuzione che di quelli arrestati.  Questo contatore non rappresenta una media nel tempo, ma visualizza solo l'ultimo valore osservato.|  
|**N. di thread fisici correnti**|Visualizza il numero di thread del sistema operativo nativo creati e posseduti da Common Language Runtime usati come thread sottostanti per gli oggetti thread gestiti.  Il valore di questo contatore non include thread usati dal runtime durante le operazioni interne. Si tratta di un sottoinsieme dei thread nel processo del sistema operativo.|  
|**N. di thread riconosciuti correnti**|Visualizza il numero di thread attualmente riconosciuti dal runtime.  Questi thread sono associati a un oggetto thread gestito corrispondente.  Il runtime non crea questi thread che, tuttavia, sono stati eseguiti almeno una volta all'interno del runtime.<br /><br /> Vengono rilevati solo i thread univoci. I thread con lo stesso ID immessi di nuovo nel runtime o ricreati dopo la chiusura del thread non vengono conteggiati due volte.|  
|**N. totale di thread riconosciuti**|Visualizza il numero totale di thread riconosciuti dal runtime dall'avvio dell'applicazione.  Questi thread sono associati a un oggetto thread gestito corrispondente.  Il runtime non crea questi thread che, tuttavia, sono stati eseguiti almeno una volta all'interno del runtime.<br /><br /> Vengono rilevati solo i thread univoci. I thread con lo stesso ID immessi di nuovo nel runtime o ricreati dopo la chiusura del thread non vengono conteggiati due volte.|  
|**Frequenza di conflitti\/sec.**|Visualizza la frequenza con cui i thread nel runtime tentano di acquisire un blocco gestito senza riuscirci.|  
|**Lunghezza coda corrente**|Visualizza il numero totale di thread in attesa di acquisire un blocco gestito nell'applicazione.  Questo contatore non rappresenta una media nel tempo, visualizza l'ultimo valore osservato.|  
|**Lunghezza coda\/sec.**|Visualizza il numero di thread al secondo in attesa di acquisire un blocco nell'applicazione.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Lunghezza massima coda**|Visualizza il numero totale di thread in attesa di acquisire un blocco gestito dall'avvio dell'applicazione.|  
|**frequenza dei thread riconosciuti\/sec.**|Visualizza il numero di thread al secondo riconosciuto dal runtime.  Questi thread sono associati a un oggetto thread gestito corrispondente.  Il runtime non crea questi thread che, tuttavia, sono stati eseguiti almeno una volta all'interno del runtime.<br /><br /> Vengono rilevati solo i thread univoci. I thread con lo stesso ID immessi di nuovo nel runtime o ricreati dopo la chiusura del thread non vengono conteggiati due volte.<br /><br /> Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**N. totale di conflitti**|Visualizza il numero totale di volte in cui i thread nel runtime hanno tentato di acquisire un blocco gestito senza riuscirci.|  
  
<a name="memory"></a>   
## Contatori delle prestazioni di memoria  
 La categoria di memoria CLR .NET della console Prestazioni include contatori che forniscono informazioni sul Garbage Collector.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di byte in tutti gli heap**|Visualizza la somma dei contatori **Dimensione heap di generazione 1**, **Dimensione heap di generazione 2**, **Dimensione heap oggetti grandi**.  Questo contatore indica la memoria corrente allocata in byte sugli heap di Garbage Collection.|  
|**N. di handle GC**|Visualizza il numero corrente di handle di Garbage Collection in uso.  Gli handle di Garbage Collection sono handle di risorse esterne a Common Language Runtime e all'ambiente gestito.|  
|**N. di raccolte di generazione 0**|Visualizza il numero di volte in cui gli oggetti di generazione 0 \(ovvero quelli allocati più di recente\) vengono sottoposti a Garbage Collection dall'avvio dell'applicazione.<br /><br /> Una Garbage Collection di generazione 0 si verifica quando la memoria disponibile nella generazione 0 non è sufficiente per soddisfare una richiesta di allocazione.  Questo contatore viene incrementato alla fine di una Garbage Collection di generazione 0.  Le Garbage Collection con generazioni superiori includono tutte quelle con generazioni inferiori.  Questo contatore viene incrementato in modo esplicito quando si verifica una Garbage Collection di generazione superiore \(1 o 2\).<br /><br /> Questo contatore visualizza 'ultimo valore osservato.  Il valore del contatore **Global \_** non è preciso e deve essere ignorato.|  
|**N. di raccolte di generazione 1**|Visualizza il numero di volte in cui che gli oggetti di generazione 1 vengono sottoposti a Garbage Collection dall'avvio dell'applicazione.<br /><br /> Il contatore viene incrementato alla fine di una Garbage Collection di generazione 1.  Le Garbage Collection con generazioni superiori includono tutte quelle con generazioni inferiori.  Questo contatore viene incrementato in modo esplicito quando si verifica una Garbage Collection di generazione superiore \(2\).<br /><br /> Questo contatore visualizza 'ultimo valore osservato.  Il valore del contatore **Global \_** non è preciso e deve essere ignorato.|  
|**N. di raccolte di generazione 2**|Visualizza il numero di volte in cui gli oggetti di generazione 2 vengono sottoposti a Garbage Collection dall'avvio dell'applicazione.  Il contatore viene incrementato alla fine di una Garbage Collection di generazione 2 \(denominata anche Garbage Collection completa\).<br /><br /> Questo contatore visualizza 'ultimo valore osservato.  Il valore del contatore **Global \_** non è preciso e deve essere ignorato.|  
|**N. di GC indotti**|Visualizza il numero massimo di volte in cui è stata eseguita una Garbage Collection a causa di una chiamata esplicita a <xref:System.GC.Collect%2A?displayProperty=fullName>.  È buona norma consentire al Garbage Collector di regolare la frequenza delle proprie raccolte.|  
|**N. di oggetti bloccati**|Visualizza il numero di oggetti bloccati rilevati nell'ultima Garbage Collection.  Un oggetto bloccato è un oggetto che non può essere spostato all'interno della memoria tramite il Garbage Collector.  Tramite questo contatore si tiene traccia degli oggetti bloccati solo negli heap raccolti tramite il Garbage Collector.  Ad esempio, una Garbage Collection di generazione 0 causa l'enumerazione degli oggetti bloccati solo nell'heap di generazione 0.|  
|**N. di blocchi sink in uso**|Viene visualizzato il numero corrente di blocchi di sincronizzazione in uso.  I blocchi di sincronizzazione sono strutture di dati per oggetto allocate per memorizzare le informazioni di sincronizzazione.  Sono contenuti riferimenti deboli a oggetti gestiti e devono essere analizzati dal Garbage Collector.  I blocchi di sincronizzazione non si limitano all'archiviazione di informazioni sulla sincronizzazione, ma possono archiviare anche i metadati di interoperabilità COM.  Questo contatore indica problemi di prestazioni dovuti a un uso intensivo di primitive di sincronizzazione.|  
|**N. totale di byte con commit**|Visualizza la quantità di memoria virtuale, in byte, di cui il Garbage Collector ha attualmente eseguito il commit.  La memoria con commit è la memoria fisica per cui è stato riservato spazio nel file di paging su disco.|  
|**N. totale di byte riservati**|Viene visualizzata la quantità di memoria virtuale, in byte, attualmente riservata al Garbage Collector.  La memoria riservata è lo spazio di memoria virtuale riservato all'applicazione quando non vengono usati il disco o le pagine della memoria principale.|  
|**% di tempo in GC**|Visualizza la percentuale di tempo impiegato per l'esecuzione di una Garbage Collection dopo l'ultimo ciclo di Garbage Collection.  Questo contatore indica in genere il lavoro svolto dal Garbage Collector per raccogliere e comprimere la memoria per conto dell'applicazione.  Questo contatore viene aggiornato solo alla fine di ogni Garbage Collection.  Questo contatore non rappresenta una media. Il valore visualizzato riflette l'ultimo valore osservato.|  
|**Byte allocati\/secondo**|Visualizza il numero di byte al secondo allocati sull'heap di Garbage Collection.  Questo contatore viene aggiornato alla fine di ogni Garbage Collection, non a ogni allocazione.  Questo contatore non rappresenta una media del tempo, ma visualizza la differenza tra i valori osservati per gli ultimi due campioni divisa per la durata dell'intervallo dei campioni.|  
|**Oggetti di finalizzazione esclusi**|Visualizza il numero di oggetti della Garbage Collection che non vengono inclusi in una raccolta perché in attesa di essere finalizzati.  Se questi oggetti contengono riferimenti ad altri oggetti, anche questi saranno esclusi dalla raccolta e non verranno conteggiati da questo contatore.  Il contatore **Memoria di completamento promossa dalla generazione 0** rappresenta tutta la memoria rimasta dopo la finalizzazione.<br /><br /> Questo contatore non è cumulativo, ma viene aggiornato alla fine di ogni Garbage Collection con il conteggio degli oggetti esclusi solo durante la raccolta specificata.  Questo contatore indica il sovraccarico eventualmente sostenuto dall'applicazione a causa della finalizzazione.|  
|**Dimensioni heap di generazione 0**|Visualizza il numero massimo di byte che è possibile allocare nella generazione 0. Non indica il numero corrente di byte allocati nella generazione 0.<br /><br /> Quando le allocazioni eseguite dall'ultima raccolta superano questa dimensione, si verifica una Garbage Collection di generazione 0.  Le dimensioni della generazione 0 vengono regolate dal Garbage Collector e possono essere modificate durante l'esecuzione dell'applicazione.  Alla fine di una raccolta di generazione 0 le dimensioni dell'heap di generazione 0 sono di 0 byte.  Questo contatore indica la dimensione in byte delle allocazioni che richiamano la Garbage Collection di generazione 0 successiva.<br /><br /> Questo contatore viene aggiornato alla fine di una Garbage Collection, non a ogni allocazione.|  
|**Byte promossi di generazione 0\/sec.**|Visualizza il numero di byte al secondo promossi dalla generazione 0 alla generazione 1.  La memoria viene promossa quando non è raccolta dalla Garbage Collection.  Questo contatore è un indicatore degli oggetti di lunga durata creati al secondo.<br /><br /> Questo contatore visualizza la differenza tra i valori osservati negli ultimi due esempi divisa per la durata dell'intervallo di campionamento.|  
|**Dimensione heap di generazione 1**|Visualizza il numero corrente di byte nella generazione 1. Questo contatore non visualizza la dimensione massima della generazione 1.  Gli oggetti non vengono allocati direttamente in questa generazione, ma vengono promossi dalle Garbage Collection di generazione 0.  Questo contatore viene aggiornato alla fine di una Garbage Collection, non a ogni allocazione.|  
|**Byte promossi di generazione 1\/sec.**|Visualizza il numero di byte al secondo promossi dalla generazione 1 alla generazione 2.  In questo contatore non sono inclusi gli oggetti promossi solo perché in attesa di essere finalizzati.<br /><br /> La memoria viene promossa quando non è raccolta dalla Garbage Collection.  Nessun elemento viene promosso dalla generazione 2 perché è quella meno recente.  Questo contatore è un indicatore degli oggetti di durata molto lunga creati al secondo.<br /><br /> Questo contatore visualizza la differenza tra i valori osservati negli ultimi due esempi divisa per la durata dell'intervallo di campionamento.|  
|**Dimensione heap di generazione 2**|Visualizza il numero corrente di byte nella generazione 2.  Gli oggetti non vengono allocati direttamente in questa generazione, ma vengono promossi dalla generazione 1 durante le Garbage Collection di generazione 1 precedenti.  Questo contatore viene aggiornato alla fine di una Garbage Collection, non a ogni allocazione.|  
|**Dimensione heap oggetti grandi**|Visualizza le dimensioni correnti in byte dell'heap oggetti grandi.  Gli oggetti che superano circa 85.000 byte sono considerati oggetti di grandi dimensioni dal Garbage Collector e vengono allocati direttamente in un heap speciale; non vengono promossi da una generazione all'altra.  Questo contatore viene aggiornato alla fine di una Garbage Collection, non a ogni allocazione.|  
|**ID processo**|Viene visualizzato l'ID processo dell'istanza del processo CLR in fase di monitoraggio.|  
|**Memoria di finalizzazione promossa dalla generazione 0**|Visualizza i byte di memoria promossi dalla generazione 0 alla generazione 1 solo perché in attesa di essere completati.  Questo contatore non è cumulativo, ma visualizza il valore rilevato al termine dell'ultima Garbage Collection.|  
|**Memoria promossa dalla generazione 0**|Visualizza i byte di memoria non raccolti dalla Garbage Collection e promossi dalla generazione 0 alla generazione 1.  In questo contatore non sono inclusi gli oggetti promossi solo perché in attesa di essere finalizzati.  Questo contatore non è cumulativo, ma visualizza il valore rilevato al termine dell'ultima Garbage Collection.|  
|**Memoria promossa dalla generazione 1**|Visualizza i byte di memoria non raccolti dalla Garbage Collection e promossi dalla generazione 1 alla generazione 2.  In questo contatore non sono inclusi gli oggetti promossi solo perché in attesa di essere finalizzati.  Questo contatore non è cumulativo, ma visualizza il valore rilevato al termine dell'ultima Garbage Collection.  Questo contatore viene reimpostato su 0 se l'ultima Garbage Collection è stata solo di generazione 0.|  
  
<a name="networking"></a>   
## Contatori delle prestazioni della rete  
 La categoria di rete CLR .NET della console Prestazioni include contatori che forniscono informazioni sui dati che un'applicazione invia e riceve in rete.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**Byte ricevuti**|Il totale cumulativo di byte ricevuti da tutti gli oggetti <xref:System.Net.Sockets.Socket> all'interno di <xref:System.AppDomain> dall'avvio del processo.  Questo numero include i dati e le informazioni sul protocollo non definiti da TCP\/IP.|  
|**Byte inviati**|Il numero cumulativo di byte inviati da tutti gli oggetti <xref:System.Net.Sockets.Socket> all'interno di <xref:System.AppDomain> dall'avvio del processo.  Questo numero include i dati e le informazioni sul protocollo non definiti da TCP\/IP.|  
|**Connessioni stabilite**|Il numero totale di oggetti <xref:System.Net.Sockets.Socket> per tutti i socket di flusso connessi all'interno di <xref:System.AppDomain> dall'avvio del processo.|  
|**Datagrammi ricevuti**|Il numero totale cumulativo di pacchetti di datagrammi ricevuti da tutti gli oggetti <xref:System.Net.Sockets.Socket> all'interno di <xref:System.AppDomain> dall'avvio del processo.|  
|**Datagrammi inviati**|Il numero totale cumulativo di pacchetti di datagrammi inviati da tutti gli oggetti <xref:System.Net.Sockets.Socket> all'interno di <xref:System.AppDomain> dall'avvio del processo.|  
|**Durata media di HttpWebRequest**|Il tempo medio di completamento per tutti gli oggetti <xref:System.Net.HttpWebRequest> terminati nell'ultimo intervallo in <xref:System.AppDomain> dall'avvio del processo.|  
|**Tempo medio coda di HttpWebRequest**|Il tempo medio in coda per tutti gli oggetti <xref:System.Net.HttpWebRequest> usciti dalla coda nell'ultimo intervallo in <xref:System.AppDomain> dall'avvio del processo.|  
|**HttpWebRequest creati\/sec.**|Il numero di oggetti <xref:System.Net.HttpWebRequest> creati al secondo all'interno di <xref:System.AppDomain>.|  
|**HttpWebRequest in coda\/sec.**|Il numero di oggetti <xref:System.Net.HttpWebRequest> aggiunti alla coda al secondo all'interno di <xref:System.AppDomain>.|  
|**HttpWebRequest interrotti\/sec.**|Il numero di oggetti <xref:System.Net.HttpWebRequest> in cui l'applicazione ha chiamato il metodo <xref:System.Net.HttpWebRequest.Abort%2A> al secondo all'interno di <xref:System.AppDomain>.|  
|**HttpWebRequest non riusciti\/sec.**|Il numero di oggetti <xref:System.Net.HttpWebRequest> che hanno ricevuto un codice di stato di errore dal server al secondo all'interno di <xref:System.AppDomain>.|  
  
 Sono supportate diverse classi di contatori delle prestazioni della rete:  
  
-   I contatori evento che misurano il numero di volte in cui si verifica un evento.  
  
-   I contatori dati che misurano la quantità di dati inviati o ricevuti.  
  
-   I contatori di durata che misurano la durata dei diversi processi.  I tempi vengono misurati su ciascun intervallo degli oggetti \(in genere in secondi\) dopo che escono da diversi stati.  
  
-   I contatori per ogni intervallo che misurano il numero di oggetti che stanno effettuando una particolare transizione per intervallo \(in genere al secondo\).  
  
 I contatori delle prestazioni della rete per gli eventi includono quanto segue:  
  
-   **Connessioni stabilite**  
  
-   **Datagrammi ricevuti**  
  
-   **Datagrammi inviati**  
  
 I contatori delle prestazioni forniscono i conteggi dall'avvio del processo.  I conteggi delle connessioni <xref:System.Net.Sockets.Socket> stabilite includono le chiamate al metodo <xref:System.Net.Sockets.Socket> esplicite da un'applicazione per una connessione al socket di flusso stabilita, nonché chiamate interne effettuate da altre classi \(ad esempio <xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>, <xref:System.Net.WebClient> e <xref:System.Net.Sockets.TcpClient>\) alla classe <xref:System.Net.Sockets.Socket>  
  
 I conteggi per **Datagrammi ricevuti** e **Datagrammi inviati** includono pacchetti di datagrammi inviati o ricevuti mediante chiamate al metodo <xref:System.Net.Sockets.Socket> esplicite da un'applicazione, nonché chiamate interne effettuate da altre classi \(ad esempio, <xref:System.Net.Sockets.UdpClient>\) a <xref:System.Net.Sockets.Socket>.  .  I conteggi **Datagrammi ricevuti** e **Datagrammi inviati** possono essere usati anche per fornire una misura molto elementare di quanti byte sono stati inviati o ricevuti mediante datagrammi, presupponendo una dimensione media per un datagramma.  
  
 I contatori delle prestazioni della rete per i dati includono:  
  
-   **Byte ricevuti**  
  
-   **Byte inviati**  
  
 I contatori precedenti indicano i conteggi di byte dall'avvio del processo.  
  
 Esistono due contatori di durata che misurano il tempo impiegato dagli oggetti <xref:System.Net.HttpWebRequest> per passare in tutto il proprio ciclo di vita del ciclo o solo parte di esso:  
  
-   **Durata media di HttpWebRequest**  
  
-   **Tempo medio coda di HttpWebRequest**  
  
 Per il contatore **Durata media di HttpWebRequest**, la durata per la maggior parte degli oggetti <xref:System.Net.HttpWebRequest> inizia sempre dall'ora di creazione dell'oggetto fino all'ora di chiusura del flusso di risposta da parte dell'applicazione.  Esistono due casi non comuni:  
  
-   Se l'applicazione non chiama mai i metodi <xref:System.Net.HttpWebRequest.GetResponse%2A> o <xref:System.Net.HttpWebRequest.BeginGetResponse%2A>, la durata dell'oggetto <xref:System.Net.HttpWebRequest> viene ignorata.  
  
-   Se l'oggetto <xref:System.Net.HttpWebRequest> genera <xref:System.Net.WebException> quando si chiama il metodo <xref:System.Net.HttpWebRequest.GetResponse%2A> o <xref:System.Net.HttpWebRequest.EndGetResponse%2A>, la durata termina quando viene generata l'eccezione.  Tecnicamente, anche il flusso di risposta sottostante viene chiuso a questo punto \(il flusso di risposta restituito all'utente è in effetti un flusso di memoria che contiene una copia del flusso di risposta\).  
  
 Sono disponibili quattro contatori che rilevano determinati problemi degli oggetti <xref:System.Net.HttpWebRequest> per intervallo.  Questi contatori delle prestazioni consentono agli sviluppatori di applicazioni, agli amministratori e al personale del supporto di comprendere meglio le attività degli oggetti <xref:System.Net.HttpWebRequest>.  I contatori includono quando segue:  
  
-   **HttpWebRequest creati\/sec.**  
  
-   **HttpWebRequest in coda\/sec.**  
  
-   **HttpWebRequest interrotti\/sec.**  
  
-   **HttpWebRequest non riusciti\/sec.**  
  
 Per il contatore **HttpWebRequest interrotti\/sec.**, vengono conteggiate anche le chiamate interne a <xref:System.Net.HttpWebRequest.Abort%2A>.  Queste chiamate interne sono generalmente causate dai timeout che un'applicazione desidera misurare.  
  
 Il contatore **HttpWebRequest non riusciti\/sec.** contiene il numero di oggetti <xref:System.Net.HttpWebRequest> che hanno ricevuto un codice di stato di errore dal server al secondo.  Ciò significa che il codice di stato ricevuto dal server Http alla fine della richiesta non era compreso tra 200 e 299.  L'esito dei codici di stato che vengono gestiti e restituiscono una nuova richiesta \(ad esempio, molti dei codici di stato Unauthorized 401\) dipende dal risultato del tentativo.  Se l'applicazione rileva un errore basato sul tentativo, questo contatore viene incrementato.  
  
 L'accesso e la gestione dei contatori delle prestazioni della rete possono essere eseguite con <xref:System.Diagnostics.PerformanceCounter> e le classi correlate nello spazio dei nomi <xref:System.Diagnostics>.  I contatori delle prestazioni di rete possono essere visualizzati anche nella console di Windows Performance Monitor.  
  
 I contatori delle prestazioni della rete devono essere abilitati nel file di configurazione da usare.  Tutti i contatori delle prestazioni della rete vengono abilitati o disabilitati con una singola impostazione nel file di configurazione.  Non è possibile abilitare o disabilitare singoli contatori delle prestazioni della rete.  Per altre informazioni, vedere  [Elemento \<performanceCounter\> \(Impostazioni di rete\)](../../../docs/framework/configure-apps/file-schema/network/performancecounter-element-network-settings.md).  
  
 Se sono abilitati i contatori di rete, le operazioni di creazione e di aggiornamento verranno eseguite per AppDomain e per i contatori delle prestazioni globali.  Se disabilitato, l'applicazione non fornirà dati del contatore di prestazioni di rete.  
  
 I contatori delle prestazioni sono raggruppati in categorie.  Un'applicazione può elencare tutte le categorie con il codice riportato di seguito:  
  
```  
PerformanceCounterCategory[] Array = PerformanceCounterCategory.GetCategories();  
for (int i = 0; i < Array.Length; i++)  
{  
    Console.Out.WriteLine("{0}. Name={1} Help={2}", i, Array[i].CategoryName, Array[i].CategoryHelp);  
}  
  
```  
  
 I contatori delle prestazioni della rete sono elencati in due categorie:  
  
-   ".NET CLR Networking": i contatori delle prestazioni originali introdotti in .NET Framework versione 2 e supportati in .NET Framework versione 2 e versioni successive.  
  
-   ".NET CLR Networking 4.0.0.0": tutti i contatori socket sopra indicati più i nuovi contatori delle prestazioni supportati in .NET Framework versione 4 e versioni successive.  Questi nuovi contatori forniscono informazioni sulle prestazioni degli oggetti <xref:System.Net.HttpWebRequest>.  
  
 Per altre informazioni sull'accesso e la gestione dei contatori delle prestazioni in un'applicazione, vedere [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md).  
  
<a name="security"></a>   
## Contatori delle prestazioni di sicurezza  
 La categoria di sicurezza CLR .NET della console Prestazioni include contatori che forniscono informazioni sui controlli di sicurezza eseguiti da Common Language Runtime per un'applicazione.  Nella tabella che segue vengono descritti tali contatori delle prestazioni.  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|**N. di controlli in fase di collegamento**|Visualizza il numero totale di controlli di sicurezza per l'accesso di codice in fase di collegamento dall'avvio dell'applicazione.  I controlli di sicurezza per l'accesso di codice in fase di collegamento vengono eseguiti quando un chiamante richiede una particolare autorizzazione in fase di compilazione Just\-In\-Time \(JIT\).  Un controllo in fase di collegamento viene eseguito una sola volta per ogni chiamante.  Questo conteggio non segnala problemi gravi relativi alle prestazioni, ma indica solo l'attività del sistema di sicurezza.|  
|**% di tempo per controlli RT**|Visualizza la percentuale di tempo impiegato per eseguire i controlli di sicurezza per l'accesso di codice di runtime dall'ultimo campionamento.  Questo contatore viene aggiornato alla fine di un controllo di sicurezza di .NET Framework.  Non rappresenta una media, ma l'ultimo valore osservato.|  
|**% di tempo per l'autenticazione firma**|Riservato per usi futuri.|  
|**Profondità percorso stack**|Visualizza la profondità dello stack durante l'ultimo controllo di sicurezza per l'accesso di codice di runtime.  I controlli di sicurezza per l'accesso di codice di runtime vengono eseguiti mediante i percorsi nello stack.  Questo contatore non rappresenta una media, ma visualizza solo l'ultimo valore osservato.|  
|**Totale controlli di runtime**|Visualizza il numero totale di controlli di sicurezza per l'accesso di codice di runtime eseguiti dall'avvio dell'applicazione.  I controlli di sicurezza per l'accesso di codice di runtime vengono eseguiti quando un chiamante richiede una particolare autorizzazione.  Il controllo di runtime viene eseguito su tutte le chiamate del chiamante ed esamina lo stack del thread corrente del chiamante.  Se usato con il contatore **Profondità percorso stack**, questo contatore indica la riduzione delle prestazioni che si verifica per i controlli di sicurezza.|  
  
## Vedere anche  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)   
 [Profilatura runtime](../../../docs/framework/debug-trace-profile/runtime-profiling.md)