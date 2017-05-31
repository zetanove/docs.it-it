---
title: Hosting di .NET Core | Microsoft Docs
description: Hosting del runtime di .NET Core da codice nativo
keywords: .NET, .NET Core, Hosting, Hosting di .NET Core
author: mjrousos
ms.author: mikerou
ms.date: 2/3/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 13edec8b-614d-47ed-9e95-ed6d3b94ec0c
ms.translationtype: Human Translation
ms.sourcegitcommit: d866cf8eab2b8db936d813ccae7882f8d7db5720
ms.openlocfilehash: cf420d4379afbdb3c6db048c7817a4c143c124d9
ms.contentlocale: it-it
ms.lasthandoff: 04/26/2017

---

# <a name="hosting-net-core"></a>Hosting di .NET Core

Come tutto il codice gestito, le applicazioni .NET Core sono eseguite da un host. L'host è responsabile dell'avvio del runtime, inclusi i componenti come JIT e Garbage Collector, della creazione di AppDomain e della chiamata dei punti di ingresso gestiti.

L'hosting del runtime di .NET Core rappresenta uno scenario avanzato e, nella maggior parte dei casi, gli sviluppatori .NET Core non devono occuparsi dell'hosting poiché i processi di compilazione di .NET Core includono un host predefinito per l'esecuzione delle applicazioni .NET Core. Tuttavia, in alcune circostanze particolari può essere utile ospitare in modo esplicito il runtime di .NET Core per richiamare il codice gestito in un processo nativo o per avere maggior controllo sul funzionamento del runtime.

Questo articolo offre una panoramica dei passaggi necessari per avviare il runtime di .NET Core da codice nativo, creare un dominio di applicazione iniziale (<xref:System.AppDomain>) ed eseguire il codice gestito in tale dominio.

## <a name="prerequisites"></a>Prerequisiti

Poiché gli host sono applicazioni native, in questa esercitazione verrà descritta la costruzione di un'applicazione C++ per l'hosting di .NET Core. Sarà necessario un ambiente di sviluppo C++, come quello incluso in [Visual Studio](https://www.visualstudio.com/downloads/).

Poiché sarà necessaria anche un'applicazione .NET Core semplice con cui testare l'host, installare [.NET Core SDK](https://www.microsoft.com/net/core) e [creare una piccola app di test .NET Core](../../csharp/getting-started/with-visual-studio.md), ad esempio un'app 'Hello World'. L'app 'Hello World' creata dal nuovo modello di progetto della console di .NET Core è sufficiente.

Questa esercitazione e l'esempio associato creano un host Windows. Per informazioni sull'hosting in Unix, vedere le note alla fine dell'articolo.

## <a name="creating-the-host"></a>Creazione dell'host

Nel repository GitHub dotnet/docs è disponibile un [host di esempio](https://github.com/dotnet/docs/tree/master/samples/core/hosting) che illustra i passaggi descritti in questo articolo. I commenti nel file *host.cpp* dell'esempio associano chiaramente i passaggi numerati di questa esercitazione alla posizione in cui vengono eseguiti nell'esempio. Per istruzioni sul download, vedere [Esempi ed esercitazioni](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

Tenere presente che poiché l'host di esempio è destinato a essere usato ai fini dell'apprendimento, il controllo degli errori non è prioritario e l'host è stato progettato per evidenziare la leggibilità e non l'efficienza. Nel repository [dotnet/coreclr](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts) sono disponibili esempi di host più reali. In particolare, l'[host CoreRun](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts/corerun) è un host di utilizzo generale da esaminare dopo aver letto l'esempio più semplice.

### <a name="a-note-about-mscoreeh"></a>Nota su mscoree.h
L'interfaccia di hosting principale di .NET Core (`ICLRRuntimeHost2`) è definita in [MSCOREE.IDL](https://github.com/dotnet/coreclr/blob/master/src/inc/MSCOREE.IDL). Una versione dell'intestazione di questo file (mscoree.h) a cui l'host dovrà fare riferimento viene prodotta tramite MIDL quando viene compilato il [runtime di .NET Core](https://github.com/dotnet/coreclr/). Se non si vuole compilare il runtime di .NET Core, mscoree.h è disponibile anche come [intestazione precompilata](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc) nel repository dotnet/coreclr. Le [istruzioni sulla compilazione del runtime di .NET Core](https://github.com/dotnet/coreclr#building-the-repository) sono disponibili nel relativo repository GitHub. 

### <a name="step-1---identify-the-managed-entry-point"></a>Passaggio 1: Identificare il punto di ingresso gestito
Dopo il riferimento alle intestazioni necessarie, ad esempio [mscoree.h](https://github.com/dotnet/coreclr/tree/master/src/pal/prebuilt/inc/mscoree.h) e stdio.h, una delle prime operazioni che devono essere eseguite da un host .NET Core consiste nell'individuare il punto di ingresso gestito da usare. Nell'host di esempio questa operazione viene eseguita usando il primo argomento della riga di comando dell'host come percorso di un binario gestito di cui eseguire il metodo `main`.

[!code-cpp[NetCoreHost#1](../../../samples/core/hosting/host.cpp#1)]

### <a name="step-2---find-and-load-coreclrdll"></a>Passaggio 2: Trovare e caricare CoreCLR.dll
Le API del runtime di .NET Core sono in *CoreCLR.dll* in Windows. Per ottenere l'interfaccia di hosting (`ICLRRuntimeHost2`), è necessario trovare e caricare *CoreCLR.dll*. L'host definisce una convenzione per l'individuazione di *CoreCLR.dll*. Alcuni host prevedono che il file si trovi in un percorso del computer noto, ad esempio %programfiles%\dotnet\shared\Microsoft.NETCore.App\1.1.0. Altri prevedono che *CoreCLR.dll* venga caricato da un percorso successivo all'host o all'app da ospitare. Altri ancora usano una variabile di ambiente per trovare la libreria.

In Linux o Mac la libreria di runtime principale è rispettivamente *libcoreclr.so* o *libcoreclr.dylib*.

L'host di esempio esegue il probe in alcuni percorsi comuni di *CoreCLR.dll*. Dopo essere stata individuata, la libreria deve essere caricata tramite `LoadLibrary` (o `dlopen` in Linux/Mac).

[!code-cpp[NetCoreHost#2](../../../samples/core/hosting/host.cpp#2)]

### <a name="step-3---get-an-iclrruntimehost2-instance"></a>Passaggio 3: Ottenere un'istanza ICLRRuntimeHost2
L'interfaccia di hosting `ICLRRuntimeHost2` viene recuperata chiamando `GetProcAddress` (o `dlsym` in Linux/Mac) in `GetCLRRuntimeHost` e quindi richiamando la funzione. 

[!code-cpp[NetCoreHost#3](../../../samples/core/hosting/host.cpp#3)]

### <a name="step-4---setting-startup-flags-and-starting-the-runtime"></a>Passaggio 4: Impostazione dei flag di avvio e avvio del runtime
Con un `ICLRRuntimeHost2` disponibile, è ora possibile specificare flag di avvio del runtime e avviare il runtime. I flag di avvio determineranno il Garbage Collector (GC) da usare (simultaneo o server), l'uso di AppDomain singoli o multipli e i criteri di ottimizzazione del caricatore da usare per il caricamento di assembly indipendente dal dominio.

[!code-cpp[NetCoreHost#4](../../../samples/core/hosting/host.cpp#4)]

Il runtime viene avviato con una chiamata alla funzione `Start`.

```C++
hr = runtimeHost->Start();
```

### <a name="step-5---preparing-appdomain-settings"></a>Passaggio 5: Preparazione delle impostazioni dell'AppDomain
Dopo aver avviato il runtime, sarà necessario impostare un AppDomain. Poiché quando si crea un AppDomain .NET sono presenti numerose opzioni da specificare, è necessario preparare tali impostazioni.

I flag AppDomain specificano i comportamenti di AppDomain correlati alla sicurezza e all'interoperabilità. Gli host Silverlight precedenti usavano queste impostazioni per creare il codice utente mediante sandbox, mentre gli host .NET Core più recenti eseguono il codice utente come totalmente attendibile e abilitano l'interoperabilità.

[!code-cpp[NetCoreHost#5](../../../samples/core/hosting/host.cpp#5)]

Dopo aver deciso quali flag AppDomain usare, è necessario definire le proprietà dell'AppDomain. Le proprietà sono coppie chiave/valore delle stringhe. Molte delle proprietà riguardano la modalità con la quale l'AppDomain caricherà gli assembly.

Le proprietà di AppDomain comuni includono:

* `TRUSTED_PLATFORM_ASSEMBLIES` Elenco di percorsi di assembly (delimitati da ';' in Windows e ':' in Unix) che l'AppDomain deve classificare in ordine di priorità di caricamento e ai quali deve assegnare attendibilità totale, anche nei domini parzialmente attendibili. Questo elenco deve contenere assembly 'Framework' e altri moduli attendibili, analogamente a GAC negli scenari .NET Framework. Alcuni host inseriranno le librerie accanto a *coreclr.dll* nell'elenco, mentre altri avranno manifesti hardcoded che elencano gli assembly attendibili per i propri scopi.
* `APP_PATHS` Elenco di percorsi in cui eseguire il probe se un assembly non viene trovato nell'elenco degli assembly di piattaforma attendibili (TPA). Questi percorsi devono essere i percorsi in cui è possibile trovare gli assembly degli utenti. In un AppDomain creato mediante sandbox agli assembly caricati da questi percorsi verrà assegnata soltanto un'attendibilità parziale. I percorsi APP_PATH comuni includono il percorso da cui è stata caricata l'app di destinazione o altri percorsi in cui è noto si trovino gli asset utente.
*  `APP_NI_PATHS` Elenco molto simile ad APP_PATHS ma che deve includere i percorsi in cui verrà eseguito il probe delle immagini native.
*  `NATIVE_DLL_SEARCH_DIRECTORIES` Questa proprietà è un elenco di percorsi in cui il caricatore esegue il probe quando cerca DLL native chiamate tramite p/invoke.
*  `PLATFORM_RESOURCE_ROOTS` Questo elenco include i percorsi in cui eseguire il probe di assembly satelliti di risorse in sottodirectory specifiche delle impostazioni cultura.
*  `AppDomainCompatSwitch` Questa stringa specifica i quirk di compatibilità da usare per gli assembly senza Moniker della versione di .NET Framework di destinazione (attributo a livello di assembly che indica il Framework in cui deve essere eseguito un assembly) esplicito. Solitamente la stringa dovrebbe essere impostata su `"UseLatestBehaviorWhenTFMNotSpecified"`, ma alcuni hosts potrebbero preferire quirk di compatibilità Silverlight o Windows Phone precedenti.

In questo [host di esempio semplice](https://github.com/dotnet/docs/tree/master/samples/core/hosting) queste proprietà sono impostate come segue:

[!code-cpp[NetCoreHost#6](../../../samples/core/hosting/host.cpp#6)]

### <a name="step-6---create-the-appdomain"></a>Passaggio 6: Creare l'AppDomain
Dopo aver preparato tutti i flag e le proprietà AppDomain, è possibile usare `ICLRRuntimeHost2::CreateAppDomainWithManager` per impostare l'AppDomain. Questa funzione accetta facoltativamente un nome di assembly completo e un nome di tipo da usare come gestore AppDomain del dominio. Un gestore AppDomain può consentire a un host di controllare alcuni aspetti del comportamento dell'AppDomain e può offrire i punti di ingresso per l'avvio di codice gestito se l'host non intende richiamare il codice utente direttamente.   

[!code-cpp[NetCoreHost#7](../../../samples/core/hosting/host.cpp#7)]

### <a name="step-7---run-managed-code"></a>Passaggio 7: Eseguire il codice gestito
Con un AppDomain attivo e in esecuzione, l'host può ora avviare l'esecuzione del codice gestito. Il modo più semplice per eseguire questa operazione consiste nell'usare `ICLRRuntimeHost2::ExecuteAssembly` per richiamare un metodo del punto di ingresso dell'assembly gestito. Si noti che questa funzione funziona solo in scenari con dominio singolo.

[!code-cpp[NetCoreHost#8](../../../samples/core/hosting/host.cpp#8)]

Se `ExecuteAssembly` non soddisfa le esigenze dell'host, un'altra opzione consiste nell'usare `CreateDelegate` per creare un puntatore funzione a un metodo gestito statico. Questa operazione richiede che l'host conosca la firma del metodo chiamato per poter creare il tipo di puntatore funzione ma offre agli host la flessibilità di richiamare codice diverso da un punto di ingresso dell'assembly.

```C++
void *pfnDelegate = NULL;
hr = runtimeHost->CreateDelegate(
  domainId,
  L"HW, Version=1.0.0.0, Culture=neutral",    // Target managed assembly
  L"ConsoleApplication.Program",            // Target managed type
  L"Main",                                    // Target entry point (static method)
  (INT_PTR*)&pfnDelegate);

((MainMethodFp*)pfnDelegate)(NULL);
```

### <a name="step-8---clean-up"></a>Passaggio 8: Pulire
È necessario infine che l'host esegua una pulizia scaricando gli AppDomain, interrompendo il runtime e rilasciando il riferimento `ICLRRuntimeHost2`.

[!code-cpp[NetCoreHost#9](../../../samples/core/hosting/host.cpp#9)]

## <a name="about-hosting-net-core-on-unix"></a>Informazioni sull'hosting di .NET Core in Unix
.NET Core è un prodotto multipiattaforma che viene eseguito nei sistemi operativi Windows, Linux e Mac. Tuttavia, analogamente alle applicazioni native, gli host delle diverse piattaforme presentano alcune differenze. Il processo descritto sopra relativo all'uso di `ICLRRuntimeHost2` per l'avvio del runtime, la creazione di un AppDomain e l'esecuzione di codice gestito dovrebbe funzionare in tutti i sistemi operativi supportati. Tuttavia,le interfacce definite in mscoree.h possono risultare difficili da usare in piattaforme Unix poiché mscoree effettua numerose assunzioni Win32.

Per rendere più semplice l'hosting nelle piattaforme Unix, in [coreclrhost.h](https://github.com/dotnet/coreclr/blob/master/src/coreclr/hosts/inc/coreclrhost.h) è disponibile un set di wrapper di API di hosting più indipendenti dalla piattaforma.

Per un esempio di uso di coreclrhost.h (anziché di mscoree.h direttamente), vedere l'[host UnixCoreRun](https://github.com/dotnet/coreclr/tree/master/src/coreclr/hosts). I passaggi per l'uso delle API di coreclrhost.h per ospitare il runtime sono simili ai passaggi per l'uso di mscoree.h:

1. Identificare il codice gestito da eseguire, ad esempio dai parametri della riga di comando. 
2. Caricare la libreria CoreCLR.
    1. `dlopen("./libcoreclr.so", RTLD_NOW | RTLD_LOCAL);` 
3. Ottenere i puntatori funzione alle funzioni `coreclr_initialize`, `coreclr_create_delegate`, `coreclr_execute_assembly` e `coreclr_shutdown` di CoreCLR usando `dlsym`
    1. `coreclr_initialize_ptr coreclr_initialize = (coreclr_initialize_ptr)dlsym(coreclrLib, "coreclr_initialize");`
4. Impostare le proprietà AppDomain, ad esempio l'elenco TPA. L'operazione è analoga a quella del passaggio 5 del flusso di lavoro di mscoree descritto in precedenza.
5. Usare `coreclr_initialize` per avviare il runtime e creare un AppDomain. Verrà anche creato un puntatore `hostHandle` che verrà usato nelle chiamate di hosting future.
    1. Si noti che questa funzione esegue i ruoli di entrambi i passaggi 4 e 6 del flusso di lavoro precedente. 
6. Usare `coreclr_execute_assembly` o `coreclr_create_delegate` per eseguire il codice gestito. Queste funzioni sono analoghe alle funzioni `ExecuteAssembly` e `CreateDelegate` di mscoree del passaggio 7 del flusso di lavoro precedente.
7. Usare `coreclr_shutdown` per scaricare l'AppDomain e arrestare il runtime. 

## <a name="conclusion"></a>Conclusione
Dopo aver compilato l'host, è possibile testarlo eseguendolo dalla riga di comando e passando tutti gli argomenti previsti dall'host, ad esempio l'app gestita da eseguire. Quando si specifica l'app .NET Core che deve essere eseguita dall'host, assicurarsi di usare il file DLL prodotto da `dotnet build`. Gli eseguibili prodotti da `dotnet publish` per le applicazioni indipendenti costituiscono l'host .NET Core predefinito (in modo che l'app possa essere avviata direttamente dalla riga di comando negli scenari principali). Il codice utente viene compilato in un file DLL con lo stesso nome. 

Se si verifica un malfunzionamento inizialo, verificare che *coreclr.dll* sia disponibile nel percorso previsto dall'host, che tutte le librerie Framework necessarie siano incluse nell'elenco TPA e che il numero di bit (32 o 64) di CoreCLR corrisponda alla modalità di compilazione dell'host.

Sebbene rappresenti uno scenario avanzato che molti sviluppatori non richiedono, l'hosting del runtime di .NET Core può essere molto utile per gli sviluppatori che devono avviare codice gestito da un processo nativo o che necessitano di maggior controllo sul comportamento del runtime di .NET Core. Poiché .NET Core può essere eseguito side-by-side, è possibile creare host che inizializzano e avviano più versioni del runtime di .NET Core ed eseguono le app in tutte le versioni nello stesso processo. 

