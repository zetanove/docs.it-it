---
title: "Procedure consigliate per la persistenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6974c5a4-1af8-4732-ab53-7d694608a3a0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedure consigliate per la persistenza
In questo documento vengono descritte le procedure consigliate per la progettazione e la configurazione del flusso di lavoro al fine di mantenerne la persistenza.  
  
## Progettazione e implementazione di flussi di lavoro durevoli  
 In generale, in un flusso di lavoro le attività vengono eseguite in periodi brevi separati da intervalli durante i quali il flusso di lavoro è inattivo perché in attesa di un evento,ad esempio un messaggio o la scadenza di un timer.Per essere in grado di scaricare l'istanza del flusso di lavoro quando diventa inattiva, l'host del servizio deve renderla persistente.Questa operazione è possibile solo se l'istanza del flusso di lavoro non si trova in un'area di non persistenza, ad esempio in attesa di un callback asincrono o del completamento di una transazione.Per consentire a un'istanza del flusso di lavoro inattiva di essere scaricata, l'autore del flusso di lavoro deve utilizzare ambiti di transazione e attività asincrone solo per azioni di breve durata.In particolare, le attività di ritardo all'interno di tali aree di non persistenza devono essere le più brevi possibili.  
  
 Un flusso di lavoro può essere reso persistente solo se tutti i tipi di dati utilizzati sono serializzabili.I tipi personalizzati utilizzati in flussi di lavoro persistenti, inoltre, devono essere serializzabili tramite <xref:System.Runtime.Serialization.NetDataContractSerializer> per essere resi persistenti da <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>.  
  
 Se un'istanza del flusso di lavoro non è stata resa persistente, non è possibile recuperarla in caso in cui si verifichi un errore nell'host o nel computer.In generale, si consiglia di rendere subito persistente un'istanza del flusso di lavoro nel relativo ciclo di vita.  
  
 Se il flusso di lavoro è occupato per un periodo di tempo prolungato, si consiglia di rendere persistente la relativa istanza regolarmente durante tutto il periodo.A tale scopo, aggiungere le attività <xref:System.Activities.Statements.Persist> durante tutta la sequenza di operazioni che tengono occupata l'istanza del flusso di lavoro.In questo modo il riciclo del dominio applicazione o eventuali errori nell'host o nel computer non provocano l'esecuzione del rollback del sistema all'inizio del periodo in cui il flusso di lavoro è occupato.Tenere presente che l'aggiunta di attività <xref:System.Activities.Statements.Persist> al flusso di lavoro potrebbe provocare una riduzione delle prestazioni.  
  
 Windows Server AppFabric consente di semplificare notevolmente la configurazione e l'utilizzo della persistenza.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Concetti di salvataggio permanente](http://go.microsoft.com/fwlink/?LinkID=201200&clcid=0x409)  
  
## Configurazione dei parametri di scalabilità  
 I requisiti relativi alla scalabilità e alle prestazione determinano le impostazioni dei parametri seguenti:  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>  
  
-   <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A>  
  
 In base allo scenario corrente, tali parametri dovrebbero essere impostati nel modo indicato di seguito.  
  
### Scenario: presenza di un numero ridotto di istanze del flusso di lavoro che richiedono un tempo di risposta ottimale  
 In questo scenario tutte le istanze del flusso di lavoro devono rimanere caricate quando diventano inattive.Impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> su un valore elevato.Questa impostazione consente di impedire che un'istanza del flusso di lavoro si sposti tra computer.Utilizzare questa impostazione solo se si verifica una o più delle condizioni seguenti:  
  
-   Un'istanza del flusso del lavoro riceve un unico messaggio in tutta la durata.  
  
-   Tutte le istanze del flusso di lavoro vengono eseguite in un unico computer.  
  
-   Tutti i messaggi ricevuti da un'istanza del flusso di lavoro vengono recapitati nello stesso computer.  
  
 Utilizzare attività <xref:System.Activities.Statements.Persist> o impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> su 0 per abilitare il recupero dell'istanza del flusso di lavoro dopo eventuali errori dell'host del servizio o del computer.  
  
### Scenario: inattività delle istanze del flusso di lavoro per periodi di tempo prolungati  
 In questo scenario impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> su 0 per rilasciare le risorse il prima possibile.  
  
### Scenario: le istanze del flusso di lavoro ricevono più messaggi in un breve periodo di tempo  
 In questo scenario impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> su 60 secondi se i messaggi vengono ricevuti dallo stesso computer.In questo modo si impedisce che un'istanza del flusso di lavoro venga scaricata e caricata rapidamentee che l'istanza rimanga in memoria per un periodo di tempo eccessivo.  
  
 Impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> su 0 e <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A> su BasicRetry o AggressiveRetry se tali messaggi possono essere ricevuti da computer diversi.In questo modo l'istanza del flusso di lavoro può essere caricata da un altro computer.  
  
### Scenario: il flusso di lavoro utilizza le attività di ritardo con durate brevi  
 In questo scenario <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> esegue regolarmente il polling sul database di persistenza per istanze che devono essere caricate a causa di un'attività <xref:System.Activities.Statements.Delay> scaduta.Se <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> trova un timer che scadrà nell'intervallo di polling successivo, l'archivio di istanze del flusso di lavoro SQL riduce l'intervallo di polling.Il polling successivo verrà eseguito subito dopo la scadenza del timer.In questo modo si ottiene un'elevata precisione per i timer in esecuzione da più tempo rispetto all'intervallo di polling, impostato da <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>.Per abilitare un'elaborazione corretta di ritardi più brevi, l'istanza del flusso di lavoro deve rimanere in memoria almeno per la durata di un intervallo di polling.  
  
 Impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> su 0 per scrivere la scadenza nel database di persistenza.  
  
 Impostare <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> su un valore maggiore o uguale a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> per mantenere l'istanza in memoria almeno per la durata di un intervallo di polling.  
  
 Si consiglia di non ridurre il valore di <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> per non aumentare il carico sul database di persistenza.Ogni host del servizio che utilizza <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> esegue il polling sul database una volta per periodo del rilevamento.Se si imposta <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> su un intervallo di tempo troppo breve, le prestazioni del sistema potrebbero diminuire nel caso in cui il numero di host del servizio sia elevato.  
  
## Configurazione dell'archivio di istanze del flusso di lavoro SQL  
 All'archivio di istanze del flusso di lavoro SQL sono associati i parametri di configurazione seguenti:  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceEncodingOption%2A>  
 Questo parametro indica a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> di comprimere lo stato dell'istanza del flusso di lavoro.La compressione consente di ridurre la quantità di dati archiviata nel database di persistenza e di diminuire il traffico di rete nel caso in cui il database di persistenza si trovi in un server database dedicato.Se utilizzata, la compressione richiede risorse computazionali per comprimere ed estrarre lo stato dell'istanza.Nella maggior parte dei casi la compressione consente di aumentare le prestazioni.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceCompletionAction%2A>  
 Questo parametro indica a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> di mantenere o eliminare istanze completate.Se le istanze completate non vengono eliminate, i requisiti di archiviazione del database di persistenza e la dimensione delle tabelle aumentano, con un conseguente incremento dei tempi di ricerca.È consigliabile pertanto indicare a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> di eliminare le istanze completate, a meno che queste ultime non siano necessarie per l'esecuzione di attività di debug o di controllo.Le istanze eliminate devono essere mantenute solo se l'utente definisce un processo per l'eventuale rimozione.Si noti che non è possibile riutilizzare chiavi di correlazione fino a quando l'istanza del flusso di lavoro completata è presente nell'archivio di istanze.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>  
 Questo parametro definisce l'intervallo massimo in base al quale <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> esegue il polling sul database di persistenza per istanze che devono essere caricate quando un'attività <xref:System.Activities.Statements.Delay> scade.Se <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> trova un timer che scadrà nell'intervallo di polling successivo, l'intervallo di polling verrà ridotto in modo che il polling successivo venga eseguito subito dopo la scadenza del timer.In questo modo si ottiene un'elevata precisione per i timer in esecuzione da più tempo rispetto a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>.  
  
 Si consiglia di non ridurre il valore di <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> per non aumentare il carico sul database di persistenza.Ogni host del servizio che utilizza <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> esegue il polling sul database una volta per periodo del rilevamento.Se si imposta <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> su un intervallo di tempo troppo breve, le prestazioni del sistema potrebbero diminuire nel caso in cui il numero di host del servizio sia elevato.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>  
 Questo parametro definisce l'intervallo in base al l'host rinnova il blocco nel database di persistenza.La riduzione dell'intervallo consentirà un recupero più rapido delle istanze del flusso di lavoro in caso di errore dell'host o del computer.Un periodo di rinnovo del blocco più breve, tuttavia, provoca l'aumento del carico sul database di persistenza.Ogni host del servizio che utilizza <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> aggiornerà i blocchi nel database una volta per periodo di rinnovo.Se in un computer sono in esecuzione numerosi host del servizio, verificare che il carico causato dal rinnovo del blocco non diminuisca le prestazioni del sistema.Se questo accade, provare ad aumentare il valore di <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>  
 Se abilitato, <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> tenta nuovamente di caricare un'istanza bloccata per i successivi 30 secondi.Impostare <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> su BasicRetry o AggressiveRetry se il flusso di lavoro riceve più messaggi in un breve periodo di tempo e tali messaggi vengono recapitati in computer diversi.  
  
 Poiché il meccanismo di ricaricamento non introduce alcun sovraccarico nelle prestazioni finché l'operazione non viene tentata, è necessario abilitare sempre <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>.