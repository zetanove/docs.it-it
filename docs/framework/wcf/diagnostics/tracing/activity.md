---
title: "Attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70471705-f55f-4da1-919f-4b580f172665
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attivit&#224;
Questo argomento descrive le tracce attività del modello di traccia di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].Le attività sono unità di elaborazione che consentono all'utente di restringere l'ambito di un errore e quindi di individuarne le cause con maggiore facilità.Gli errori che si verificano nella stessa attività sono correlati in modo diretto.Si consideri ad esempio il caso di un'operazione che non riesce poiché la decrittografia di un messaggio ha avuto esito negativo.Le tracce relative alla non riuscita dell'operazione e della decrittografia del messaggio vengono visualizzate entrambe nella stessa attività, evidenziando in questo modo una correlazione diretta fra i due eventi di errore.  
  
## Configurazione della traccia attività  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] fornisce attività predefinite per l'elaborazione delle applicazioni \(vedere [Elenco delle attività](../../../../../docs/framework/wcf/diagnostics/tracing/activity-list.md)\).È inoltre possibile definire attività a livello di programmazione allo scopo di raggruppare più tracce utente.Per ulteriori informazioni, vedere [Creazione di tracce di codice utente](../../../../../docs/framework/wcf/diagnostics/tracing/emitting-user-code-traces.md).  
  
 Per emettere tracce attività in fase di esecuzione, utilizzare l'impostazione `ActivityTracing` dell'origine di traccia `System.ServiceModel` o di altre origini di traccia personalizzate o fornite da [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], come illustrato nel codice di configurazione seguente.  
  
```  
<source name="System.ServiceModel" switchValue="Verbose,ActivityTracing">  
```  
  
 Per ulteriori informazioni sull'elemento di configurazione e sugli attributi utilizzati, vedere l'argomento [Configurazione delle funzionalità di traccia](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).  
  
## Visualizzazione delle attività  
 Per visualizzare le attività e le relative funzionalità è possibile utilizzare lo [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).Quando la traccia attività è attiva, questo strumento recupera le tracce e le ordina in base all'attività.È inoltre possibile visualizzare i trasferimenti di traccia.Un trasferimento di traccia indica il tipo di correlazione fra due attività.È ad esempio possibile visualizzare un'attività che ha provocato l'avvio di un'altra attività,come nel caso di una richiesta di messaggio che ha avviato un handshake di sicurezza per ottenere un token di conversazione protetta.  
  
### Correlazione delle attività nel visualizzatore di tracce dei servizi  
 Lo strumento visualizzatore di tracce dei servizi fornisce due visualizzazioni di attività:  
  
-   Visualizzazione **elenco**, in cui l'ID attività viene utilizzato per correlare direttamente le tracce di più processi.Le tracce associate a processi distinti, ad esempio client e servizio, ma aventi lo stesso ID attività vengono raggruppate nella stessa attività.Di conseguenza, se nel servizio si verifica un errore che a sua volta comporta un errore nel client, entrambi gli errori verranno inclusi nella stessa visualizzazione di attività dello strumento.  
  
-   Visualizzazione **Grafico**, in cui le attività vengono raggruppate per processo.In questa visualizzazione, le tracce di un client e di un servizio aventi lo stesso ID attività vengono riportate in attività diverse.Per correlare le attività aventi lo stesso ID ma contenute in processi distinti, lo strumento mostra i flussi dei messaggi fra le attività correlate.  
  
 Per ulteriori informazioni e per una visualizzazione grafica del visualizzatore di tracce dei servizi, vedere [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) e [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
## Definizione dell'ambito di un'attività  
 Le attività vengono definite in fase di progettazione per indicare un'unità logica di esecuzione.Le tracce emesse con lo stesso identificatore di attività sono direttamente correlate, in quanto parte della stessa attività.Poiché le attività possono oltrepassare i limiti di endpoint \(ad esempio una richiesta\), per ogni attività vengono definiti due ambiti.  
  
-   Ambito `Global`, per applicazione.In questo ambito, l'attività viene identificata in base al proprio identificatore di attività globalmente univoco \(gAId, global Activity Identifier\) a 128 bit.Il gAid è l'ID che viene propagato fra gli endpoint.  
  
-   Ambito `Local`, per endpoint.In questo ambito, l'attività viene identificata in base al proprio gAId, al nome dell'origine di traccia che emette le tracce attività e all'ID del processo.Questa terna costituisce l'ID attività locale \(lAId, local Activity Identifier\).Il lAId viene utilizzato per definire i limiti \(locali\) di un'attività.  
  
## Schema di traccia  
 Le tracce possono essere emesse utilizzando qualsiasi schema e tra piattaforme Microsoft diverse."e2e" \(ovvero "End to End"\) è un schema utilizzato comunemente.Questo schema include un gAId a 128 bit, il nome dell'origine di traccia e l'ID del processo.In codice gestito, <xref:System.Diagnostics.XmlWriterTraceListener> emette tracce nello schema E2E.  
  
 Gli sviluppatori possono impostare l'AID emesso con una traccia impostando la proprietà <xref:System.Diagnostics.CorrelationManager.ActivityId%2A> con un GUID nell'archiviazione locale di thread \(TLS, Thread Local Storage\).L'esempio seguente illustra come eseguire questa aggiunta.  
  
```  
// set the current Activity ID to a new GUID.  
CorrelationManager.ActivityId = Guid.NewGuid();  
```  
  
 L'impostazione di gAId in TLS sarà evidente quando le tracce vengono emesse utilizzando un'origine di traccia, come illustrato nell'esempio seguente.  
  
```  
TraceSource traceSource = new TraceSource("myTraceSource");  
traceSource.TraceEvent(TraceEventType.Warning, eventId, "Information");  
```  
  
 La traccia emessa conterrà il gAId presente in TLS, il nome dell'origine di traccia passato come parametro al costruttore dell'origine di traccia e l'ID del processo corrente.  
  
## Durata dell'attività  
 In termini rigorosi, l'evidenza di un'attività inizia la prima la prima volta che l'ID attività viene utilizzato in una traccia emessa e termina l'ultima volta che tale ID viene utilizzato in una traccia emessa.Un set predefinito di tipi di traccia viene fornito dallo spazio dei nomi <xref:System.Diagnostics>, che utilizza due tipi di traccia, Start e Stop, per contrassegnare in modo esplicito i limiti di durata dell'attività.  
  
-   Start: indica l'inizio di un'attività.Una traccia di inizio fornisce un record di inizio di una nuova attività cardine di elaborazione.Tale traccia contiene un nuovo ID attività per una determinata origine di analisi in un processo specificato. Se tuttavia l'ID attività viene propagato fra più endpoint, viene visualizzata una traccia "Start" per ogni endpoint.Esempi di avvio di una nuova attività includono la creazione di un nuovo thread di elaborazione o l'immissione di un nuovo metodo pubblico.  
  
-   Stop: indica la fine di un'attività.Una traccia di interruzione fornisce un record di interruzione di un'attività cardine di elaborazione esistente.Tale traccia contiene un ID attività esistente per una determinata origine di analisi in un processo specificato. Se tuttavia l'ID attività viene propagato fra più endpoint, viene visualizzata una traccia "Stop" per ogni endpoint.Esempi di interruzione di un'attività includono l'interruzione di un thread di elaborazione o l'uscita da un metodo il cui inizio era stato denotato con una traccia "Start".  
  
-   Suspend: indica una sospensione nell'elaborazione di un'attività.Una traccia di sospensione contiene un ID attività esistente, la cui elaborazione si prevede verrà ripresa in seguito.Non vengono emesse tracce con questo ID tra l'evento di sospensione e quello di ripresa dall'origine della traccia corrente.Ne è un esempio la sospensione di un'attività in caso di chiamata a una funzione della libreria esterna o di attesa in una risorsa quale una porta di completamento di I\/O.  
  
-   Resume: indica la ripresa dell'elaborazione di un'attività.Una traccia di ripresa contiene un ID attività esistente la cui ultima traccia emessa dall'origine della traccia corrente era "Suspend".Negli esempi è inclusa la restituzione da una chiamata a una funzione della libreria esterna o la segnalazione per riprendere l'elaborazione da parte di una risorsa, ad esempio una porta di completamento di I\/O.  
  
-   Transfer: dato che alcune attività sono causate da altre o sono correlate ad altre, possono essere correlate ad altre attività tramite tracce di trasferimento.Un trasferimento registra la relazione diretta di un'attività con un'altra  
  
 Le tracce Start e Stop non sono critiche per la correlazione.Possono tuttavia contribuire ad aumentare le prestazioni, il profiling e la convalida dell'ambito dell'attività.  
  
 Utilizzando questi tipi, gli strumenti riescono a ottimizzare l'accesso ai registri di traccia per individuare gli eventi immediatamente correlati della stessa attività o eventi in attività correlate se lo strumento segue tracce di trasferimento.Gli strumenti interromperanno l'analisi dei registri di una determinata attività quando vedono una traccia Start\/Stop.  
  
 Questi tipi di traccia possono essere utilizzati anche per il profiling.Le risorse utilizzate tra i marcatori di inizio e di arresto rappresentano il tempo inclusivo dell'attività, comprese le attività logiche contenute.La sottrazione degli intervalli di tempo tra le tracce Suspend e Resume fornisce il tempo di attività effettivo.  
  
 La traccia Stop è inoltre particolarmente utile per convalidare l'ambito delle attività implementate.Se alcune tracce di elaborazione vengono visualizzate dopo la traccia Stop, anziché all'interno di una determinata attività, è probabile che vi sia un difetto del codice.  
  
## Linee guida per l'utilizzo della traccia attività  
 Di seguito viene illustrato come utilizzare le tracce di ActivityTracing \(Start, Stop, Suspend, Resume e Transfer\).  
  
-   La traccia è un grafico ciclico diretto, non una struttura.È possibile restituire il controllo a un'attività che ha generato un'attività.  
  
-   Un'attività denota un limite di elaborazione che può essere significativo per l'amministratore del sistema o per le configurazioni supportate.  
  
-   Ogni metodo [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)], sia nel client che nel server è vincolato dall'inizio di una nuova attività, quindi \(al termine del lavoro\) dalla terminazione della nuova attività e dal ritorno all'attività ambiente.  
  
-   Le attività a esecuzione prolungata \(in corso\), ad esempio l'ascolto di connessioni o l'attesa di messaggi, sono rappresentate da marcatori di avvio\/arresto corrispondenti.  
  
-   Le attività avviate dal ricevimento o dall'elaborazione di un messaggio sono rappresentate da limiti di traccia.  
  
-   Le attività rappresentano attività, non necessariamente degli oggetti.Un'attività deve essere interpretata come "ciò che si stava verificando quando ...\(si è verificata l'emissione di una traccia significativa\)".  
  
## Vedere anche  
 [Configurazione delle funzionalità di traccia](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [Scenari di analisi end\-to\-end](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)   
 [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)   
 [Creazione di tracce di codice utente](../../../../../docs/framework/wcf/diagnostics/tracing/emitting-user-code-traces.md)