---
title: "Diagnosing Errors with Managed Debugging Assistants | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EHMDA"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "run-time error debugging"
  - "managed code, run-time debugging"
  - "resource debugging"
  - "registry, MDAs"
  - "common language runtime, debugging"
  - "MDAs (managed debugging assistants)"
  - "configuration files [.NET Framework], debugging runtime events"
  - "messages, managed debugging assistants"
  - "application configuration files, managed debugging assistants"
  - "debugging [.NET Framework], managed debugging assistants"
  - "environment variables, MDAs"
  - "access violation debugging [.NET Framework]"
  - "diagnostics, managed debugging assistants"
  - "unmanaged code, run-time debugging"
  - "default debug output stream"
  - "memory, debugging"
  - "app.config files, managed debugging assistants"
  - "managed debugging assistants (MDAs)"
  - "debugging [.NET Framework], run-time errors"
  - "trapping events"
  - "runtime, error debugging"
  - "disabling MDAs"
  - "output, managed debugging assistants"
  - "errors [.NET Framework], managed debugging assistants"
ms.assetid: 76994ee6-9fa9-4059-b813-26578d24427c
caps.latest.revision: 63
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 63
---
# Diagnosing Errors with Managed Debugging Assistants
Gli assistenti al debug gestito sono strumenti per il debug da usare insieme a CLR \(Common Language Runtime\) per fornire informazioni sullo stato del runtime.  Gli assistenti generano messaggi informativi su eventi di runtime che non possono essere intercettati in altro modo.  È possibile usare gli assistenti al debug gestito per isolare bug di applicazione difficili da individuare, che si verificano durante la transizione tra codice gestito e non gestito.  È possibile abilitare o disabilitare tutti gli assistenti al debug gestito aggiungendo una chiave al Registro di sistema di Windows oppure impostando una variabile di ambiente.  Le impostazioni di configurazione dell'applicazione permettono di abilitare assistenti al debug gestito specifici.  È possibile definire impostazioni di configurazione aggiuntive per alcuni singoli assistenti al debug gestito nel file di configurazione dell'applicazione.  Poiché questi file di configurazione sono analizzati durante il caricamento del runtime, è necessario abilitare l'assistente al debug gestito prima dell'avvio dell'applicazione gestita.  Non è possibile abilitarlo per applicazioni già avviate.  
  
> [!NOTE]
>  Quando un assistente al debug gestito è stato avviato, sarà attivo anche quando il codice non è in esecuzione in un debugger.  Se un evento dell'assistente al debug gestito è generato quando non è presente alcun debugger, il messaggio relativo all'evento è visualizzato in una finestra di dialogo per eccezioni non gestite, anche se non si tratta di un'eccezione non gestita.  Per evitare la visualizzazione della finestra di dialogo, rimuovere l'impostazione per l'abilitazione dell'assistente al debug gestito quando il codice non è in esecuzione in un ambiente di debug.  
  
> [!NOTE]
>  Quando il codice è in esecuzione nell'ambiente di sviluppo integrato \(IDE, Integrated Development Environment\) di Visual Studio, è possibile evitare la finestra di dialogo per le eccezioni visualizzata per eventi dell'assistente al debug gestito specifici.  A tale scopo, scegliere **Eccezioni** dal menu **Debug**.  Se il menu **Debug** non include un comando **Eccezioni**, scegliere **Personalizza** dal menu **Strumenti** per aggiungerlo. Nella finestra di dialogo **Eccezioni** espandere l'elenco **Assistenti al debug gestito**, quindi deselezionare la casella di controllo **Generata** per il singolo assistente al debug gestito.  Ad esempio, per evitare la finestra di dialogo per le eccezioni per un [contextSwitchDeadlock](../../../docs/framework/debug-trace-profile/contextswitchdeadlock-mda.md), deselezionare la casella di controllo **Generata** accanto al nome corrispondente nell'elenco **Assistenti al debug gestito**.  È anche possibile usare questa finestra di dialogo per abilitare la visualizzazione delle finestre di dialogo per le eccezioni dell'assistente al debug gestito.  
  
 Nella tabella seguente sono elencati gli assistenti al debug gestito disponibili in .NET Framework.  
  
|||  
|-|-|  
|[asynchronousThreadAbort](../../../docs/framework/debug-trace-profile/asynchronousthreadabort-mda.md)|[bindingFailure](../../../docs/framework/debug-trace-profile/bindingfailure-mda.md)|  
|[callbackOnCollectedDelegate](../../../docs/framework/debug-trace-profile/callbackoncollecteddelegate-mda.md)|[contextSwitchDeadlock](../../../docs/framework/debug-trace-profile/contextswitchdeadlock-mda.md)|  
|[dangerousThreadingAPI](../../../docs/framework/debug-trace-profile/dangerousthreadingapi-mda.md)|[dateTimeInvalidLocalFormat](../../../docs/framework/debug-trace-profile/datetimeinvalidlocalformat-mda.md)|  
|[dirtyCastAndCallOnInterface](../../../docs/framework/debug-trace-profile/dirtycastandcalloninterface-mda.md)|[disconnectedContext](../../../docs/framework/debug-trace-profile/disconnectedcontext-mda.md)|  
|[dllMainReturnsFalse](../../../docs/framework/debug-trace-profile/dllmainreturnsfalse-mda.md)|[exceptionSwallowedOnCallFromCom](../../../docs/framework/debug-trace-profile/exceptionswallowedoncallfromcom-mda.md)|  
|[failedQI](../../../docs/framework/debug-trace-profile/failedqi-mda.md)|[fatalExecutionEngineError](../../../docs/framework/debug-trace-profile/fatalexecutionengineerror-mda.md)|  
|[gcManagedToUnmanaged](../../../docs/framework/debug-trace-profile/gcmanagedtounmanaged-mda.md)|[gcUnmanagedToManaged](../../../docs/framework/debug-trace-profile/gcunmanagedtomanaged-mda.md)|  
|[illegalPrepareConstrainedRegion](../../../docs/framework/debug-trace-profile/illegalprepareconstrainedregion-mda.md)|[invalidApartmentStateChange](../../../docs/framework/debug-trace-profile/invalidapartmentstatechange-mda.md)|  
|[invalidCERCall](../../../docs/framework/debug-trace-profile/invalidcercall-mda.md)|[invalidFunctionPointerInDelegate](../../../docs/framework/debug-trace-profile/invalidfunctionpointerindelegate-mda.md)|  
|[invalidGCHandleCookie](../../../docs/framework/debug-trace-profile/invalidgchandlecookie-mda.md)|[invalidIUnknown](../../../docs/framework/debug-trace-profile/invalidiunknown-mda.md)|  
|[invalidMemberDeclaration](../../../docs/framework/debug-trace-profile/invalidmemberdeclaration-mda.md)|[invalidOverlappedToPinvoke](../../../docs/framework/debug-trace-profile/invalidoverlappedtopinvoke-mda.md)|  
|[invalidVariant](../../../docs/framework/debug-trace-profile/invalidvariant-mda.md)|[jitCompilationStart](../../../docs/framework/debug-trace-profile/jitcompilationstart-mda.md)|  
|[loaderLock](../../../docs/framework/debug-trace-profile/loaderlock-mda.md)|[loadFromContext](../../../docs/framework/debug-trace-profile/loadfromcontext-mda.md)|  
|[marshalCleanupError](../../../docs/framework/debug-trace-profile/marshalcleanuperror-mda.md)|[marshaling](../../../docs/framework/debug-trace-profile/marshaling-mda.md)|  
|[memberInfoCacheCreation](../../../docs/framework/debug-trace-profile/memberinfocachecreation-mda.md)|[moduloObjectHashcode](../../../docs/framework/debug-trace-profile/moduloobjecthashcode-mda.md)|  
|[nonComVisibleBaseClass](../../../docs/framework/debug-trace-profile/noncomvisiblebaseclass-mda.md)|[notMarshalable](../../../docs/framework/debug-trace-profile/notmarshalable-mda.md)|  
|[openGenericCERCall](../../../docs/framework/debug-trace-profile/opengenericcercall-mda.md)|[overlappedFreeError](../../../docs/framework/debug-trace-profile/overlappedfreeerror-mda.md)|  
|[pInvokeLog](../../../docs/framework/debug-trace-profile/pinvokelog-mda.md)|[pInvokeStackImbalance](../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md)|  
|[raceOnRCWCleanup](../../../docs/framework/debug-trace-profile/raceonrcwcleanup-mda.md)|[reentrancy](../../../docs/framework/debug-trace-profile/reentrancy-mda.md)|  
|[releaseHandleFailed](../../../docs/framework/debug-trace-profile/releasehandlefailed-mda.md)|[reportAvOnComRelease](../../../docs/framework/debug-trace-profile/reportavoncomrelease-mda.md)|  
|[streamWriterBufferedDataLost](../../../docs/framework/debug-trace-profile/streamwriterbuffereddatalost-mda.md)|[virtualCERCall](../../../docs/framework/debug-trace-profile/virtualcercall-mda.md)|  
  
 Per impostazione predefinita, .NET Framework attiva un sottoinsieme di assistenti al debug gestito per tutti i debugger gestiti.  È possibile visualizzare il set predefinito in Visual Studio scegliendo **Eccezioni** dal menu **Debug** ed espandendo l'elenco **Assistenti al debug gestito**.  
  
## Abilitazione e disabilitazione di assistenti al debug gestito  
 È possibile abilitare e disabilitare gli assistenti al debug gestito usando una chiave del Registro di sistema, una variabile di ambiente e impostazioni di configurazione dell'applicazione.  Per usare le impostazioni di configurazione dell'applicazione, è necessario abilitare la chiave del Registro di sistema o la variabile di ambiente.  
  
 In Visual Studio 2005 e versioni successive non sarà possibile disabilitare gli assistenti al debug gestito inclusi nel set predefinito o abilitare assistenti al debug gestito non inclusi nel set predefinito se il processo di hosting è abilitato.  Poiché il processo di hosting è abilitato per impostazione predefinita, sarà necessario disabilitarlo in modo esplicito.  
  
 Per disabilitare il processo di hosting in Visual Studio, eseguire le operazioni seguenti:  
  
1.  Selezionare un progetto in **Esplora soluzioni**.  
  
2.  Scegliere **Proprietà** dal menu **Progetto**.  
  
     Sarà visualizzata la finestra **Creazione progetti**.  
  
3.  Fare clic sulla scheda **Debug**.  
  
4.  Nella sezione **Attiva debugger** deselezionare la casella di controllo **Attiva il processo di hosting di Visual Studio**.  
  
 La disabilitazione del processo di hosting, tuttavia, potrebbe influire negativamente sulle prestazioni.  Per evitare di dovere disattivare gli assistenti al debug gestito, impedire a Visual Studio di disattivare la finestra di dialogo relativa all'assistente al debug gestito quando si riceve una notifica.  A tale scopo, scegliere **Eccezioni** dal menu **Debug**, espandere l'elenco **Assistenti al debug gestito** e quindi selezionare o deselezionare la casella di controllo **Generata** per il singolo assistente al debug gestito.  
  
### Abilitazione e disabilitazione di assistenti al debug gestito tramite una chiave del Registro di sistema  
 È possibile abilitare gli assistenti al debug gestito aggiungendo la sottochiave HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\.NETFramework\\MDA \(tipo REG\_SZ, valore 1\) al Registro di sistema di Windows.  Copiare l'esempio seguente in un file di testo con nome MDAEnable.reg.  Aprire l'editor del Registro di sistema di Windows \(RegEdit.exe\) e scegliere **Importa** dal menu **File**.  Selezionare il file MDAEnable.reg per abilitare l'assistente al debug gestito in tale computer.  Se si imposta la sottochiave sul valore di stringa pari a 1 \(non il valore DWORD pari a 1\), sarà abilitata la lettura delle impostazioni dell'assistente al debug gestito dal file *NomeApplicazione.suffisso*.mda.config.  Ad esempio il nome del file di configurazione dell'assistente al debug gestito per Blocco note sarà blocconote.exe.mda.config.  
  
```  
Windows Registry Editor Version 5.00  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework]  
"MDA"="1"  
  
```  
  
 Se il computer esegue un'applicazione a 32 bit in un sistema operativo a 64 bit, la chiave dell'assistente al debug gestito deve essere configurata come segue:  
  
```  
Windows Registry Editor Version 5.00   
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework]  
"MDA"="1"  
  
```  
  
 Per altre informazioni, vedere [Abilitazione e disabilitazione di assistenti al debug gestito tramite impostazioni di configurazione specifiche dell'applicazione](#appConfig).  L'impostazione del Registro di sistema può essere sostituita dalla variabile di ambiente COMPLUS\_MDA.  Per altre informazioni, vedere [Abilitazione e disabilitazione di assistenti al debug gestito tramite una variabile di ambiente](#envVariable).  
  
 Per disabilitare gli assistenti al debug gestito, impostare la sottochiave relativa a MDA su 0 \(zero\) usando l'editor del Registro di sistema di Windows.  
  
 Per impostazione predefinita, alcuni assistenti al debug gestito sono abilitati quando si esegue un'applicazione associata a un debugger, anche se non si aggiunge la chiave del Registro di sistema,  ad esempio gli assistenti [pInvokeStackImbalance](../../../docs/framework/debug-trace-profile/pinvokestackimbalance-mda.md) e [invalidApartmentStateChange](../../../docs/framework/debug-trace-profile/invalidapartmentstatechange-mda.md).  È possibile disabilitare questi assistenti eseguendo il file MDADisable.reg, come descritto in precedenza in questa sezione.  
  
<a name="envVariable"></a>   
### Abilitazione e disabilitazione di assistenti al debug gestito tramite una variabile di ambiente  
 L'attivazione dell'assistente al debug gestito può essere controllata anche dalla variabile di ambiente COMPLUS\_MDA, che sostituisce la chiave del Registro di sistema.  La stringa COMPLUS\_MDA è un elenco di nomi di assistenti al debug gestito o di altre stringhe di controllo speciali delimitato da punto e virgola e in cui non è applicata la distinzione tra maiuscole\/minuscole.  L'avvio con un debugger gestito o non gestito abilita un set di assistenti al debug gestito per impostazione predefinita,  aggiungendo in modo implicito l'elenco delimitato da punto e virgola di assistenti al debug gestito abilitati per impostazione predefinita con i debugger davanti al valore della variabile di ambiente o della chiave del Registro di sistema.  Di seguito sono elencate le stringhe di controllo speciali:  
  
-   `0` \- Disattiva tutti gli assistenti al debug gestito.  
  
-   `1` \- Legge le impostazioni dell'assistente al debug gestito da *NomeApplicazione*.mda.config.  
  
-   `managedDebugger` \- Attiva esplicitamente tutti gli assistenti al debug gestito attivati in modo implicito quando si avvia un eseguibile gestito con un debugger.  
  
-   `unmanagedDebugger` \- Attiva esplicitamente tutti gli assistenti al debug gestito attivati in modo implicito quando si avvia un eseguibile non gestito con un debugger.  
  
 In caso di conflitto, le impostazioni più recenti eseguono l'override di quelle precedenti:  
  
-   `COMPLUS_MDA=0` disabilita tutti gli assistenti al debug gestito, inclusi quelli abilitati in modo implicito con un debugger.  
  
-   `COMPLUS_MDA=gcUnmanagedToManaged` abilita `gcUnmanagedToManaged`, oltre a eventuali assistenti al debug gestito abilitati in modo implicito con un debugger.  
  
-   `COMPLUS_MDA=0;gcUnmanagedToManaged` abilita `gcUnmanagedToManaged` ma disabilita gli assistenti al debug gestito che sarebbero altrimenti abilitati in modo implicito con un debugger.  
  
<a name="appConfig"></a>   
### Abilitazione e disabilitazione di assistenti al debug gestito tramite impostazioni di configurazione specifiche dell'applicazione  
 È possibile abilitare, disabilitare e configurare individualmente alcuni assistenti nel file di configurazione MDA per l'applicazione.  Per abilitare l'uso di un file di configurazione dell'applicazione al fine di configurare gli assistenti al debug gestito, è necessario impostare la chiave del Registro di sistema relativa a MDA o la variabile di ambiente COMPLUS\_MDA.  Il file di configurazione dell'applicazione si trova in genere nella stessa directory del file eseguibile \(con estensione exe\) dell'applicazione.  Il formato del nome del file è *NomeApplicazione*.mda.config. Ad esempio, blocconote.exe.mda.config.  Gli assistenti abilitati nel file di configurazione dell'applicazione potrebbero disporre di attributi o elementi progettati in modo specifico per il controllo del comportamento dell'assistente.  L'esempio seguente mostra come abilitare e configurare [marshaling](../../../docs/framework/debug-trace-profile/marshaling-mda.md).  
  
```  
<mdaConfig>  
  <assistants>  
    <marshaling>  
      <methodFilter>  
        <match name="*"/>  
      </methodFilter>  
      <fieldFilter>  
        <match name="*"/>  
      </fieldFilter>  
    </marshaling>  
  </assistants>  
</mdaConfig>  
```  
  
 L'assistente `Marshaling` emette informazioni sul tipo gestito di cui si sta eseguendo il marshalling a un tipo non gestito per ogni transizione da gestito a non gestito nell'applicazione.  L'assistente al debug gestito per il `Marshaling` può anche filtrare i nomi dei campi metodo e struttura forniti rispettivamente negli elementi figlio `<methodFilter>` e `<fieldFilter>`.  
  
 L'esempio seguente mostra come abilitare più assistenti al debug gestito usando le rispettive impostazioni predefinite.  
  
```  
<mdaConfig>  
  <assistants>  
    <illegalPrepareConstrainedRegion />  
    <invalidCERCall />  
    <openGenericCERCall />  
    <virtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
> [!IMPORTANT]
>  Se si specifica più di un assistente in un file di configurazione, è necessario elencarli in ordine alfabetico.  Ad esempio, per abilitare gli assistenti `virtualCERCall` e `invalidCERCall`, è necessario aggiungere la voce `<invalidCERCall />` prima della voce `<virtualCERCall />`.  Se le voci non sono in ordine alfabetico, sarà visualizzato un messaggio relativo a un'eccezione non gestita per file di configurazione non valido.  
  
### Output degli assistenti al debug gestito  
 L'output degli assistenti al debug gestito è analogo all'esempio seguente, che mostra l'output dall'assistente `pInvokeStackImbalance`.  
  
 `A call to PInvoke function 'MDATest!MDATest.Program::StdCall' has unbalanced the stack.  This is likely because the managed PInvoke signature does not match the unmanaged target signature.  Check that the calling convention and parameters of the PInvoke signature match the target unmanaged signature.`  
  
## Vedere anche  
 [Debugging, Tracing, and Profiling](../../../docs/framework/debug-trace-profile/index.md)