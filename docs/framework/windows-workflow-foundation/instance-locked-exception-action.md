---
title: "Instance Locked Exception Action | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 164a5419-315c-4987-ad72-54cbdb88d402
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Instance Locked Exception Action
La proprietà <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> dell'Archivio di istanze del flusso di lavoro SQL consente di specificare l'azione che il provider di persistenza SQL deve eseguire quando riceve un'eccezione <xref:System.Runtime.DurableInstancing.InstanceLockedException>.Il provider di persistenza riceve questa eccezione quando tenta di bloccare un'istanza del servizio flusso di lavoro che è attualmente bloccata da un altro host del servizio.I valori di questa proprietà sono <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>, <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> e <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.Il valore predefinito è <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.Nell'elenco seguente vengono descritte le tre opzioni:  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.L'host del servizio non tenta di bloccare l'istanza del servizio flusso di lavoro e passa <xref:System.Runtime.DurableInstancing.InstanceLockedException> al chiamante. Se il flusso di lavoro rimane in memoria per un periodo superiore a 60 secondi, utilizzare <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> come tentativo.Il valore predefinito è <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.L'host del servizio tenta di nuovo di bloccare l'istanza con un intervallo lineare tra tentativi e passa <xref:System.Runtime.DurableInstancing.InstanceLockedException> al chiamante alla fine della sequenza.Se il flusso di lavoro rimane in memoria approssimativamente tra i 5 e 60 secondi e i messaggi arrivano in batch, per cui è più probabile che i messaggi siano inviati alla stessa istanza nello stesso host per elaborare tutti i messaggi prima di scaricare il flusso di lavoro, utilizzare <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> per ottenere la migliore latenza senza sprecare risorse.  
  
-   <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>.L'host del servizio tenta di nuovo di bloccare l'istanza di servizio del flusso di lavoro con un intervallo di interruzione esponenziale tra tentativi e passa l'eccezione al chiamante alla fine della sequenza.Se il flusso di lavoro rimane in memoria per un tempo molto breve \(meno di 5 secondi\) o una Web farm è grande e la probabilità che un altro messaggio sia recapitato allo stesso host non è molto elevata, utilizzare <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> per ottenere la migliore latenza.  
  
 La funzionalità Instance Locked Exception Action supporta gli scenari seguenti.In tutti gli scenari, se la proprietà instanceLockedExceptionAction di SqlWorkflowInstanceStore è impostata su <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction> o <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>, l'host tenta in modo trasparente di acquisire periodicamente il blocco sulle istanze.  
  
1.  **Abilitazione dell'arresto normale e del riciclo sovrapposto di domini dell'applicazione.** Si supponga che un oggetto **AppDomain** con un host del servizio in cui sono in esecuzione le istanze del servizio flusso di lavoro sia in fase di riciclo e che venga visualizzato un nuovo oggetto **AppDomain** per gestire le nuove richieste mentre l'oggetto **AppDomain** precedente non è più disponibile.L'arresto attende finché le istanze del servizio flusso di lavoro non sono inattive, quindi le istanze vengono rese persistenti e scaricate.Qualsiasi tentativo da parte degli host nel nuovo **AppDomain** di bloccare un'istanza genererà un'eccezione <xref:System.Runtime.DurableInstancing.InstanceLockedException>.  
  
2.  **Ridimensionamento orizzontale dei flussi di lavoro durevoli in una farm omogenea di server.** Si supponga che un nodo di una server farm in cui è in esecuzione un'istanza del flusso di lavoro venga arrestato in modo anomalo e l'host del flusso di lavoro non possa rimuovere i blocchi sull'istanza che sta eseguendo.Quando un host del servizio che è in esecuzione in un altro nodo della farm riceve un messaggio per l'istanza di quel flusso di lavoro, tenta di acquisire i blocchi su queste istanze e riceverà l'eccezione <xref:System.Runtime.DurableInstancing.InstanceLockedException>.I blocchi scadranno dopo un po' di tempo perché l'host che doveva rinnovare il blocco non esiste più.  
  
     **Ridimensionamento orizzontale dei flussi di lavoro durevoli in una farm omogenea di server.**  Si supponga di voler ridimensionare orizzontalmente un flusso di lavoro durevole utilizzando più host in un bilanciamento del carico di rete \(NLB\), che l'host del flusso di lavoro in esecuzione in un nodo della farm carichi un'istanza del flusso di lavoro e stia elaborando un messaggio e che il successivo messaggio all'istanza venga indirizzato all'host in esecuzione in un altro nodo perché il bilanciamento del carico di rete non dispone dell'algoritmo di routing per recapitare i messaggi all'host che sta già eseguendo l'istanza.Dopo la ricezione del messaggio, il secondo host tenta di caricare l'istanza del flusso di lavoro e riceve l'eccezione <xref:System.Runtime.DurableInstancing.InstanceLockedException> perché il primo host dispone di un blocco sull'istanza.Il primo host sblocca l'istanza al termine dell'elaborazione del primo messaggio e il secondo host acquisisce il blocco quando ritenta la volta successiva, carica l'istanza ed elabora il secondo messaggio.