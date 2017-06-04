---
title: "Diagnostica di applicazioni transazionali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a993492-1088-4d10-871b-0c09916af05f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Diagnostica di applicazioni transazionali
In questo argomento viene illustrato come utilizzare la funzionalità di gestione e di diagnostica di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per risolvere i problemi di un'applicazione transazionale.  
  
## Contatori di prestazioni  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un set standard di contatori delle prestazioni per misurare le prestazioni delle applicazioni transazionali.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Contatori di prestazioni](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md).  
  
 I contatori delle prestazioni vengono definiti a tre diversi livelli: servizio, endpoint e operazione come descritto nelle tabelle seguenti.  
  
### Contatori delle prestazioni del servizio  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|Transazioni propagate|Numero di transazioni propagate alle operazioni in questo servizio.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato al servizio.|  
|Transazioni propagate al secondo|Numero di transazioni propagate alle operazioni in questo servizio ogni secondo.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato al servizio.|  
|Operazioni transazionali con commit eseguito|Numero di operazioni transazionali eseguite la cui transazione è stata completata e di cui è stato eseguito il commit del risultato nel servizio.  Per le attività completate nell'ambito di tali operazioni viene eseguito il commit completo.  Le risorse vengono aggiornate in base alle attività completate nell'operazione.|  
|Operazioni transazionali con commit eseguito al secondo|Numero di operazioni transazionali eseguite la cui transazione è stata completata e di cui è stato eseguito il commit del risultato nel servizio ogni secondo.  Per le attività completate nell'ambito di tali operazioni viene eseguito il commit completo.  Le risorse vengono aggiornate in base alle attività completate nell'operazione.|  
|Operazioni transazionali interrotte|Numero di operazioni transazionali eseguite la cui transazione è stata completata con il risultato annullato nel servizio.  Per le attività completate nell'ambito di tali operazioni viene eseguito il rollback.  Viene ripristinato lo stato precedente delle risorse.|  
|Operazioni transazionali interrotte ogni secondo|Numero di operazioni transazionali eseguite la cui transazione è stata completata con il risultato annullato nel servizio ogni secondo.  Per le attività completate nell'ambito di tali operazioni viene eseguito il rollback.  Viene ripristinato lo stato precedente delle risorse.|  
|Operazioni transazionali incerte|Numero di operazioni transazionali eseguite la cui transazione è stata completata con un risultato in dubbio nel servizio.  Le attività completate con un risultato in dubbio sono in stato indeterminato.  Le risorse vengono mantenute con risultato in sospeso.|  
|Operazioni transazionali in dubbio al secondo|Numero di operazioni transazionali eseguite la cui transazione è stata completata con un risultato in dubbio nel servizio ogni secondo.  Le attività completate con un risultato in dubbio sono in stato indeterminato.  Le risorse vengono mantenute con risultato in sospeso.|  
  
### Contatori delle prestazioni dell'endpoint  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|Transazioni propagate|Numero di transazioni propagate alle operazioni in questo endpoint.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato all'endpoint.|  
|Transazioni propagate al secondo|Numero di transazioni propagate alle operazioni in questo endpoint ogni secondo.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato all'endpoint.|  
  
### Contatori delle prestazioni per l'operazione  
  
|Contatore di prestazioni|Descrizione|  
|------------------------------|-----------------|  
|Transazioni propagate|Numero di transazioni propagate alle operazioni in questo endpoint.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato all'endpoint.|  
|Transazioni propagate al secondo|Numero di transazioni propagate alle operazioni in questo endpoint ogni secondo.  Questo contatore viene incrementato ogni volta che è presente una transazione nel messaggio inviato all'endpoint.|  
  
## Strumentazione gestione Windows  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] espone dati di ispezione di un servizio in fase di esecuzione tramite un provider WMI di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'accesso ai dati WMI, vedere [Utilizzo di Strumentazione gestione Windows \(WMI\) per la diagnostica](../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
 Un numero di proprietà WMI in sola lettura indica le impostazioni della transazione applicate per un servizio.  Nella tabelle seguenti vengono elencate tutte queste impostazioni.  
  
 In un servizio, `ServiceBehaviorAttribute` dispone delle proprietà seguenti.  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|ReleaseServiceInstanceOnTransactionComplete|Booleano|Specifica se l'oggetto servizio viene riciclato al completamento della transazione corrente.|  
|TransactionAutoCompleteOnSessionClose|Booleano|Specifica se alla chiusura della sessione corrente vengono completate le transazioni in sospeso.|  
|TransactionIsolationLevel|Stringa che contiene un valore valido dell'enumerazione <xref:System.Transactions.IsolationLevel>.|Specifica il livello di isolamento della transazione supportato dal servizio.|  
|TransactionTimeout|<xref:System.DateTime>|Specifica il periodo di tempo entro il quale deve essere completata una transazione.|  
  
 `ServiceTimeoutsBehavior` dispone della proprietà seguente.  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TransactionTimeout|<xref:System.DateTime>|Specifica il periodo di tempo entro il quale deve essere completata una transazione.|  
  
 In un'associazione, `TransactionFlowBindingElement` dispone delle proprietà seguenti.  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TransactionProtocol|Stringa che contiene un valore valido del tipo <xref:System.ServiceModel.TransactionProtocol>.|Specifica il protocollo di transazione da utilizzare per la propagazione di una transazione.|  
|TransactionFlow|Booleano|Specifica se è attivato il flusso delle transazioni in ingresso.|  
  
 In un'operazione, `OperationBehaviorAttribute` dispone delle proprietà seguenti:  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TransactionAutoComplete|Booleano|Specifica se eseguire automaticamente il commit della transazione corrente se non si verifica alcuna eccezione non gestita.|  
|TransactionScopeRequired|Booleano|Specifica se l'operazione richiede una transazione.|  
  
 In un'operazione, `TransactionFlowAttribute` dispone delle proprietà seguenti.  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|TransactionFlowOption|Stringa che contiene un valore valido dell'enumerazione <xref:System.ServiceModel.TransactionFlowOption>.|Specifica in che misura è richiesto il flusso delle transazioni.|  
  
## Traccia  
 Le tracce consentono di controllare e analizzare errori nelle applicazioni transazionali.  È possibile attivare la traccia nei modi seguenti:  
  
-   Traccia [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] standard  
  
     Questo tipo di traccia è equivalente alla traccia di qualsiasi applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Configurazione delle funzionalità di traccia](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).  
  
-   Traccia WS\-AtomicTransaction  
  
     È possibile attivare la traccia WS\-AtomicTransaction tramite l'[Utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md).  Tale traccia consente di comprendere lo stato delle transazioni e di conoscere i partecipanti all'interno di un sistema.  Per attivare anche la traccia del modello di servizi interna, è possibile impostare la chiave del Registro di sistema `HKLM\SOFTWARE\Microsoft\WSAT\3.0\ServiceModelDiagnosticTracing` su un valore valido dell'enumerazione <xref:System.Diagnostics.SourceLevels>.  È possibile attivare la registrazione messaggi nella stessa modalità utilizzata per altre applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Traccia `System.Transactions`  
  
     Quando si utilizza il protocollo OleTransactions, i messaggi di protocollo non possono essere tracciati.  Il supporto di traccia fornito dall'infrastruttura <xref:System.Transactions>, che utilizza OleTransactions, consente agli utenti di visualizzare gli eventi che si sono verificati nelle transazioni.  Per attivare la traccia per un'applicazione <xref:System.Transactions>, includere il codice seguente nel file di configurazione `App.config`.  
  
    ```  
    <configuration>  
      <system.diagnostics>  
         <sources>  
            <source name="System.Transactions" switchValue="Verbose, ActivityTracing">  
               <listeners>  
                  <add name="Text"  
                     type="System.Diagnostics.XmlWriterTraceListener"  
                     initializeData="SysTx.log"  
                     traceOutputOptions="Callstack" />  
               </listeners>  
            </source>  
         </sources>  
         <trace autoflush="true" indentsize="4">  
         </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
     In tal modo si attiva inoltre la traccia [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], poiché anche [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'infrastruttura <xref:System.Transactions>.  
  
## Vedere anche  
 [Amministrazione e diagnostica](../../../../docs/framework/wcf/diagnostics/index.md)   
 [Configurazione delle funzionalità di traccia](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [Utilità di configurazione WS\-AtomicTransaction \(wsatConfig.exe\)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)