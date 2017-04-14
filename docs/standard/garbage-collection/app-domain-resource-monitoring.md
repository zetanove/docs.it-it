---
title: "Application Domain Resource Monitoring | Microsoft Docs"
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
  - "monitoring managed memory use by application domain"
  - "application domains, memory use"
  - "memory use, monitoring"
  - "application domains, resource monitoring"
ms.assetid: 318bedf8-7f35-4f00-b34a-2b7b8e3fa315
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Application Domain Resource Monitoring
Il monitoraggio delle risorse del dominio applicazione \(ARM\) consente agli host di monitorare la CPU e l'utilizzo della memoria in base al dominio applicazione.  È utile per gli host quale ad esempio ASP.NET che utilizzano molti domini applicazione in un processo di lunga durata.  L'host può scaricare il dominio di un'applicazione che influisce negativamente sulle prestazioni dell'intero processo, soltanto però se è in grado di identificare l'applicazione problematica.  Il monitoraggio ARM fornisce informazioni utili ai fini di una decisione in tal senso.  
  
 È possibile ad esempio che un servizio di hosting abbia numerose applicazioni in esecuzione in un server ASP.NET.  Se un'applicazione nel processo inizia a utilizzare troppa memoria o troppo tempo processore, il servizio di hosting può utilizzare il monitoraggio ARM per identificare il dominio applicazione che causa il problema.  
  
 Il monitoraggio ARM è sufficientemente leggero da utilizzare nelle applicazioni attive.  È possibile accedere alle informazioni tramite Traccia eventi per Windows \(ETW\) o direttamente tramite le API gestite o native.  
  
## Abilitazione del monitoraggio delle risorse  
 Il monitoraggio ARM può essere abilitato in quattro modi: fornendo un file di configurazione all'avvio di Common Language Runtime \(CLR\), utilizzando un'API di hosting non gestita, utilizzando codice gestito oppure attendendo gli eventi ETW ARM.  
  
 Non appena il monitoraggio ARM viene abilitato, inizia a raccogliere dati in tutti i domini applicazione del processo.  Se un dominio applicazione è stato creato prima che il monitoraggio ARM fosse abilitato, i dati cumulativi iniziano dal momento in cui il monitoraggio viene abilitato, non dal momento della creazione del dominio applicazione. Una volta abilitato, il monitoraggio ARM non può essere disabilitato.  
  
-   È possibile abilitare il monitoraggio ARM all'avvio di CLR aggiungendo l'elemento [\<appDomainResourceMonitoring\>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md) al file di configurazione e impostando l'attributo `enabled` su `true`.  Il valore `false` \(impostazione predefinita\) significa solo che il monitoraggio ARM non viene abilitato all'avvio; sarà possibile attivarlo in un secondo momento utilizzando uno degli altri meccanismi di attivazione.  
  
-   L'host può abilitare il monitoraggio ARM richiedendo l'interfaccia di hosting [ICLRAppDomainResourceMonitor](../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md).  Una volta ottenuta correttamente questa interfaccia, il monitoraggio ARM è abilitato.  
  
-   Il codice gestito può abilitare il monitoraggio ARM impostando la proprietà statica <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName> \(`Shared` in Visual Basic\) su `true`.  Non appena la proprietà viene impostata, il monitoraggio ARM è abilitato.  
  
-   Il monitoraggio ARM può essere abilitato successivamente all'avvio attendendo gli eventi ETW.  Il monitoraggio viene abilitato e inizia a generare eventi per tutti i domini applicazione quando si abilita il provider pubblico `Microsoft-Windows-DotNETRuntime` tramite la parola chiave `AppDomainResourceManagementKeyword`.  Per correlare i dati con i domini applicazione e i thread, è necessario abilitare anche il provider `Microsoft-Windows-DotNETRuntimeRundown` con la parola chiave `ThreadingKeyword`.  
  
## Utilizzo di ARM  
 Il monitoraggio ARM fornisce il tempo processore totale utilizzato da un dominio applicazione e tre tipi di informazioni sull'utilizzo della memoria.  
  
-   **Tempo processore totale di un dominio applicazione, in secondi**: viene calcolato sommando le durate dei thread segnalate dal sistema operativo per tutti i thread la cui esecuzione nel dominio applicazione nel corso della sua durata ha richiesto del tempo.  I thread bloccati o sospesi non utilizzano tempo processore.  Quando un thread esegue una chiamata in codice nativo, il tempo trascorso dal thread nel codice viene incluso nel conteggio del dominio applicazione in cui è stata effettuata la chiamata.  
  
    -   API gestita: proprietà <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=fullName>.  
  
    -   API di hosting: metodo [ICLRAppDomainResourceMonitor::GetCurrentCpuTime](../Topic/ICLRAppDomainResourceMonitor::GetCurrentCpuTime%20Method.md).  
  
    -   Eventi ETW: eventi `ThreadCreated`, `ThreadAppDomainEnter` e `ThreadTerminated`.  Per informazioni sui provider e le parole chiave, vedere "Eventi di monitoraggio delle risorse di AppDomain" in [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md).  
  
-   **Allocazioni gestite totali eseguite da un dominio applicazione nel corso della sua durata, in byte**: non sempre le allocazioni totali riflettono l'utilizzo della memoria da parte di un dominio applicazione, poiché gli oggetti allocati possono essere di breve durata.  Tuttavia, se un'applicazione alloca e libera grandi quantità di oggetti, il peso delle allocazioni può essere significativo.  
  
    -   API gestita: proprietà <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=fullName>.  
  
    -   API di hosting: metodo [ICLRAppDomainResourceMonitor::GetCurrentAllocated](../Topic/ICLRAppDomainResourceMonitor::GetCurrentAllocated%20Method.md).  
  
    -   Eventi ETW: evento `AppDomainMemAllocated`, campo `Allocated`.  
  
-   **Memoria gestita, in byte, oggetto di riferimento da parte di un dominio applicazione ed esclusa dalla procedura completa di Garbage Collection bloccante più recente**: il numero è preciso soltanto dopo una procedura bloccante completa. Al contrario, le raccolte simultanee vengono eseguite in background e non bloccano l'applicazione. L'overload del metodo <xref:System.GC.Collect?displayProperty=fullName>, ad esempio, provoca una procedura completa di Garbage Collection bloccante.  
  
    -   API gestita: proprietà <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=fullName>.  
  
    -   API di hosting: metodo [ICLRAppDomainResourceMonitor::GetCurrentSurvived](../Topic/ICLRAppDomainResourceMonitor::GetCurrentSurvived%20Method.md), parametro `pAppDomainBytesSurvived`.  
  
    -   Eventi ETW: evento `AppDomainMemSurvived`, campo `Survived`.  
  
-   **Memoria gestita totale, in byte, oggetto di riferimento da parte del processo ed esclusa dalla procedura completa di Garbage Collection bloccante più recente**: la memoria esclusa per singoli domini applicazione può essere confrontata con questo numero.  
  
    -   API gestita: proprietà <xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=fullName>.  
  
    -   API di hosting: metodo [ICLRAppDomainResourceMonitor::GetCurrentSurvived](../Topic/ICLRAppDomainResourceMonitor::GetCurrentSurvived%20Method.md), parametro `pTotalBytesSurvived`.  
  
    -   Eventi ETW: evento `AppDomainMemSurvived`, campo `ProcessSurvived`.  
  
### Rilevamento di una procedura completa di Garbage Collection bloccante  
 Per stabilire il momento in cui i conteggi della memoria esclusa sono precisi, è necessario sapere quando si verifica una procedura completa di Garbage Collection bloccante.  Il metodo da impiegare dipende dall'API utilizzata per esaminare le statistiche del monitoraggio ARM.  
  
#### API gestita  
 Se si utilizzano le proprietà della classe <xref:System.AppDomain>, è possibile utilizzare il metodo <xref:System.GC.RegisterForFullGCNotification%2A?displayProperty=fullName> per registrarsi per la notifica delle raccolte complete.  La soglia utilizzata non è importante, in quanto l'attesa riguarda il completamento di una raccolta piuttosto che l'approssimarsi di una raccolta.  È quindi possibile chiamare il metodo <xref:System.GC.WaitForFullGCComplete%2A?displayProperty=fullName>, che impone un blocco fino al termine della raccolta completa.  È possibile creare un thread che chiami il metodo in un ciclo ed esegua le analisi necessarie a ogni restituzione del metodo.  
  
 In alternativa, è possibile chiamare il metodo <xref:System.GC.CollectionCount%2A?displayProperty=fullName> periodicamente per vedere se il conteggio delle raccolte di generazione 2 sia aumentato.  A seconda della frequenza di polling, questa tecnica potrebbe non considerare precisa un'indicazione dell'occorrenza di una raccolta completa.  
  
#### API di hosting  
 Se si utilizza l'API di hosting non gestita, l'host deve passare a CLR un'implementazione dell'interfaccia [IHostGCManager](../../../ocs/framework/unmanaged-api/hosting/ihostgcmanager-interface.md).  CLR chiama il metodo [IHostGCManager::SuspensionEnding](../Topic/IHostGCManager::SuspensionEnding%20Method.md) quando riprende l'esecuzione dei thread sospesi durante una raccolta.  CLR passa la generazione della raccolta completata come parametro del metodo, così l'host può determinare se la raccolta era completa o parziale.  L'implementazione del metodo [IHostGCManager::SuspensionEnding](../Topic/IHostGCManager::SuspensionEnding%20Method.md) può eseguire una query per la memoria esclusa, per assicurare che i conteggi vengono recuperati non appena aggiornati.  
  
## Vedere anche  
 <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName>   
 [Interfaccia ICLRAppDomainResourceMonitor](../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)   
 [\<appDomainResourceMonitoring\>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)   
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)