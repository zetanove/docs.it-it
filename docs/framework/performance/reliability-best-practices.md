---
title: "Reliability Best Practices | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "marking locks"
  - "rebooting databases"
  - "denial of service attacks"
  - "back-out code"
  - "SQL Server [.NET Framework], reliability"
  - "synchronization, reliability"
  - "single-threaded COM components"
  - "slow leaks"
  - "suspending threads"
  - "asynchronous exception handling"
  - "leaked resources [.NET Framework]"
  - "unmanaged memory"
  - "memory, reliability"
  - "threading [.NET Framework], reliability"
  - "process-wide domain shared states"
  - "shared states"
  - "SafeHandle class, reliability"
  - "reliability contracts [.NET Framework]"
  - "cleanup operations"
  - "constrained execution regions"
  - "CERs"
  - "finalizers, reliability"
  - "reliability [.NET Framework]"
  - "blocks, reliability"
  - "finally clauses"
  - "cross-application domain shared states"
  - "catch blocks"
  - "identifying locks"
  - "writing reliable code"
  - "impersonation"
  - "GC.KeepAlive method"
  - "managed threading"
  - "locks, reliability"
  - "STA-dependent features"
  - "fibers"
ms.assetid: cf624c1f-c160-46a1-bb2b-213587688da7
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# Reliability Best Practices
Le regole per l'ottimizzazione dell'affidabilità indicate di seguito riguardano specificamente SQL Server, ma sono valide per qualsiasi applicazione server basata su host.  È estremamente importante che nei server, ad esempio SQL Server, non si verifichino problemi di perdita di risorse e arresto del sistema.  Non è tuttavia possibile ottenere questo risultato scrivendo codice di back\-out per ogni metodo che determina la modifica dello stato di un oggetto.  L'obiettivo da raggiungere non è quello di scrivere codice gestito completamente affidabile, in grado di correggere qualsiasi errore in qualunque posizione tramite codice di back\-out.  Sarebbe un'attività estremamente impegnativa con scarse probabilità di successo.  Common Language Runtime \(CLR\) non è sempre in grado di offrire garanzie sufficienti riguardo alla possibilità di scrivere codice perfetto in base al codice gestito.  Inoltre, a differenza di ASP.NET, SQL Server viene eseguito in un unico processo che non può essere riciclato senza disabilitare il database per un periodo di tempo eccessivamente lungo.  
  
 In considerazione delle garanzie limitate di CLR e dell'esecuzione di SQL Server in un unico processo, l'affidabilità risulta basata sull'interruzione dei thread o sul riciclo dei domini applicazioni, quando necessario, nonché sull'adozione di precauzioni per evitare che si verifichino perdite di risorse del sistema operativo quali handle o memoria.  Anche in questo modo, comunque, i requisiti per l'affidabilità rimangono rilevanti:  
  
-   Non devono mai verificarsi perdite di risorse del sistema operativo.  
  
-   Tutti i blocchi gestiti, in qualsiasi formato, devono essere identificati in CLR.  
  
-   Lo stato condiviso tra domini applicazioni non deve mai essere interrotto, in modo che il riciclo di <xref:System.AppDomain> venga eseguito correttamente.  
  
 Anche se a livello teorico è possibile scrivere codice gestito per gestire le eccezioni <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> e <xref:System.OutOfMemoryException>, non è ragionevole aspettarsi che gli sviluppatori scrivano codice con un tale livello di dettaglio per un'intera applicazione.  Per questo motivo, le eccezioni fuori banda determinano l'interruzione del thread in esecuzione. Se al momento dell'interruzione del thread era in corso la modifica di uno stato condiviso, situazione accertabile in base alla presenza di un blocco di proprietà del thread, l'oggetto <xref:System.AppDomain> viene scaricato.  Quando un metodo utilizzato per la modifica dello stato condiviso viene interrotto, lo stato viene danneggiato perché non è possibile scrivere codice di back\-out affidabile per le attività di aggiornamento dello stato condiviso.  
  
 In .NET Framework versione 2.0 l'unico host che presenta requisiti di affidabilità è SQL Server.  Se l'assembly è destinato all'esecuzione su SQL Server, è opportuno verificare che i requisiti di affidabilità siano soddisfatti per ogni parte dell'assembly, anche se è prevista la disabilitazione di specifiche funzionalità durante l'esecuzione nel database.  Questa verifica è necessaria perché il motore di analisi del codice esamina il codice a livello di assembly e non è in grado di distinguere il codice disabilitato.  In ambito di programmazione SQL Server è anche necessario tenere presente che SQL Server viene sempre eseguito in un unico processo e che il riciclo di <xref:System.AppDomain> viene utilizzato per la pulitura di tutte le risorse, quali la memoria e gli handle del sistema operativo.  
  
 Per il codice di back\-out, non è possibile basarsi unicamente su finalizzatori, distruttori o blocchi `try/finally`,  che potrebbero essere interrotti o non essere chiamati.  
  
 La generazione di eccezioni asincrone, <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> e <xref:System.OutOfMemoryException>, può verificarsi in posizioni impreviste, ipoteticamente in ogni istruzione del linguaggio macchina.  
  
 I thread gestiti non sono necessariamente thread Win32 in SQL. Possono anche essere fiber.  
  
 La modifica dello stato condiviso modificabile tra domini applicazioni o a livello di processo è un'operazione estremamente difficile che comporta dei rischi. Si consiglia quindi di evitarla, quando possibile.  
  
 Le condizioni di memoria insufficiente non sono rare in SQL Server.  
  
 Se lo stato condiviso delle librerie contenute in SQL Server non viene aggiornato correttamente, esiste un'alta probabilità che il codice non venga ripristinato fino al riavvio del database.  In alcuni casi estremi è inoltre possibile che, a causa di questa situazione, si verifichi un errore nel processo SQL Server e che quindi venga riavviato il database.  Il riavvio del database può determinare la disabilitazione di un sito Web o può influire sui processi operativi aziendali, con effetti negativi sulla disponibilità.  Una perdita lenta ma costante di risorse del sistema operativo, quali handle o memoria, può impedire al server di allocare gli handle, senza alcuna possibilità di ripristino, oppure può determinare, a lungo termine, una riduzione delle prestazioni del server e della disponibilità delle applicazioni dei clienti.  È chiaramente opportuno evitare scenari di questo tipo.  
  
## Regole per le procedure consigliate  
 Nell'introduzione sono stati evidenziati i criteri su cui è opportuno basare l'analisi del codice gestito in esecuzione sul server per aumentare la stabilità e l'affidabilità del framework.  Tutti questi controlli, che sono in genere consigliati in qualsiasi situazione, rappresentano un requisito indispensabile per il corretto funzionamento del server.  
  
 In caso di deadlock o di limitazione di risorse, in SQL Server viene interrotto un thread o viene eliminato un oggetto <xref:System.AppDomain>.  Quando si verifica una situazione di questo tipo, è garantita solo l'esecuzione del codice di back\-out in un'area a esecuzione vincolata \(CER, Constrained Execution Region\).  
  
### Utilizzare SafeHandle per evitare perdite di risorse  
 In caso di scaricamento di un oggetto <xref:System.AppDomain>, non è possibile dipendere esclusivamente dall'esecuzione di finalizzatori o di blocchi `finally`. È quindi importante astrarre l'accesso a ogni risorsa del sistema operativo tramite la classe <xref:System.Runtime.InteropServices.SafeHandle> anziché <xref:System.IntPtr>, <xref:System.Runtime.InteropServices.HandleRef> o una classe simile.  Ciò consente a CLR di rilevare e chiudere l'handle utilizzate anche in caso di eliminazione di <xref:System.AppDomain>.  <xref:System.Runtime.InteropServices.SafeHandle> utilizzerà un finalizzatore critico che CLR eseguirà sempre.  
  
 L'handle del sistema operativo rimane archiviato nell'handle Safe dal momento della creazione fino a quello del rilascio.  In nessun momento può verificarsi un'eccezione <xref:System.Threading.ThreadAbortException> con perdita di un handle.  Inoltre, la funzione di platform invoke eseguirà il conteggio dei riferimenti dell'handle, consentendo di tenerne traccia per l'intera durata e impedendo un eventuale problema di sicurezza dovuto a una race condition tra `Dispose` e un metodo che fa attualmente uso dell'handle.  
  
 Quasi tutte le classi che attualmente dispongono di un finalizzatore solo per eliminare un handle del sistema operativo non ne avranno più bisogno.  Il finalizzatore sarà incluso nella classe derivata <xref:System.Runtime.InteropServices.SafeHandle>.  
  
 Si noti che <xref:System.Runtime.InteropServices.SafeHandle> non sostituisce <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>.  Dall'eliminazione esplicita delle risorse del sistema operativo possono ancora derivare potenziali vantaggi in termini di prestazioni e di risoluzione di conflitti di risorse.  Al riguardo, è sufficiente considerare che i blocchi `finally` che eseguono l'eliminazione esplicita di risorse possono non essere eseguiti completamente.  
  
 La classe <xref:System.Runtime.InteropServices.SafeHandle> consente di implementare un metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> che esegue le operazioni appropriate per liberare l'handle, ad esempio passando lo stato a una routine di rilascio degli handle del sistema operativo oppure liberando un insieme di handle in un ciclo.  L'esecuzione di questo metodo è garantita da CLR.  È responsabilità dell'autore dell'implementazione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> assicurarsi che l'handle venga rilasciato in qualsiasi circostanza.  In caso contrario, l'handle andrà perso, con conseguente possibile perdita delle risorse native associate.  È pertanto estremamente importante strutturare le classi derivate di <xref:System.Runtime.InteropServices.SafeHandle> in modo che l'implementazione del metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> non richieda l'allocazione di alcuna risorsa che potrebbe non risultare disponibile al momento della chiamata.  Si noti che è consentito chiamare metodi che possono generare errori nell'ambito dell'implementazione di <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>, purché il codice riesca a gestire tali errori e a rispettare il contratto per rilasciare l'handle nativo.  Ai fini del debug, <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> restituisce un valore <xref:System.Boolean>, che può essere impostato su `false` qualora si verifichi un errore irreversibile che impedisce il rilascio della risorsa.  In questo modo, verrà attivato l'assistente al debug gestito \(MDA, Managed Debugging Assistant\) [releaseHandleFailed](../../../docs/framework/debug-trace-profile/releasehandlefailed-mda.md), se abilitato, per facilitare l'identificazione del problema.  Non vi saranno altri effetti su CLR. <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> non verrà chiamato di nuovo per la stessa risorsa e, di conseguenza, l'handle andrà perso.  
  
 <xref:System.Runtime.InteropServices.SafeHandle> non è appropriato in determinati contesti.  Poiché il metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> può essere eseguito su un thread finalizzatore <xref:System.GC>, non è opportuno eseguire il wrapping in un oggetto <xref:System.Runtime.InteropServices.SafeHandle> degli handle che devono essere rilasciati su uno specifico thread.  
  
 I Runtime Callable Wrapper \(RCW\) possono essere eliminati da CLR senza codice aggiuntivo.  Per il codice che utilizza platform invoke e gestisce un oggetto COM come `IUnknown*` o <xref:System.IntPtr>, il codice deve essere riscritto per utilizzare un RCW.  <xref:System.Runtime.InteropServices.SafeHandle> potrebbe non essere adatto a questo scenario a causa della possibilità di metodo di rilascio non gestito che chiama nuovamente il codice gestito.  
  
#### Regola per l'analisi del codice  
 Utilizzare <xref:System.Runtime.InteropServices.SafeHandle> per incapsulare le risorse del sistema operativo.  Non utilizzare <xref:System.Runtime.InteropServices.HandleRef> né campi di tipo <xref:System.IntPtr>.  
  
### Assicurarsi che non sia necessario eseguire i finalizzatori per impedire perdite di risorse del sistema operativo  
 Controllare accuratamente i finalizzatori per accertarsi che non si verifichi la perdita di una risorsa critica del sistema operativo anche se questi non vengono eseguiti.  Diversamente da quanto avviene durante il normale scaricamento di <xref:System.AppDomain>, ossia quando un'applicazione viene eseguita in uno stato stabile o quando viene arrestato un server SQL Server, durante uno scaricamento improvviso di <xref:System.AppDomain>, gli oggetti non vengono finalizzati.  Accertarsi che non si verifichino perdite di risorse in caso di scaricamento improvviso perché la corretta esecuzione di un'applicazione non può essere garantita, ma è indispensabile che venga mantenuta l'integrità del server.  Utilizzare <xref:System.Runtime.InteropServices.SafeHandle> per liberare qualsiasi risorsa del sistema operativo.  
  
### Assicurarsi che non sia necessario eseguire le clausole finally per impedire perdite di risorse del sistema operativo  
 Poiché non è possibile garantire che le clausole `finally` vengano eseguite esternamente alle aree a esecuzione vincolata, gli sviluppatori di librerie non devono basarsi sul codice interno a un blocco `finally` per liberare le risorse gestite.  A questo scopo, si consiglia di utilizzare <xref:System.Runtime.InteropServices.SafeHandle>.  
  
#### Regola per l'analisi del codice  
 Per la pulitura delle risorse del sistema operativo, utilizzare <xref:System.Runtime.InteropServices.SafeHandle> anziché `Finalize`.  Per incapsulare le risorse, non utilizzare <xref:System.IntPtr>, ma <xref:System.Runtime.InteropServices.SafeHandle>.  Se è necessario che la clausola finally venga eseguita, inserirla in un'area a esecuzione vincolata.  
  
### Tutti i blocchi devono passare attraverso il codice di blocco gestito esistente  
 CLR deve essere in grado di identificare i casi di blocco del codice, in modo da stabilire se procedere all'eliminazione dell'oggetto <xref:System.AppDomain> anziché limitarsi alla sola interruzione del thread.  Quest'ultima può risultare pericolosa perché i dati elaborati dal thread possono rimanere in uno stato incoerente.  È pertanto necessario riciclare l'intero <xref:System.AppDomain>.  Dalla mancata identificazione di un blocco possono derivare situazioni di deadlock o risultati non corretti.  Per identificare le aree di blocco, utilizzare i metodi <xref:System.Threading.Thread.BeginCriticalRegion%2A> e <xref:System.Threading.Thread.EndCriticalRegion%2A>.  Si tratta di metodi statici inclusi nella classe <xref:System.Threading.Thread> e applicabili solo al thread corrente, che consentono di impedire a un thread di modificare il conteggio dei blocchi di un altro thread.  
  
 Poiché nei metodi <xref:System.Threading.Monitor.Enter%2A> e <xref:System.Threading.Monitor.Exit%2A> è incorporata questa notifica CLR, si consiglia di utilizzarli. Lo stesso vale per l'[Istruzione lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md), in cui questi metodi vengono utilizzati.  
  
 Gli altri meccanismi di blocco, ad esempio gli spinlock e l'oggetto <xref:System.Threading.AutoResetEvent>, devono chiamare questi metodi per notificare a CLR l'ingresso in una sezione critica.  Questi metodi non acquisiscono alcun blocco. Notificano semplicemente a CLR che il codice viene eseguito in una sezione critica e che l'interruzione del thread può causare problemi di incoerenza dello stato condiviso.  Se è stato definito un tipo di blocco specifico, ad esempio una classe <xref:System.Threading.ReaderWriterLock> personalizzata, utilizzare questi metodi di conteggio dei blocchi.  
  
#### Regola per l'analisi del codice  
 Contrassegnare e identificare tutti i blocchi tramite i metodi <xref:System.Threading.Thread.BeginCriticalRegion%2A> e <xref:System.Threading.Thread.EndCriticalRegion%2A>.  Non utilizzare <xref:System.Threading.Interlocked.CompareExchange%2A>, <xref:System.Threading.Interlocked.Increment%2A> e <xref:System.Threading.Interlocked.Decrement%2A> in un ciclo.  Non eseguire un platform invoke delle varianti Win32 di questi metodi.  Non utilizzare <xref:System.Threading.Thread.Sleep%2A> in un ciclo  né campi di tipo volatile.  
  
### Inserire il codice di pulitura in un blocco finally o catch, non dopo un blocco catch  
 Il codice di pulitura non deve mai seguire un blocco `catch`, ma deve essere sempre inserito in un blocco `finally` o nel blocco `catch` stesso.  Questa dovrebbe essere la normale procedura da seguire.  Un blocco `finally` è in genere preferibile perché esegue lo stesso codice sia quando viene generata un'eccezione sia quando viene rilevata normalmente la fine del blocco `try`.  Se viene generata un'eccezione imprevista, ad esempio <xref:System.Threading.ThreadAbortException>, il codice di pulitura non verrà eseguito.  Affinché non si verifichino perdite, è opportuno eseguire il wrapping delle risorse non gestite, di cui viene normalmente eseguita la pulitura in un blocco `finally`, in un oggetto <xref:System.Runtime.InteropServices.SafeHandle>.  Per eliminare in modo efficace gli oggetti, inclusi gli handle, è possibile utilizzare la parola chiave `using` di C\#.  
  
 Anche se le risorse sul thread finalizzatore possono essere eliminate mediante il riciclo di <xref:System.AppDomain>, è importante inserire il codice di pulitura nella posizione corretta.  Si noti che, se un thread riceve un'eccezione asincrona senza avere il controllo di un blocco, CLR tenterà di interrompere il thread senza eseguire il riciclo di <xref:System.AppDomain>.  Accertarsi che le risorse vengano sottoposte al processo di pulitura il prima possibile per aumentarne la disponibilità e migliorarne la durata.  Se l'handle di un file in un percorso di codice di errore non viene chiuso esplicitamente, attendere che venga eliminato dal finalizzatore <xref:System.Runtime.InteropServices.SafeHandle>. Alla successiva esecuzione, il codice potrebbe non riuscire ad accedere allo stesso file se il finalizzatore non è ancora stato eseguito.  Per questo motivo è opportuno, anche se non obbligatorio, verificare che il codice di pulitura sia effettivamente disponibile e funzionante affinché gli errori possano essere corretti in modo più semplice e veloce.  
  
#### Regola per l'analisi del codice  
 Il codice di pulitura che segue la clausola `catch` deve essere inserito in blocco `finally`.  Inserire le chiamate per l'eliminazione delle risorse in un blocco finally. I blocchi `catch` devono terminare in un'istruzione throw o rethrow.  Se esiste la possibilità che vengano generate eccezioni, ad esempio durante la verifica della possibilità di stabilire una connessione di rete, in cui può essere rilevata una delle numerose eccezioni possibili, qualsiasi codice che in circostanze normali richiede la rilevazione di un certo numero di eccezioni dovrebbe indicare la necessità di eseguire test per controllare se l'elaborazione avrà esito positivo.  
  
### Eliminare lo stato condiviso modificabile a livello di processo tra i domini applicazioni o utilizzare un'area a esecuzione vincolata  
 Come indicato nell'introduzione, è difficile scrivere codice gestito con cui monitorare lo stato condiviso a livello di processo tra i domini applicazioni in maniera affidabile.  Per stato condiviso a livello di processo si intende qualsiasi tipo di struttura dati condivisa tra domini applicazioni, in codice Win32, all'interno di CLR o in codice gestito che utilizza servizi remoti.  La scrittura di uno stato condiviso modificabile in codice gestito è un'operazione particolarmente complessa, da eseguire con estrema attenzione.  Se esiste uno stato condiviso a livello di processo o computer, trovare un modo per eliminarlo oppure proteggerlo tramite un'area a esecuzione vincolata.  Si noti che qualsiasi libreria con stato condiviso non identificato o non corretto può determinare l'arresto anomalo di un host, ad esempio SQL Server, che richiede lo scaricamento pulito di <xref:System.AppDomain>.  
  
 Se il codice utilizza un oggetto COM, evitare di condividere tale oggetto tra i domini applicazioni.  
  
### Blocchi non funzionanti a livello di processo o tra domini applicazioni  
 In precedenza, il metodo <xref:System.Threading.Monitor.Enter%2A> e l'[Istruzione lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md) venivano utilizzati per creare blocchi di processo globali,  che si verificano ad esempio impostando un blocco sulle classi flessibili di <xref:System.AppDomain>, quali le istanze di <xref:System.Type> da assembly non condivisi, gli oggetti <xref:System.Threading.Thread>, le stringhe interne e alcune stringhe condivise tra domini applicazioni tramite servizi remoti.  Questi blocchi non sono più validi a livello di processo.  Per individuare la presenza di un blocco tra diversi domini applicazioni a livello di processo, determinare se il codice all'interno del blocco fa uso di risorse esterne persistenti, ad esempio un file su disco o eventualmente un database.  
  
 Si noti che l'acquisizione di un blocco all'interno di un oggetto <xref:System.AppDomain> può provocare problemi nel caso in cui il codice protetto utilizzi una risorsa esterna, perché tale codice può essere eseguito simultaneamente tra più domini applicazioni.  Questa situazione può costituire un problema quando si eseguono operazioni di scrittura in un file di log o di associazione a un socket per l'intero processo.  Queste modifiche indicano che non esiste una tecnica semplice, tramite il codice gestito, per ottenere un blocco globale del processo se non utilizzando un'istanza denominata di <xref:System.Threading.Mutex> o <xref:System.Threading.Semaphore>.  Creare codice che non viene eseguito simultaneamente in due domini applicazioni oppure utilizzare la classe <xref:System.Threading.Mutex> o <xref:System.Threading.Semaphore>.  Se il codice esistente non può essere modificato, non utilizzare un mutex denominato Win32 per ottenere la sincronizzazione perché l'esecuzione in modalità fiber implica l'impossibilità di garantire che un mutex venga acquisito e rilasciato dallo stesso thread del sistema operativo.  È necessario utilizzare la classe gestita <xref:System.Threading.Mutex>, una classe denominata <xref:System.Threading.ManualResetEvent> o <xref:System.Threading.AutoResetEvent> oppure una classe <xref:System.Threading.Semaphore> per sincronizzare il blocco del codice in modo che CLR ne sia consapevole anziché sincronizzare il blocco tramite codice non gestito.  
  
#### Evitare lock\(typeof\(MyType\)\)  
 Anche gli oggetti <xref:System.Type> pubblici e privati inclusi in assembly condivisi, con una sola copia del codice condiviso tra tutti i domini applicazioni, presentano problemi.  Per gli assembly condivisi esiste un'unica istanza di un oggetto <xref:System.Type> per processo e, di conseguenza, la stessa istanza di <xref:System.Type> viene condivisa da più domini applicazioni.  L'acquisizione di un blocco su un'istanza di <xref:System.Type> ha effetto sull'intero processo e non solo sull'oggetto <xref:System.AppDomain>.  Se un oggetto <xref:System.AppDomain> acquisisce un blocco su un oggetto <xref:System.Type>, il thread viene interrotto improvvisamente senza il rilascio del blocco,  che può quindi causare una situazione di deadlock in altri domini applicazioni.  
  
 Una tecnica efficace per acquisire blocchi in metodi statici consiste nell'aggiungere al codice un oggetto statico di sincronizzazione interna.  Questo oggetto può essere inizializzato nel costruttore della classe, se disponibile, o altrimenti nel modo seguente:  
  
```  
private static Object s_InternalSyncObject;  
private static Object InternalSyncObject   
{  
    get   
    {  
        if (s_InternalSyncObject == null)   
        {  
            Object o = new Object();  
            Interlocked.CompareExchange(  
                ref s_InternalSyncObject, o, null);  
        }  
        return s_InternalSyncObject;  
    }  
}  
```  
  
 Quando si acquisisce un blocco, utilizzare la proprietà `InternalSyncObject` per ottenere un oggetto a cui applicare il blocco.  Questa proprietà non deve essere utilizzata se l'oggetto di sincronizzazione interna è stato inizializzato nel costruttore della classe.  Il codice di inizializzazione del blocco per la verifica dovrebbe essere simile al seguente:  
  
```  
public static MyClass SingletonProperty   
{  
    get   
    {  
        if (s_SingletonProperty == null)   
        {  
            lock(InternalSyncObject)   
            {  
                // Do not use lock(typeof(MyClass))   
                if (s_SingletonProperty == null)   
                {  
                    MyClass tmp = new MyClass(…);     
                    // Do all initialization before publishing  
                    s_SingletonProperty = tmp;  
                }  
            }  
        }  
        return s_SingletonProperty;  
    }  
}  
```  
  
#### Nota su Lock\(this\)  
 È in genere possibile acquisire un blocco su un singolo oggetto accessibile pubblicamente.  Se tuttavia si tratta di un oggetto Singleton, da cui può derivare il deadlock dell'intero sottosistema, è opportuno prendere in considerazione anche la possibilità di utilizzare il modello di progettazione indicato in precedenza.  Un blocco sul singolo oggetto <xref:System.Security.SecurityManager> può ad esempio causare un deadlock all'interno di <xref:System.AppDomain> rendendo l'intero <xref:System.AppDomain> inutilizzabile.  È consigliabile non acquisire alcun blocco su un oggetto accessibile pubblicamente di questo tipo.  Tuttavia, un blocco su una matrice o una raccolta singola non dovrebbe in genere presentare problemi.  
  
#### Regola per l'analisi del codice  
 Non acquisire blocchi su tipi che possono essere utilizzati tra domini applicazioni o che non hanno una forte identità.  Non chiamare il metodo <xref:System.Threading.Monitor.Enter%2A> su un oggetto <xref:System.Type>, <xref:System.Reflection.MethodInfo>, <xref:System.Reflection.PropertyInfo>, <xref:System.String>, <xref:System.ValueType>, <xref:System.Threading.Thread> o qualsiasi oggetto derivato da <xref:System.MarshalByRefObject>.  
  
### Rimuovere le chiamate GC.KeepAlive  
 In una quantità significativa di codice esistente, il metodo <xref:System.GC.KeepAlive%2A> non viene utilizzato quando opportuno o viceversa viene utilizzato quando non opportuno.  Dopo la conversione in <xref:System.Runtime.InteropServices.SafeHandle>, le classi non devono chiamare <xref:System.GC.KeepAlive%2A>, supponendo che non dispongano di un finalizzatore ma si basino su <xref:System.Runtime.InteropServices.SafeHandle> per finalizzare gli handle del sistema operativo.  Mentre i costi a livello di prestazioni risultanti dal mantenimento di una chiamata a <xref:System.GC.KeepAlive%2A> sono trascurabili, la percezione che una chiamata a <xref:System.GC.KeepAlive%2A> sia necessaria o sufficiente per la risoluzione di un problema di durata, che potrebbe non esistere più, rende più difficile la gestione del codice.  Tuttavia, quando si utilizzano i Runtime Callable Wrapper di interoperabilità COM, il metodo <xref:System.GC.KeepAlive%2A> è ancora necessario.  
  
#### Regola per l'analisi del codice  
 Rimuovere <xref:System.GC.KeepAlive%2A>.  
  
### Utilizzare l'attributo di protezione host  
 La classe <xref:System.Security.Permissions.HostProtectionAttribute>, relativa all'attributo di protezione host, consente di utilizzare azioni di protezione dichiarativa per determinare i requisiti di protezione host. In questo modo, l'host può impedire anche al codice completamente attendibile di chiamare metodi non appropriati per l'host stesso, quali <xref:System.Environment.Exit%2A> o <xref:System.Windows.Forms.MessageBox.Show%2A> per SQL Server.  
  
 L'attributo di protezione host influisce solo sulle applicazioni non gestite che ospitano Common Language Runtime e implementano la protezione host, ad esempio SQL Server.  Quando applicata, l'azione di protezione ha per effetto la creazione di una richiesta di collegamento in base alle risorse host esposte dalla classe o dal metodo.  Se il codice viene eseguito in un'applicazione client o su un server privo di protezione host, l'attributo non ha alcun effetto. Non viene rilevato e quindi nemmeno applicato.  
  
> [!IMPORTANT]
>  Lo scopo di questo attributo è di imporre le regole del modello di programmazione specifico per l'host, non il comportamento di sicurezza.  Anche se per la verifica della conformità ai requisiti del modello di programmazione viene utilizzata una richiesta di collegamento, la classe <xref:System.Security.Permissions.HostProtectionAttribute> non è un'autorizzazione di sicurezza.  
  
 Se l'host non dispone di requisiti del modello di programmazione, non verranno effettuate richieste di collegamento.  
  
 Questo attributo consente di identificare:  
  
-   Metodi o classi non idonei per il modello di programmazione dell'host, tuttavia benigni.  
  
-   Metodi o classi che non sono idonei per il modello di programmazione dell'host e che potrebbero portare alla destabilizzazione del codice utente gestito dal server.  
  
-   Metodi o classi che non sono idonei per il modello di programmazione dell'host e che potrebbero portare alla destabilizzazione del processo server stesso.  
  
> [!NOTE]
>  Se si crea una libreria di classi che verrà chiamata da applicazioni eseguibili in un ambiente host protetto, è necessario applicare questo attributo ai membri che espongono categorie di risorse dell'enumerazione <xref:System.Security.Permissions.HostProtectionResource>.  I membri della libreria di classi .NET Framework con questo attributo provocano solo la verifica del chiamante immediato.  Analogamente, anche i membri della propria libreria devono determinare il controllo del rispettivo chiamante immediato.  
  
 Per ulteriori informazioni sull'attributo di protezione host, vedere <xref:System.Security.Permissions.HostProtectionAttribute>.  
  
#### Regola per l'analisi del codice  
 Per SQL Server, tutti i metodi utilizzati per introdurre la sincronizzazione o il threading devono essere identificati con l'attributo di protezione host.  Tra questi metodi sono inclusi quelli che condividono lo stato, sono sincronizzati o gestiscono processi esterni.  I valori di <xref:System.Security.Permissions.HostProtectionResource> che influiscono su SQL Server sono <xref:System.Security.Permissions.HostProtectionResource>, <xref:System.Security.Permissions.HostProtectionResource> e <xref:System.Security.Permissions.HostProtectionResource>.  Tuttavia, l'identificazione con un attributo di protezione host è necessaria per tutti i metodi che espongono un qualsiasi oggetto <xref:System.Security.Permissions.HostProtectionResource>, non solo per quelli che utilizzano risorse che influiscono su SQL.  
  
### Non inserire blocchi indefiniti nel codice gestito  
 L'inserimento di un blocco in codice non gestito anziché gestito può determinare un attacco di tipo Denial of Service perché CLR non è in grado di interrompere il thread.  Un thread bloccato impedisce lo scaricamento di <xref:System.AppDomain>, se non mediante l'esecuzione di operazioni estremamente inaffidabili.  L'inserimento di un blocco tramite una primitiva di sincronizzazione Win32 non è ammissibile.  Se possibile, è opportuno evitare di inserire un blocco in una chiamata a `ReadFile` in un socket. In una situazione ideale, l'API Win32 dovrebbe fornire un meccanismo che imponga il timeout di un'operazione di questo tipo.  
  
 Tutti i metodi che effettuano chiamate all'interno di codice nativo dovrebbero utilizzare una chiamata Win32 con un valore finito di timeout.  Anche se autorizzato a specificare il timeout, l'utente non deve avere la possibilità di impostare un timeout infinito, a meno che non disponga di specifiche autorizzazioni di sicurezza.  Come indicazione generale, tenere presente che, se un metodo si blocca per più di 10 secondi, sarà necessario utilizzare una versione con supporto per i timeout o disporre di supporto CLR aggiuntivo.  
  
 Di seguito sono illustrati alcuni esempi di API problematiche.  Le pipe, sia anonime sia denominate, possono essere create senza timeout. È tuttavia necessario verificare che né `CreateNamedPipe` né `WaitNamedPipe` venga mai chiamato con NMPWAIT\_WAIT\_FOREVER.  È inoltre possibile che si verifichi un blocco imprevisto anche se è specificato un timeout.  La chiamata a `WriteFile` su una pipe unnamed causa un blocco finché non vengono scritti tutti i byte e pertanto, se nel buffer sono presenti dati non letti, il blocco determinato dalla chiamata a `WriteFile` si protrarrà finché il lettore non libera spazio nel buffer della pipe.  I socket dovrebbero sempre utilizzare API che rispettano un meccanismo di timeout.  
  
#### Regola per l'analisi del codice  
 Un blocco senza timeout in codice non gestito è un attacco di tipo Denial of Service.  Non eseguire richiami piattaforma su `WaitForSingleObject`, `WaitForSingleObjectEx`, `WaitForMultipleObjects`, `MsgWaitForMultipleObjects` e `MsgWaitForMultipleObjectsEx`.  Non utilizzare NMPWAIT\_WAIT\_FOREVER.  
  
### Identificare le funzionalità dipendenti da apartment a thread singolo  
 Identificare il codice in cui vengono utilizzati apartment a thread singolo \(STA, Single\-Threaded Apartment\),  che sono disabilitati nel processo SQL Server.  Le funzionalità che dipendono da `CoInitialize`, ad esempio i contatori delle prestazioni o gli Appunti, devono essere disabilitate in SQL Server.  
  
### Assicurarsi che i finalizzatori non presentino problemi di sincronizzazione  
 È possibile che nelle versioni future di .NET Framework siano disponibili più thread finalizzatori e che pertanto vengano eseguiti simultaneamente i finalizzatori appartenenti a istanze diverse dello stesso tipo.  Non è necessario che i finalizzatori siano completamente thread\-safe perché il Garbage Collector garantisce che il finalizzatore per un'istanza di un determinato oggetto venga eseguito da un unico thread.  È tuttavia necessario che i finalizzatori vengano codificati per evitare situazioni di race condition e deadlock quando eseguiti simultaneamente su più istanze di oggetti diversi.  Per utilizzare un qualsiasi stato esterno in un finalizzatore, ad esempio per scrivere in un file di log, è necessario gestire problemi di threading.  Non fare affidamento sulla finalizzazione per fornire funzionalità thread\-safe.  Non utilizzare l'archiviazione locale di thread, gestita o nativa, per archiviare i dati statici nel thread finalizzatore.  
  
#### Regola per l'analisi del codice  
 I finalizzatori non devono presentare alcun problema di sincronizzazione.  Non utilizzare uno stato modificabile statico in un finalizzatore.  
  
### Evitare di utilizzare memoria non gestita, se possibile  
 La memoria non gestita può andare perduta, proprio come un handle del sistema operativo.  Se possibile, provare a utilizzare la memoria nello stack tramite [stackalloc](../Topic/stackalloc%20\(C%23%20Reference\).md), un oggetto gestito bloccato quale l'[Istruzione fixed](../Topic/fixed%20Statement%20\(C%23%20Reference\).md) o un oggetto <xref:System.Runtime.InteropServices.GCHandle> che fa uso di un byte\[\].  Questi verranno eventualmente eliminati da <xref:System.GC>.  Se tuttavia è necessario allocare memoria non gestita, prendere in considerazione l'opportunità di utilizzare una classe derivata da <xref:System.Runtime.InteropServices.SafeHandle> per il wrapping dell'allocazione della memoria.  
  
 Si noti che esiste almeno un caso in cui <xref:System.Runtime.InteropServices.SafeHandle> non è adeguato.  Per le chiamate di metodi COM che allocano o liberano memoria, viene in genere utilizzata una DLL per allocare memoria tramite `CoTaskMemAlloc`, seguita da un'altra DLL per liberare la memoria allocata tramite `CoTaskMemFree`.  L'utilizzo di <xref:System.Runtime.InteropServices.SafeHandle> in questi contesti risulta inappropriato perché questo oggetto tenta di associare la durata della memoria non gestita alla durata di <xref:System.Runtime.InteropServices.SafeHandle>, anziché consentire che venga controllata dall'altra DLL.  
  
### Esaminare tutti gli usi di Catch\(Exception\)  
 I blocchi catch che rilevano tutte le eccezioni, anziché un'eccezione specifica, sono ora in grado di rilevare anche le eccezioni asincrone.  Esaminare ogni blocco catch\(Exception\) verificando che non sia presente codice di back\-out o di rilascio di risorse importanti che potrebbe essere ignorato oppure un comportamento potenzialmente non corretto per la gestione di un'eccezione <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> o <xref:System.OutOfMemoryException>.  Si noti che nel codice possono esistere dei presupposti in base ai quali vengono rilevate solo determinate eccezioni oppure l'errore di un'eccezione è sempre dovuto a un motivo specifico.  È possibile che questi presupposti debbano essere aggiornati in modo da includere <xref:System.Threading.ThreadAbortException>.  
  
 Prendere in considerazione l'opportunità di modificare tutti i punti in cui vengono rilevate eccezioni in modo da rilevare un tipo specifico di eccezione che si prevede venga generato, ad esempio un'eccezione <xref:System.FormatException> dai metodi di formattazione delle stringhe.  In questo modo è possibile impedire l'esecuzione del blocco catch in caso di eccezioni impreviste e garantire che il codice non nasconda bug rilevando eccezioni di questo tipo.  Come regola generale, evitare sempre di gestire un'eccezione nel codice di libreria. In questo caso, infatti, la necessità di rilevare un'eccezione può indicare la presenza di un difetto di progettazione nel codice chiamato.  In alcune circostanze è opportuno rilevare un'eccezione e generarne un'altra di tipo diverso per fornire più dati.  A tale scopo, utilizzare eccezioni annidate, archiviando la causa effettiva dell'errore nella proprietà <xref:System.Exception.InnerException%2A> della nuova eccezione.  
  
#### Regola per l'analisi del codice  
 Esaminare tutti i blocchi catch nel codice gestito che rilevano tutti gli oggetti o tutte le eccezioni.  Nel linguaggio C\# questo significa contrassegnare sia `catch` {} che `catch(Exception)` {}.  Prendere in considerazione l'opportunità di rendere specifico il tipo di eccezione oppure esaminare il codice per assicurarsi che non si verifichino comportamenti non corretti qualora venga rilevata un'eccezione di tipo imprevisto.  
  
### Non presupporre che un thread gestito sia un thread Win32: è un fiber  
 È possibile utilizzare l'archiviazione locale di thread gestita, ma non quella non gestita, né è possibile presupporre che il codice venga eseguito di nuovo nel thread del sistema operativo corrente.  Non modificare impostazioni quali le impostazioni locali del thread.  Non chiamare `InitializeCriticalSection` o `CreateMutex` tramite platform invoke perché è necessario che un thread del sistema operativo che entra in un blocco possa anche uscirne.  Poiché con i fiber questo non si verifica, non è possibile utilizzare mutex e sezioni critiche Win32 in SQL in modo diretto.  Si noti che la classe gestita <xref:System.Threading.Mutex> non gestisce questi problemi di affinità di thread.  
  
 È possibile utilizzare senza alcun rischio la maggior parte dei dati sullo stato in un oggetto gestito <xref:System.Threading.Thread>, incluse l'archiviazione locale di thread gestita e le impostazioni cultura correnti dell'interfaccia utente del thread.  È inoltre possibile utilizzare l'oggetto <xref:System.ThreadStaticAttribute>, che limita l'accessibilità del valore di una variabile statica esistente al solo thread gestito corrente. Si tratta di una tecnica alternativa per gestire l'archiviazione locale dei fiber in CLR.  Per motivi legati al modello di programmazione, non è consentito modificare le impostazioni cultura correnti di un thread durante l'esecuzione in SQL.  
  
#### Regola per l'analisi del codice  
 SQL Server viene eseguito in modalità fiber. Non utilizzare l'archiviazione locale di thread.  Evitare richiami piattaforma a `TlsAlloc`, `TlsFree`, `TlsGetValue` e `TlsSetValue.`  
  
### Consentire a SQL Server di gestire la rappresentazione  
 Poiché la rappresentazione opera a livello di thread e SQL può essere eseguito in modalità fiber, il codice gestito non deve rappresentare utenti né chiamare `RevertToSelf`.  
  
#### Regola per l'analisi del codice  
 Consentire a SQL Server di gestire la rappresentazione.  Non utilizzare `RevertToSelf`, `ImpersonateAnonymousToken`, `DdeImpersonateClient`, `ImpersonateDdeClientWindow`, `ImpersonateLoggedOnUser`, `ImpersonateNamedPipeClient`, `ImpersonateSelf`, `RpcImpersonateClient`, `RpcRevertToSelf`, `RpcRevertToSelfEx` o `SetThreadToken`.  
  
### Non chiamare Thread::Suspend  
 Nonostante possa sembrare un'operazione semplice, la sospensione di un thread è in grado di causare situazioni di deadlock.  Se un thread che utilizza un blocco viene sospeso da un secondo thread e quest'ultimo tenta di acquisire lo stesso blocco, si verificherà un deadlock. <xref:System.Threading.Thread.Suspend%2A> può interferire con la sicurezza, il caricamento delle classi, i servizi remoti e reflection.  
  
#### Regola per l'analisi del codice  
 Non chiamare <xref:System.Threading.Thread.Suspend%2A>.  Prendere invece in considerazione l'opportunità di utilizzare una primitiva di sincronizzazione effettiva, ad esempio un oggetto <xref:System.Threading.Semaphore> o <xref:System.Threading.ManualResetEvent>.  
  
### Proteggere le operazioni critiche con aree a esecuzione vincolata e contratti di affidabilità  
 Quando si esegue un'operazione complessa che determina l'aggiornamento di uno stato condiviso o che deve avere esito completamente positivo o negativo, assicurarsi che questa venga protetta da un'area a esecuzione vincolata.  In questo modo si ha la sicurezza che il codice venga eseguito in ogni caso, anche se si verifica un'interruzione improvvisa del thread o uno scaricamento improvviso di <xref:System.AppDomain>.  
  
 Un'area a esecuzione vincolata consiste in un particolare blocco `try/finally`, immediatamente preceduto da una chiamata a <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>.  
  
 Quando è impostata un'area a esecuzione vincolata, il compilatore just\-in\-time viene istruito in modo da preparare tutto il codice nel blocco finally prima dell'esecuzione del blocco `try`.  Si ha così la garanzia che il codice nel blocco finally venga compilato ed eseguito in ogni caso.  È talvolta possibile che in un'area a esecuzione vincolata si trovi un blocco `try` vuoto.  L'utilizzo di un'area di questo tipo garantisce la protezione da interruzioni di thread asincrone ed eccezioni di memoria insufficiente.  Per un formato di area a esecuzione vincolata in grado di gestire anche gli overflow dello stack per codice eccessivamente dettagliato, vedere <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>.  
  
## Vedere anche  
 <xref:System.Runtime.ConstrainedExecution>   
 [SQL Server Programming and Host Protection Attributes](../../../docs/framework/performance/sql-server-programming-and-host-protection-attributes.md)