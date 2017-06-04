---
title: "Traccia e strumentazione di applicazioni | Microsoft Docs"
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
  - "traccia [.NET Framework]"
  - "strumentazione, debug [.NET Framework]"
  - "monitoraggio delle prestazioni, Strumentazione"
  - "strumentazione, informazioni"
  - "traccia [.NET Framework], informazioni sull'analisi"
  - "monitoraggio delle prestazioni, analisi del codice"
  - "Trace (classe), strumentazione per applicazioni .NET"
ms.assetid: 773b6fc4-9013-4322-b728-5dec7a72e743
caps.latest.revision: 21
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 21
---
# Traccia e strumentazione di applicazioni
La traccia consente di monitorare l'esecuzione dell'applicazione mentre è in corso. È possibile aggiungere strumentazione di traccia e debug all'applicazione .NET Framework quando la si sviluppa e usare tale strumentazione sia mentre si sviluppa l'applicazione sia dopo la distribuzione. È possibile utilizzare il <xref:System.Diagnostics.Trace?displayProperty=fullName>, <xref:System.Diagnostics.Debug?displayProperty=fullName>, e <xref:System.Diagnostics.TraceSource?displayProperty=fullName> classi per registrare le informazioni sugli errori e l'esecuzione dell'applicazione in log, file di testo o altri dispositivi per l'analisi successiva.  
  
 Il termine *strumentazione* si riferisce alla possibilità di monitorare o misurare il livello di prestazioni del prodotto e di diagnosticare gli errori. In programmazione, ciò significa la capacità di un'applicazione di incorporare:  
  
-   **Traccia del codice** -ricezione di messaggi informativi sull'esecuzione di un'applicazione in fase di esecuzione.  
  
-   **Debug** - rilevamento e correzione di errori di programmazione in un'applicazione in fase di sviluppo. Per ulteriori informazioni, vedere [debug](../Topic/Debugging%20in%20Visual%20Studio.md).  
  
-   **I contatori delle prestazioni** -componenti che consentono di tenere traccia delle prestazioni dell'applicazione. Per ulteriori informazioni, vedere [i contatori delle prestazioni](../../../docs/framework/debug-trace-profile/performance-counters.md).  
  
-   **I registri eventi** -componenti che consentono di ricevere e registrare i principali eventi durante l'esecuzione dell'applicazione. Per ulteriori informazioni, vedere il <xref:System.Diagnostics.EventLog> (classe).  
  
 La strumentazione dell'applicazione inserendo istruzioni di traccia in posizioni strategiche nel codice è particolarmente utile per le applicazioni distribuite. Usando istruzioni di traccia, è possibile instrumentare un'applicazione non solo per visualizzare informazioni in caso di problemi, ma anche per monitorare le prestazioni dell'applicazione.  
  
 Il <xref:System.Diagnostics.TraceSource> classe fornisce funzionalità di traccia avanzate e può essere utilizzato al posto dei metodi statici delle versioni precedenti <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> delle classi di traccia. La consueta <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> classi vengono ancora ampiamente usate, ma il <xref:System.Diagnostics.TraceSource> classe è consigliata per i nuovi comandi di traccia, ad esempio <xref:System.Diagnostics.TraceSource.TraceEvent%2A> e <xref:System.Diagnostics.TraceSource.TraceData%2A>.  
  
 Il <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> sono identiche, tranne che le procedure e funzioni di classi il <xref:System.Diagnostics.Trace> classe vengono compilate per impostazione predefinita nelle build di rilascio, mentre quelle del <xref:System.Diagnostics.Debug> non sono.  
  
 Il <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> classi consentono di monitorare ed esaminare le prestazioni dell'applicazione durante lo sviluppo o dopo la distribuzione. Ad esempio, è possibile utilizzare il <xref:System.Diagnostics.Trace> classe per tenere traccia di particolari tipi di azioni in un'applicazione distribuita appena si verificano (ad esempio la creazione di nuove connessioni a database) e monitorare quindi l'efficienza dell'applicazione.  
  
## <a name="code-tracing-and-debugging"></a>Traccia e debug del codice  
 Durante lo sviluppo, è possibile utilizzare i metodi di output di <xref:System.Diagnostics.Debug> classe per visualizzare i messaggi nella finestra di Output dell'ambiente di sviluppo integrato (IDE) di Visual Studio. Ad esempio:  
  
```vb  
Trace.WriteLine("Hello World!")  
Debug.WriteLine("Hello World!")  
  
```  
  
```csharp  
System.Diagnostics.Trace.WriteLine("Hello World!");  
System.Diagnostics.Debug.WriteLine("Hello World!");  
  
```  
  
 Ognuno di questi esempi consente di visualizzare "Hello World!" Nella finestra di Output quando l'applicazione viene eseguita nel debugger.  
  
 Ciò consente di eseguire il debug delle applicazioni e ottimizzarne le prestazioni in base al relativo comportamento nell'ambiente di test. È possibile eseguire il debug dell'applicazione nella build di debug con il <xref:System.Diagnostics.Debug> attributi condizionali attivato in modo da ricevere tutto l'output di debug. Quando l'applicazione è pronta per il rilascio, è possibile compilare la build di rilascio senza attivare il <xref:System.Diagnostics.Debug> attributo condizionale, in modo che il compilatore non includerà il codice di debug nell'eseguibile finale. Per ulteriori informazioni, vedere [procedura: compilare in modo condizionale con traccia e Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md). Per ulteriori informazioni su diverse configurazioni della build per l'applicazione, vedere [e compilazione](../Topic/Compiling%20and%20Building%20in%20Visual%20Studio.md).  
  
 È anche possibile tracciare esecuzione del codice in un'applicazione installata, utilizzando metodi di <xref:System.Diagnostics.Trace> (classe). Inserendo [opzioni di traccia](../../../docs/framework/debug-trace-profile/trace-switches.md) nel codice, è possibile controllare se l'analisi avviene e come sia approfondita. Ciò consente di monitorare lo stato dell'applicazione in un ambiente di produzione. Questo aspetto è particolarmente importante in un'applicazione aziendale che usa più componenti in esecuzione in più computer. È possibile controllare la modalità di utilizzo delle opzioni dopo la distribuzione tramite il file di configurazione. Per ulteriori informazioni, vedere [procedura: creare, inizializzare e configurare opzioni di traccia](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md).  
  
 Quando si sviluppa un'applicazione per la quale si prevede di usare la traccia, in genere si includono nel codice dell'applicazione sia i messaggi di traccia sia quelli di debug. Quando si è pronti per distribuire l'applicazione, è possibile compilare la build di rilascio senza attivare il **Debug** attributi condizionali. Tuttavia, è possibile attivare il **traccia** attributo condizionale in modo che il compilatore includa il codice di traccia nel file eseguibile. Per ulteriori informazioni, vedere [procedura: compilare in modo condizionale con traccia e Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md).  
  
### <a name="phases-of-code-tracing"></a>Fasi di traccia del codice  
 La traccia del codice comprende tre fasi:  
  
1.  **Strumentazione** , aggiungere codice di traccia nell'applicazione.  
  
2.  **Traccia** , ovvero il codice di traccia scrive le informazioni nella destinazione specificata.  
  
3.  **Analisi** , vengono valutate le informazioni di traccia per identificare e comprendere i problemi dell'applicazione.  
  
 Durante lo sviluppo, tutti i metodi di output di traccia e debug scrivono informazioni nella finestra di output di Visual Studio per impostazione predefinita. In un'applicazione distribuita, i metodi scrivono le informazioni di traccia nelle destinazioni specificate. Per ulteriori informazioni su come specificare una destinazione di output di tracciatura o di debug, vedere [listener di traccia](../../../docs/framework/debug-trace-profile/trace-listeners.md).  
  
 Di seguito è illustrata una panoramica dei passaggi principali eseguiti in genere per usare la traccia per analizzare e correggere i problemi potenziali nelle applicazioni distribuite. Per altre informazioni su come eseguire questi passaggi, fare clic sul collegamento appropriato.  
  
##### <a name="to-use-tracing-in-an-application"></a>Per usare la traccia in un'applicazione  
  
1.  Determinare l'output di traccia che si desidera ricevere dopo aver distribuito l'applicazione.  
  
2.  Creare un set di opzioni. Per ulteriori informazioni, vedere [procedura: configurare opzioni di traccia](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md).  
  
3.  Aggiungere istruzioni di traccia al codice dell'applicazione.  
  
4.  Determinare dove si desidera visualizzare l'output di traccia e aggiungere i listener appropriati. Per ulteriori informazioni, vedere [creazione e inizializzazione di listener di traccia](../../../docs/framework/debug-trace-profile/how-to-create-and-initialize-trace-listeners.md).  
  
5.  Eseguire il test e il debug dell'applicazione e del codice di traccia contenuto.  
  
6.  Compilare l'applicazione nel codice eseguibile usando una delle procedure seguenti:  
  
    -   Utilizzare il **compilare** menu con il **Debug** pagina del **pagine delle proprietà** nella finestra di dialogo **Esplora soluzioni**. Usare questa opzione quando si esegue la compilazione in Visual Studio.  
  
         \- oppure -  
  
    -   Utilizzare il **traccia** e **Debug** direttive del compilatore per il metodo della riga di comando di compilazione. Per ulteriori informazioni, vedere [la compilazione condizionale con traccia e Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md). Usare questa opzione quando si compila dalla riga di comando.  
  
7.  Se si verifica un problema in fase di esecuzione, attivare l'opzione di traccia appropriata. Per ulteriori informazioni, vedere [configurazione delle opzioni di traccia](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md).  
  
     Il codice di traccia scrive i messaggi di traccia in una destinazione specificata, ad esempio sullo schermo, in un file di testo o in un log eventi. Il tipo di listener incluso nella **Trace. Listeners** raccolta determina la destinazione.  
  
8.  Analizzare i messaggi di traccia per identificare e comprendere il problema nell'applicazione.  
  
## <a name="trace-instrumentation-and-distributed-applications"></a>Strumentazione della traccia e applicazioni distribuite  
 Quando si crea un'applicazione distribuita, può risultare difficile testare l'applicazione nel modo in cui verrà usata. Pochi team di sviluppo sono in grado di verificare tutte le possibili combinazioni di sistemi operativi o Web browser (incluse tutte le opzioni di lingua localizzate) o di simulare l'elevato numero di utenti che accederanno all'applicazione contemporaneamente. In questi casi, non è possibile verificare in che modo risponderà un'applicazione distribuita in caso di volumi elevati, installazioni diverse e comportamenti univoci degli utenti finali. Numerose parti di un'applicazione distribuita, inoltre, non dispongono di un'interfaccia utente con cui è possibile interagire direttamente o visualizzare l'attività di tali parti.  
  
 Tuttavia, è possibile rimediare a questa mancanza consentendo alle applicazioni distribuite di descrivere determinati eventi di interesse per gli amministratori di sistema, in particolare problemi, da *strumentazione* l'applicazione, vale a dire inserendo istruzioni di traccia in posizioni strategiche nel codice. Se quindi si verifica un evento imprevisto in fase di esecuzione (ad esempio tempi di risposta eccessivamente lenti), è possibile determinare la causa più probabile.  
  
 Con le istruzioni di traccia, è possibile evitare le complesse attività di analisi del codice sorgente originale, modifica, ricompilazione e tentativo di generare l'errore di run-time all'interno nell'ambiente di debug. Tenere presente che è possibile instrumentare un'applicazione non solo per visualizzare gli errori, ma anche per monitorare le prestazioni.  
  
## <a name="strategic-placement-of-trace-statements"></a>Posizionamento strategico delle istruzioni di traccia  
 È necessario prestare particolare attenzione durante il posizionamento delle istruzioni di traccia da usare in fase di esecuzione. È necessario valutare quali informazioni di traccia saranno necessarie in un'applicazione distribuita, in modo da includere tutti gli scenari di traccia probabili. Poiché le applicazioni che usano la traccia variano notevolmente, tuttavia, non vi sono linee guida generali per il posizionamento strategico della traccia. Per ulteriori informazioni sul posizionamento delle istruzioni di traccia, vedere [procedura: aggiungere istruzioni di traccia al codice dell'applicazione](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md).  
  
## <a name="output-from-tracing"></a>Output della traccia  
 Output di traccia viene raccolto da oggetti denominati *listener*. Un listener è un oggetto che riceve l'output di traccia e lo scrive in un dispositivo di output (in genere una finestra, un log o un file di testo). Quando viene creato un listener di traccia, viene in genere aggiunto per il <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=fullName> insieme, in modo che il listener riceva tutti gli output di traccia.  
  
 Le informazioni di analisi vengono sempre scritte almeno sul valore predefinito <xref:System.Diagnostics.Trace> destinazione di output, il <xref:System.Diagnostics.DefaultTraceListener>. Se per qualche motivo è stato eliminato il <xref:System.Diagnostics.DefaultTraceListener> senza aggiungere altri listener per il <xref:System.Diagnostics.Trace.Listeners%2A> insieme, non si riceverà alcun messaggio di traccia. Per ulteriori informazioni, vedere [listener di traccia](../../../docs/framework/debug-trace-profile/trace-listeners.md).  
  
 I sei <xref:System.Diagnostics.Debug> membri e <xref:System.Diagnostics.Trace> metodi che scrivono informazioni di traccia sono elencati nella tabella seguente.  
  
|Metodo|Output|  
|------------|------------|  
|**L'asserzione**|Il testo specificato oppure, se non è specificato, lo stack di chiamate. L'output viene scritto solo se la condizione specificata come argomento di **Assert** istruzione **false**.|  
|**Esito negativo**|Il testo specificato oppure, se non è specificato, lo stack di chiamate.|  
|**Scrittura**|Il testo specificato.|  
|**WriteIf**|Il testo specificato, se la condizione specificata come argomento di **WriteIf** istruzione viene soddisfatto.|  
|**WriteLine**|Il testo specificato e un ritorno a capo.|  
|**WriteLineIf**|Il testo specificato e un ritorno a capo, se la condizione specificata come argomento di **WriteLineIf** istruzione viene soddisfatto.|  
  
 Tutti i listener nel <xref:System.Diagnostics.Trace.Listeners%2A> raccolta ricevono i messaggi descritti nella tabella precedente, ma le azioni intraprese possono variare a seconda del tipo di listener che riceve il messaggio. Ad esempio, il <xref:System.Diagnostics.DefaultTraceListener> Visualizza una finestra di dialogo di asserzione quando riceve un **esito negativo** o non riuscito **Assert** notifica, ma un <xref:System.Diagnostics.TextWriterTraceListener> scrive semplicemente l'output relativo flusso.  
  
 È possibile produrre risultati personalizzati implementando un listener personalizzato. Un listener di traccia personalizzato potrebbe, ad esempio, visualizzare i messaggi in una finestra di messaggio o connettersi a un database per aggiungere messaggi a una tabella. Tutti i listener personalizzati devono supportare i sei metodi indicati in precedenza. Per ulteriori informazioni sulla creazione di listener definiti dallo sviluppatore, vedere <xref:System.Diagnostics.TraceListener> nei riferimenti a .NET Framework.  
  
> [!NOTE]
>  In [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], **debug. Write**, **debug. WriteIf**, **debug. WriteLine**, e **debug. WriteLineIf** hanno sostituito il **Print** metodo che era disponibile nelle versioni precedenti di Visual Basic.  
  
 Il **scrivere** e **WriteLine** metodi scrivono sempre il testo specificato. **Assert**, **WriteIf**, e **WriteLineIf** richiedono un argomento booleano che controlla se scrivere o meno il testo specificato, viene scritto il testo specificato solo se l'espressione è **true** (per **WriteIf** e **WriteLineIf**), o **false** (per **Assert**). Il **esito negativo** metodo scrive sempre il testo specificato. Per ulteriori informazioni, vedere [procedura: aggiungere istruzioni di traccia al codice dell'applicazione](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md) e il riferimento di .NET Framework.  
  
## <a name="security-concerns"></a>Problemi di sicurezza  
 Se non si disabilitano la traccia e il debug prima di distribuire un'applicazione ASP.NET, l'applicazione può rivelare informazioni su se stessa che potrebbero venire sfruttate da un programma dannoso. Per ulteriori informazioni, vedere [procedura: compilare in modo condizionale con traccia e Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md), [e compilazione](../Topic/Compiling%20and%20Building%20in%20Visual%20Studio.md), e [procedura: creare, inizializzare e configurare opzioni di traccia](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md). Il debug può essere configurato anche tramite Internet Information Services (IIS).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.TraceSource>   
 [Contratti di codice](../../../docs/framework/debug-trace-profile/code-contracts.md)   
 [In c#, F # e tipi di progetto Visual Basic](../Topic/Debugging%20Preparation:%20C%23,%20F%23,%20and%20Visual%20Basic%20Project%20Types.md)   
 [Procedura: aggiungere istruzioni di traccia al codice dell'applicazione](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [Procedura: compilare in modo condizionale con traccia e Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)   
 [Procedura: creare, inizializzare e configurare opzioni di traccia](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md)   
 [Procedura: creare e inizializzare origini di traccia](../../../docs/framework/debug-trace-profile/how-to-create-and-initialize-trace-sources.md)   
 [Procedura: utilizzare TraceSource e filtri con listener di traccia](../../../docs/framework/debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners.md)   
 [Listener di traccia](../../../docs/framework/debug-trace-profile/trace-listeners.md)   
 [Opzioni di traccia](../../../docs/framework/debug-trace-profile/trace-switches.md)