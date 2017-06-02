---
title: "MDbg.exe (.NET Framework Command-Line Debugger) | Microsoft Docs"
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
  - "command-line debugger [.NET Framework]"
  - "MDbg.exe"
ms.assetid: 28a3f509-07e2-4dbe-81df-874c5e969cc4
caps.latest.revision: 27
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 27
---
# MDbg.exe (.NET Framework Command-Line Debugger)
Il debugger della riga di comando di .NET Framework consente ai fornitori di strumenti e agli sviluppatori di applicazioni di individuare e correggere i bug nei programmi destinati a Common Language Runtime di .NET Framework.  Questo strumento usa l'API di debug del runtime per offrire servizi di debug.  È possibile usare MDbg.exe solo per eseguire il debug di codice gestito in quanto non esiste alcun supporto per il debug di codice non gestito.  
  
 Questo strumento è disponibile tramite NuGet.  Per informazioni sull'installazione, vedere [MDbg 0.1.0](http://www.nuget.org/packages/MDbg/0.1.0).  Per eseguire lo strumento, usare la console di Gestione pacchetti.  Per altre informazioni sull'uso della Console di Gestione pacchetti, vedere [Uso della console di Gestione pacchetti](http://docs.nuget.org/docs/start-here/Using-the-Package-Manager-Console).  
  
 Al prompt di Gestione pacchetti, digitare quanto segue:  
  
## Sintassi  
  
```  
MDbg [ProgramName[arguments]] [options]  
```  
  
## Comandi  
 Una volta nel debugger \(come indicato dal prompt **mdbg\>**\), digitare uno dei comandi descritti nella sezione seguente:  
  
 **command** \[*argomenti*\]  
  
 I comandi di MDbg.exe sono soggetti alla distinzione tra maiuscole e minuscole.  
  
|Comando|Descrizione|  
|-------------|-----------------|  
|**ap**\[**rocess**\] \[*number*\]|Passa a un altro processo di cui viene eseguito il debug o visualizza i processi disponibili.  I numeri non corrispondono a ID di processo \(PID\) effettivi ma a un elenco a indice zero.|  
|**a**\[**ttach**\] \[*pid*\]|Esegue la connessione a un processo o visualizza i processi disponibili.|  
|**b**\[**reak**\] \[*ClassName.Method* &#124; *FileName:LineNo*\]|Imposta un punto di interruzione in corrispondenza del metodo specificato.  I moduli vengono sottoposti a scansione in sequenza.<br /><br /> -   **break** *FileName:LineNo* imposta un punto di interruzione in corrispondenza di una posizione nell'origine.<br />-   **break** *~number* imposta un punto di interruzione su un simbolo visualizzato recentemente con il comando **x**.<br />-   **break** *module\!ClassName.Method\+IlOffset* imposta un punto di interruzione in una posizione completa.|  
|**block**\[**ingObjects**\]|Visualizza i blocchi di monitoraggio che stanno bloccando i thread.|  
|**ca**\[**tch**\] \[*exceptionType*\]|Determina l'arresto del debugger in corrispondenza di tutte le eccezioni, non solo di quelle non gestite.|  
|**cl**\[**earException**\]|Contrassegna l'eccezione corrente come gestita in modo che l'esecuzione continui.  Se non si risolve la causa dell'eccezione, questa potrebbe essere nuovamente generata in breve tempo.|  
|**conf**\[**ig**\] \[*option value*\]|Visualizza tutte le opzioni configurabili e mostra come richiamare le opzioni senza valori facoltativi.  Se si specifica l'opzione, imposta `value` come opzione corrente.  Attualmente sono disponibili le seguenti opzioni:<br /><br /> -   `extpath` imposta il percorso di ricerca delle estensioni quando viene usato il comando `load`.<br />-   `extpath+` aggiunge un percorso per il caricamento delle estensioni.|  
|**del**\[**ete**\]|Elimina un punto di interruzione.|  
|**de**\[**tach**\]|Esegue la disconnessione da un processo sottoposto a debug.|  
|**d**\[**own**\] \[*frames*\]|Sposta verso il basso lo stack frame attivo.|  
|**echo**|Restituisce un messaggio alla console.|  
|**enableNotif**\[**ication**\] *typeName* 0&#124;1|Abilita \(1\) o disabilita \(0\) le notifiche personalizzate per il tipo specificato.|  
|**ex**\[**it**\] \[*exitcode*\]|Esce dalla shell di MDbg.exe e specifica, facoltativamente, il codice di uscita del processo.|  
|**fo**\[**reach**\] \[*OtherCommand*\]|Esegue un comando su tutti i thread.  *OtherCommand* è un comando valido che viene eseguito su un singolo thread. **foreach** *OtherCommand* esegue lo stesso comando su tutti i thread.|  
|**f**\[**unceval**\] \[`-ad` *Num*\] *functionName* \[*args ...* \]|Esegue una valutazione della funzione sul thread attivo corrente, dove la funzione da valutare è *functionName*.  Il nome della funzione deve essere completo e includere gli spazi dei nomi.<br /><br /> L'opzione `-ad` specifica il dominio applicazione da usare per risolvere la funzione.  Se l'opzione `-ad` non viene specificata, per impostazione predefinita, il dominio applicazione per la risoluzione corrisponde a quello in cui è reperibile il thread usato per la valutazione della funzione.<br /><br /> Se la funzione da valutare non è statica, il primo parametro passato deve essere un puntatore `this`.  La ricerca degli argomenti per la valutazione della funzione viene eseguita in tutti i domini applicazione.<br /><br /> Per richiedere un valore di un dominio applicazione, anteporre alla variabile il nome del modulo e del dominio applicazione, ad esempio `funceval -ad 0 System.Object.ToString hello.exe#0!MyClass.g_rootRef`.  Questo comando valuta la funzione `System.Object.ToString` nel dominio applicazione `0`.  Dato che il metodo `ToString` è una funzione di istanza, il primo parametro deve essere un puntatore `this`.|  
|**g**\[**o**\]|Determina la continuazione dell'esecuzione del programma fino a quando non viene rilevato un punto di interruzione, il programma non viene chiuso o un evento, ad esempio un'eccezione non gestita, non causa la chiusura del programma.|  
|**h**\[**elp**\] \[*command*\]<br /><br /> \-oppure\-<br /><br /> **?** \[*command*\]|Visualizza una descrizione di tutti i comandi o una descrizione dettagliata di un comando specificato.|  
|**ig**\[**nore**\] \[*event*\]|Determina l'arresto del debugger solo in corrispondenza di eccezioni non gestite.|  
|**int**\[**ercept**\] *FrameNumber*|Esegue il rollback del debugger a un numero di frame specificato.<br /><br /> Se il debugger rileva un'eccezione, usare questo comando per eseguire il rollback del debugger al numero di frame specificato.  Sarà quindi possibile modificare lo stato del programma tramite il comando **set** e usare il comando **go** per continuare.|  
|**k**\[**ill**\]|Arresta il processo attivo.|  
|**l**\[**ist**\] \[*modules* &#124; *appdomains* &#124; *assemblies*\]|Visualizza i moduli, i domini applicazione o gli assembly caricati.|  
|**lo**\[**ad**\] *assemblyName*|Carica un'estensione in questo modo: l'assembly specificato viene caricato e viene quindi effettuato un tentativo di eseguire il metodo statico `LoadExtension` dal tipo `Microsoft.Tools.Mdbg.Extension.Extension`.|  
|**log** \[*eventType*\]|Imposta o visualizza gli eventi da registrare.|  
|**mo**\[**de**\] \[*option on\/off*\]|Imposta opzioni differenti del debugger.  Usare `mode` senza opzioni per ottenere un elenco delle modalità di debug e delle relative impostazioni correnti.|  
|**mon**\[**itorInfo**\] *monitorReference*|Visualizza le informazioni sul blocco di monitoraggio degli oggetti.|  
|**newo**\[**bj**\] *typeName* \[*arguments...*\]|Crea un nuovo oggetto di tipo *typeName*.|  
|**n**\[**ext**\]|Esegue il codice e passa alla riga successiva anche se questa include molte chiamate di funzione.|  
|**Opendump** *pathToDumpFile*|Apre il file dump specificato per il debug.|  
|**o**\[**ut**\]|Esegue lo spostamento alla fine della funzione corrente.|  
|**pa**\[**th**\] \[*pathName*\]|Cerca i file di origine nel percorso specificato se il percorso non è disponibile nei binari.|  
|**p**\[**rint**\] \[*var*\] &#124; \[`-d`\]|Visualizza tutte le variabili dell'ambito \(**print**\), visualizza la variabile specificata \(**print** *var*\) o visualizza le variabili del debugger \(**print** `-d`\).|  
|**printe**\[**xception**\] \[*\-r*\]|Visualizza l'ultima eccezione sul thread corrente.  Usare l'opzione di ricorsione `–r` per attraversare la proprietà `InnerException` sull'oggetto eccezione per ottenere informazioni sull'intera catena delle eccezioni.|  
|**pro**\[**cessenum**\]|Visualizza i processi attivi.|  
|**q**\[**uit**\] \[*exitcode*\]|Esce dalla shell di MDbg.exe specificando, facoltativamente, il codice di uscita del processo.|  
|**re**\[**sume**\] \[`*` &#124; \[`~`\]*threadNumber*\]|Riprende il thread corrente o quello specificato dal parametro *threadNumber*.<br /><br /> Se si specifica `*` come valore del parametro *threadNumber* oppure se il numero di thread inizia con `~`, il comando viene applicato a tutti i thread ad eccezione di quello specificato da *threadNumber*.<br /><br /> La ripresa di un thread non sospeso non produce alcun effetto.|  
|**r**\[**un**\] \[`-d`\(`ebug`\) &#124; \-`o`\(`ptimize`\) &#124;`-enc`\] \[\[*path\_to\_exe*\] \[*args\_to\_exe*\]\]|Arresta l'eventuale processo corrente e ne avvia uno nuovo.  Se non viene passato alcun argomento eseguibile, verrà eseguito l'ultimo programma eseguito con il comando `run`.  Se l'argomento eseguibile viene fornito, per l'esecuzione del programma specificato verranno usati gli argomenti facoltativamente indicati.<br /><br /> Se gli eventi di caricamento classi, caricamento moduli e avvio thread vengono ignorati \(come avviene per impostazione predefinita\), il programma verrà arrestato in corrispondenza della prima istruzione eseguibile del thread principale.<br /><br /> È possibile forzare la compilazione JIT \(just\-in\-time\) del codice usando uno dei tre flag seguenti:<br /><br /> -   `-d`*\(*`ebug`*\)* disabilita le ottimizzazioni.  Questa è l'impostazione predefinita per MDbg.exe.<br />-   `-o`*\(*`ptimize`*\)* forza l'esecuzione del codice in modalità analoga a quanto avviene all'esterno del debugger, ma comporta maggiori difficoltà durante il debug.  Questo è il flag predefinito da usare all'esterno del debugger.<br />-   `-enc` abilita la funzionalità Modifica e continuazione ma comporta una riduzione delle prestazioni.|  
|**Set** *variable*\=*value*|Modifica il valore di qualsiasi variabile inclusa nell'ambito.<br /><br /> È anche possibile creare variabili personalizzate per il debugger e assegnarvi valori di riferimento dall'interno dell'applicazione.  Questi valori fungono da handle del valore originale e anche quest'ultimo non è incluso nell'ambito.  Tutte le variabili del debugger devono iniziare con `$`, ad esempio `$var`.  Per cancellare questi handle, impostarli su un valore vuoto tramite il comando seguente:<br /><br /> `set $var=`|  
|**Setip** \[`-il`\] *number*|Imposta il puntatore all'istruzione \(IP, Instruction Pointer\) corrente nel file sulla posizione specificata.  Se si specifica l'opzione `-il`, il numero rappresenta un offset MSIL \(Microsoft Intermediate Language\) nel metodo.  In caso contrario, il numero rappresenta un numero di riga del codice sorgente.|  
|**sh**\[**ow**\] \[*lines*\]|Specifica il numero di righe da visualizzare.|  
|**s**\[**tep**\]|Sposta l'esecuzione alla funzione successiva della riga corrente oppure passa alla riga successiva se non è disponibile un'altra funzione di cui eseguire le istruzioni.|  
|**su**\[**spend**\] \[\* &#124; \[~\]*threadNumber*\]|Sospende il thread corrente o quello specificato dal parametro *threadNumber*.  Se si specifica il valore `*` per *threadNumber*, il comando viene applicato a tutti i thread.  Se il numero di thread inizia con `~`, il comando viene applicato a tutti i thread ad eccezione di quello specificato da *threadNumber*.  I thread sospesi sono esclusi dall'esecuzione quando il processo viene eseguito tramite il comando **go** o **step**.  L'esecuzione del processo non continuerà se il processo non include thread non sospesi e si emette il comando **go**.  In tal caso, premere CTRL\-C per passare al processo.|  
|**sy**\[**mbol**\] *commandName* \[*commandValue*\]|Specifica uno dei seguenti comandi:<br /><br /> -   `symbol path` \[`"``value``"`\] \- Visualizza o imposta il percorso del simbolo corrente.<br />-   `symbol addpath` `"``value``"` \- Aggiunge il valore al percorso del simbolo corrente.<br />-   `symbol reload` \[`"``module``"`\]\- Ricarica tutti i simboli oppure i simboli relativi al modulo specificato.<br />-   `symbol list` \[`module`\] \- Visualizza i simboli attualmente caricati per tutti i moduli oppure per quello specificato.|  
|**t**\[**hread**\] \[*newThread*\] \[\-*nick nickname*`]`|Il comando thread senza parametri visualizza tutti i thread gestiti nel processo corrente.  I thread sono in genere identificati in base ai relativi numeri. Se tuttavia al thread è assegnato un nome alternativo, verrà visualizzato tale nome.  È possibile usare il parametro `-nick` per assegnare un nome alternativo a un thread.<br /><br /> -   **thread** `-nick` *threadName* assegna un nome alternativo al thread attualmente in esecuzione.<br /><br /> I nomi alternativi non possono essere numeri.  Se al thread corrente è già stato assegnato un nome alternativo, il nome alternativo precedente verrà sostituito da quello nuovo.  Se il nuovo nome alternativo è una stringa vuota \(""\), il nome alternativo del thread corrente verrà eliminato e non ne verrà assegnato un altro.|  
|**u**\[**p**\]|Spostare verso l'alto lo stack frame attivo.|  
|**uwgc**\[**handle**\] \[*var*\] &#124; \[*address*\]|Visualizza la variabile rilevata da un handle.  L'handle può essere specificato in base al nome o all'indirizzo.|  
|**when**|Visualizza le istruzioni `when` attualmente attive.<br /><br /> **when** **delete all** &#124; `num` \[`num` \[`num` …\]\] \- Elimina l'istruzione `when` specificata dal numero o tutte le istruzioni `when` se viene specificato `all`.<br /><br /> **when** `stopReason` \[`specific_condition`\] **do** `cmd` \[`cmd` \[`cmd` …\] \] \- Per il parametro *stopReason* è possibile specificare uno dei valori seguenti:<br /><br /> `StepComplete`, `ProcessExited`, `ThreadCreated`, `BreakpointHit`, `ModuleLoaded`, `ClassLoaded`, `AssemblyLoaded`, `AssemblyUnloaded`, `ControlCTrapped`, `ExceptionThrown`, `UnhandledExceptionThrown`, `AsyncStop`, `AttachComplete`, `UserBreak`, `EvalComplete`, `EvalException`, `RemapOpportunityReached`, `NativeStop`.<br /><br /> *specific\_condition* può essere:<br /><br /> -   *number* \- Per `ThreadCreated` e `BreakpointHit`, l'operazione viene attivata solo quando viene arrestata da un ID thread\/numero di punto di interruzione con lo stesso valore.<br />-   \[`!`\]*name* \- Per `ModuleLoaded`, `ClassLoaded`, `AssemblyLoaded`, `AssemblyUnloaded`, `ExceptionThrown` e `UnhandledExceptionThrown`, attiva l'azione solo quando il nome corrisponde al nome di *stopReason*.<br /><br /> *specific\_condition* deve essere vuoto per altri valori di *stopReason*.|  
|**w**\[**here**\] \[`-v`\] \[`-c` *depth*\] \[*threadID*\]|Visualizza informazioni di debug relative agli stack frame.<br /><br /> -   L'opzione `-v` fornisce informazioni dettagliate su ciascun stack frame visualizzato.<br />-   Specificare un numero per `depth` se si vuole limitare il numero di frame visualizzati.  Usare il comando **all** per visualizzare tutti i frame.  Il valore predefinito è 100.<br />-   Se si specifica il parametro *threadID*, è possibile determinare quale thread è associato allo stack.  Il valore predefinito è il solo thread corrente.  Usare il comando **all** per ottenere tutti i thread.|  
|**x** \[`-c` *numSymbols*\] \[*module*\[`!`*pattern*\]\]|Visualizza le funzioni che corrispondono al parametro `pattern` per un modulo.<br /><br /> Se viene specificato il parametro *numSymbols*, l'output verrà limitato al numero indicato.  Se `!` \(che indica un'espressione regolare\) non è specificato per *pattern*, vengono visualizzate tutte le funzioni.  Se non si specifica un valore per *module*, verranno visualizzati tutti i moduli caricati.  È possibile usare simboli \(*~\#*\) per impostare punti di interruzione con il comando **break**.|  
  
## Note  
 Compilare l'applicazione di cui eseguire il debug usando flag specifici del compilatore che determinano la generazione di simboli di debug da parte del compilatore.  Per altre informazioni su questi flag, vedere la documentazione fornita con il compilatore.  È possibile eseguire il debug delle applicazioni ottimizzate, tuttavia alcune informazioni di debug risulteranno mancanti.  Molte variabili locali, ad esempio, non risulteranno visibili e le righe del codice sorgente non saranno accurate.  
  
 Dopo aver compilato l'applicazione, digitare **mdbg** al prompt dei comandi per avviare una sessione di debug, come illustrato nell'esempio che segue.  
  
```  
C:\Program Files\Microsoft Visual Studio 8\VC>mdbg  
MDbg (Managed debugger) v2.0.50727.42 (RTM.050727-4200) started.  
Copyright (C) Microsoft Corporation. All rights reserved.  
  
For information about commands type "help";  
to exit program type "quit".  
mdbg>  
```  
  
 Il prompt `mdbg>` indica che il debugger è in esecuzione.  
  
 Una volta nel debugger, usare i comandi e gli argomenti descritti nella sezione precedente.  
  
## Esempi  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)