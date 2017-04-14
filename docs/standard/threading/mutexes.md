---
title: "Mutexes | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "wait handles"
  - "threading [.NET Framework], Mutex class"
  - "Mutex class, about Mutex class"
  - "threading [.NET Framework], cross-process synchronization"
ms.assetid: 9dd06e25-12c0-4a9e-855a-452dc83803e2
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Mutexes
È possibile utilizzare un oggetto <xref:System.Threading.Mutex> per fornire l'accesso esclusivo a una risorsa.  La classe <xref:System.Threading.Mutex> utilizza più risorse di sistema rispetto a <xref:System.Threading.Monitor>, ma può essere sottoposta a marshalling oltre i limiti del dominio applicazione e può essere utilizzata per gestire più condizioni di attesa e per sincronizzare i thread in processi differenti.  Per un confronto dei meccanismi di sincronizzazione gestiti, vedere [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md).  
  
 Per esempi di codice, vedere la documentazione di riferimento per i costruttori <xref:System.Threading.Mutex.%23ctor%2A>.  
  
## Utilizzo dei mutex  
 Un thread chiama il metodo <xref:System.Threading.WaitHandle.WaitOne%2A> di un mutex per richiedere la proprietà di quest'ultimo.  La chiamata rimane bloccata finché il mutex non è disponibile o finché non è trascorso l'intervallo di timeout facoltativo.  Se un mutex non è di proprietà di alcun thread, il relativo stato risulta segnalato.  
  
 Un thread rilascia un mutex chiamando il relativo metodo <xref:System.Threading.Mutex.ReleaseMutex%2A>.  I mutex presentano affinità di thread, ossia possono essere rilasciati solo dal thread che ne è proprietario.  Se un thread rilascia un mutex di cui non è proprietario, nel thread viene generata un'eccezione <xref:System.ApplicationException>.  
  
 Poiché la classe <xref:System.Threading.Mutex> deriva da <xref:System.Threading.WaitHandle>, è anche possibile chiamare il metodo statico <xref:System.Threading.WaitHandle.WaitAll%2A> o <xref:System.Threading.WaitHandle.WaitAny%2A> di <xref:System.Threading.WaitHandle> per richiedere la proprietà di un <xref:System.Threading.Mutex> in combinazione con altri handle di attesa.  
  
 Se un thread è proprietario di un <xref:System.Threading.Mutex>, può specificare lo stesso <xref:System.Threading.Mutex> in chiamate ripetute di attesa\-richiesta senza bloccarne l'esecuzione. Per non esserne più proprietario deve tuttavia rilasciare il <xref:System.Threading.Mutex> lo stesso numero di volte.  
  
## Mutex abbandonati  
 Se un thread viene terminato senza rilasciare un <xref:System.Threading.Mutex>, si dice che il mutex viene abbandonato.  In genere si tratta di un grave errore di programmazione poiché è possibile che la risorsa protetta dal mutex venga lasciata in uno stato incoerente.  In .NET Framework versione 2.0 viene generata un'eccezione <xref:System.Threading.AbandonedMutexException> nel successivo thread che acquisisce il mutex.  
  
> [!NOTE]
>  In .NET Framework versioni 1.0 e 1.1, un <xref:System.Threading.Mutex> abbandonato viene impostato sullo stato segnalato e la proprietà del mutex viene acquisita dal successivo thread in attesa.  Se nessun thread è in attesa, il <xref:System.Threading.Mutex> rimane nello stato segnalato.  Non viene generata alcuna eccezione.  
  
 Nel caso di un mutex di sistema, un mutex abbandonato può indicare che un'applicazione è stata interrotta in modo anomalo, ad esempio tramite Gestione attività Windows.  
  
## Mutex locali e di sistema  
 Esistono due tipi di mutex: mutex locali e mutex di sistema denominati.  Se si crea un oggetto <xref:System.Threading.Mutex> utilizzando un costruttore che accetta un nome, questo viene associato a un oggetto del sistema operativo con il nome specificato.  I mutex di sistema denominati sono visibili in tutto il sistema operativo e possono essere utilizzati per sincronizzare le attività dei processi.  È possibile creare più oggetti <xref:System.Threading.Mutex> che rappresentano lo stesso mutex di sistema denominato ed è possibile utilizzare il metodo <xref:System.Threading.Mutex.OpenExisting%2A> per aprire un mutex di sistema denominato esistente.  
  
 Un mutex locale esiste solo all'interno del processo.  Può essere utilizzato da qualsiasi thread del processo che presenti un riferimento all'oggetto <xref:System.Threading.Mutex> locale.  Ciascun oggetto <xref:System.Threading.Mutex> è un mutex locale distinto.  
  
### Sicurezza del controllo di accesso per i mutex di sistema  
 .NET Framework versione 2.0 consente di interrogare e impostare la sicurezza del controllo di accesso Windows per gli oggetti di sistema denominati.  Si consiglia di proteggere i mutex di sistema sin dal momento della creazione perché gli oggetti di sistema sono definiti a livello globale e possono quindi essere bloccati da altro codice.  
  
 Per informazioni sulla sicurezza del controllo di accesso per i mutex, vedere le classi <xref:System.Security.AccessControl.MutexSecurity> e <xref:System.Security.AccessControl.MutexAccessRule>, l'enumerazione <xref:System.Security.AccessControl.MutexRights>, i metodi <xref:System.Threading.Mutex.GetAccessControl%2A>, <xref:System.Threading.Mutex.SetAccessControl%2A> e <xref:System.Threading.Mutex.OpenExisting%2A> della classe <xref:System.Threading.Mutex> e il costruttore <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29>.  
  
## Vedere anche  
 <xref:System.Threading.Mutex>   
 <xref:System.Threading.Mutex.%23ctor%2A>   
 <xref:System.Security.AccessControl.MutexSecurity>   
 <xref:System.Security.AccessControl.MutexAccessRule>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Monitor](../Topic/Monitors.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)