---
title: .NET Core
description: .NET Core
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: f2b312cb-f80c-4b0d-9101-93908f06a6fa
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 26210b19de4f7bf70c085735771b0175945f38d4
ms.lasthandoff: 03/02/2017

---

# <a name="net-core"></a>.NET Core

> Per imparare a creare una semplice applicazione .NET Core, consultare le [esercitazioni introduttive](getting-started.md). Sono necessari pochi minuti per realizzare ed eseguire la prima app.

.NET Core è una piattaforma di sviluppo generale gestita da Microsoft e dalla community .NET su [GitHub](https://github.com/dotnet/core). È multipiattaforma, supporta Windows, macOS e Linux e può essere usata su dispositivi, ambienti cloud e scenari IoT/incorporati. 

Di seguito sono elencate le principali caratteristiche di .NET Core:

- **Distribuzione flessibile:** può essere incluso nell'app o installato side-by-side a livello di computer o di utente.
- **Multipiattaforma:** viene eseguito in Windows, macOS e Linux e può essere trasferito in altri sistemi operativi. Le CPU, gli scenari applicativi e i [sistemi operativi supportati](https://github.com/dotnet/core/blob/master/roadmap.md) aumenteranno nel tempo e saranno rilasciati da Microsoft, altre società e singoli utenti.
- **Strumenti da riga di comando:** tutti gli scenari di prodotto possono essere usati dalla riga di comando. 
- **Compatibile:** .NET Core è compatibile con .NET Framework, Xamarin e Mono, tramite la [libreria .NET Standard](../standard/library.md).
- **Open source:** la piattaforma .NET Core è open source e usa le licenze MIT e Apache 2. La documentazione è concessa in licenza da [CC-BY](http://creativecommons.org/licenses/by/4.0/). .NET Core è un progetto [.NET Foundation](http://www.dotnetfoundation.org/).
- **Supportato da Microsoft:** .NET Core è supportato da Microsoft, in base al [supporto di .NET Core](https://www.microsoft.com/net/core/support/).

## <a name="composition"></a>Composizione

.NET Core è costituito dalle parti seguenti:

- Un [runtime .NET](https://github.com/dotnet/coreclr), che fornisce un sistema di tipi, il caricamento dell'assembly, un garbage collector, l'interoperabilità nativa e altri servizi di base. 
- Un set di [librerie framework](https://github.com/dotnet/corefx), che fornisce tipi di dati primitivi, tipi di composizione app e utilità fondamentali. 
- Un [set di strumenti SDK](https://github.com/dotnet/cli) e [compilatori di linguaggio](https://github.com/dotnet/roslyn) per un'esperienza di sviluppo di base, disponibile in [.NET Core SDK](sdk.md).
- L'host di app 'dotnet', che viene usato per avviare le app .NET Core. Tale host seleziona e ospita il runtime, fornisce criteri di caricamento di assembly e avvia l'app. Lo stesso host viene anche usato per avviare gli strumenti SDK in modo analogo.

### <a name="languages"></a>Linguaggi

È possibile usare i linguaggi C# ed F# (prossimamente anche Visual Basic) per scrivere librerie e applicazioni per .NET Core. I compilatori vengono eseguiti su .NET Core, che consente di sviluppare per .NET Core in qualsiasi ambiente di esecuzione. In generale, i compilatori non verranno usati direttamente, ma tramite gli strumenti SDK.

I compilatori C# ed F# e gli strumenti .NET Core sono o possono essere integrati in diversi editor di testo e ambienti di sviluppo integrati, tra cui Visual Studio, [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp), Sublime Text e Vim, in modo da rendere lo sviluppo .NET Core un'opzione utile nel sistema operativo e nell'ambiente di sviluppo preferito. Questa integrazione è resa in parte possibile dal [progetto OmniSharp](http://www.omnisharp.net/).

### <a name="net-apis-and-compatibility"></a>API .NET e compatibilità

.NET Core può essere considerato come una versione multipiattaforma di .NET Framework, a livello delle librerie di classi base di.NET Framework . Implementa le specifiche della [libreria .NET Standard](../standard/library.md). .NET Core fornisce un sottoinsieme delle API disponibili in .NET Framework o Mono/Xamarin. In alcuni casi, i tipi non sono completamente implementati (alcuni membri non sono disponibili o sono stati spostati).

Per altre informazioni sulla guida di orientamento alle API di .NET Core, consultare la [.NET Core Roadmap](https://github.com/dotnet/core/blob/master/roadmap.md) (Guida di orientamento di .NET Core).

### <a name="relationship-to-the-net-standard-library"></a>Relazione con la libreria .NET Standard

La [libreria .NET Standard](../standard/library.md) è una specifica API che descrive il set coerente di API .NET che gli sviluppatori possono aspettarsi in ogni implementazione di .NET. Le implementazioni di .NET devono implementare questa specifica per essere conformi alla libreria .NET Standard e per il supporto di librerie che hanno come destinazione la libreria .NET Standard. 

.NET Core implementa la libreria .NET Standard e pertanto supporta le librerie .NET Standard.

### <a name="workloads"></a>Carichi di lavoro

Di per sé .NET Core include un singolo modello di applicazione - app console - che risulta utile per gli strumenti, i servizi locali e i giochi basati su testo. Modelli di applicazioni aggiuntivi sono stati integrati in .NET Core per estenderne le funzionalità, ad esempio:

- [ASP.NET Core](http://asp.net)
- [Piattaforma UWP (Universal Windows Platform) di Windows 10](https://developer.microsoft.com/windows)
- [Xamarin.Forms](https://www.xamarin.com/forms)

### <a name="open-source"></a>Open source

[.NET Core](https://github.com/dotnet/core) è open source (licenza MIT) ed è stato fornito a [.NET Foundation](http://dotnetfoundation.org) da Microsoft nel 2014. Attualmente è uno dei progetti .NET Foundation più attivi. Può essere adottato liberamente da singoli utenti e società, anche a scopo commerciale, accademico o personale. Numerose società usano .NET Core come parte di app, strumenti, nuove piattaforme e servizi di hosting. Alcune di queste società apportano contributi significativi a .NET Core su GitHub e forniscono indicazioni sull'uso del prodotto come parte del gruppo [.NET Foundation Technical Steering Group](http://www.dotnetfoundation.org/blog/tsg-welcome).

## <a name="acquisition"></a>Acquisizione

.NET Core viene distribuito in due modi, come pacchetti in NuGet.org e come distribuzioni autonome.

### <a name="distributions"></a>Distribuzioni

È possibile scaricare .NET Core nella pagina [.NET Core Getting Started](https://www.microsoft.com/net/core) (Introduzione a .NET Core).

- La distribuzione *Microsoft .NET Core* include il runtime di CoreCLR, librerie associate, un host di applicazioni console e l'utilità di avvio app `dotnet`. Viene descritta nel metapacchetto [`Microsoft.NETCore.App`](https://www.nuget.org/packages/Microsoft.NETCore.App).
- La distribuzione *Microsoft .NET Core SDK* include .NET Core e un set di strumenti per il ripristino di pacchetti NuGet e la compilazione e creazione di app. 

Per iniziare con lo sviluppo di .NET Core, viene innanzitutto installato .NET Core SDK. È possibile scegliere di installare altre compilazioni (probabilmente in versione provvisoria) di .NET Core.

### <a name="packages"></a>Pacchetti

- I [pacchetti di .NET Core](packages.md) contengono il runtime di .NET Core e le librerie (assembly di riferimento e implementazioni). Ad esempio, [System.Net.Http](https://www.nuget.org/packages/System.Net.Http/).
- I [metapacchetti di .NET Core](packages.md) descrivono i diversi livelli e modelli di app facendo riferimento al set appropriato di pacchetti di librerie con versione.

## <a name="architecture"></a>Architettura

.NET Core è un'implementazione .NET multipiattaforma. La principale preoccupazione architetturale univoca di .NET Core è correlata a fornire implementazioni specifiche della piattaforma per le piattaforme supportate.

### <a name="environments"></a>Ambienti

.NET Core è supportato da Microsoft in Windows, macOS e Linux. In Linux, Microsoft supporta principalmente .NET Core in esecuzione nelle famiglie di distribuzione Red Hat Enterprise Linux (RHEL) e Debian.

.NET Core attualmente supporta CPU X64. In Windows, è supportata anche X86 e ARM64 e ARM32 lo saranno a breve.

L'articolo [.NET Core Roadmap](https://github.com/dotnet/core/blob/master/roadmap.md) (Guida di orientamento di .NET Core) fornisce informazioni più dettagliate su carico di lavoro, piani e supporto dell'ambiente del sistema operativo e della CPU.

Altre società o i gruppi possono supportare .NET Core per altri tipi di app e ambienti.

### <a name="designed-for-adaptability"></a>Progettato per l'adattabilità

.NET Core è stato progettato come prodotto molto simile, ma allo stesso tempo unico rispetto ad altri prodotti .NET. È stato progettato per consentire una maggiore adattabilità alle nuove piattaforme, per nuovi carichi di lavoro e con nuove toolchain del compilatore. Dispone di numerose porte del sistema operativo e della CPU attive e può essere trasferito a molte altre. Un esempio è il progetto [LLILC](https://github.com/dotnet/llilc), ovvero un prototipo iniziale della compilazione nativa di .NET Core tramite il compilatore [LLVM](http://llvm.org/).

Il prodotto è suddiviso in più parti, in modo che ognuna possa adattarsi alla nuova piattaforma in diverse pianificazioni. Il runtime e le librerie di base specifiche della piattaforma devono essere trasferite come elementi univoci. Le librerie indipendenti dalla piattaforma dovrebbero funzionare in modo indipendente su tutte le piattaforme, per costruzione. Esiste una propensione del progetto alla riduzione delle implementazioni specifiche della piattaforma al fine di aumentare l'efficienza dello sviluppatore, preferendo il codice C# indipendente dalla piattaforma ogni volta che un algoritmo o un'API può essere implementata completamente o in parte in questo modo.

In genere, viene richiesto come implementare .NET Core al fine di supportare più sistemi operativi e se sono disponibili implementazioni separate o viene usata [la compilazione condizionale](https://en.wikipedia.org/wiki/Conditional_compilation). Sono disponibili entrambe le opzioni, con una forte preferenza per la compilazione condizionale.

Nel grafico seguente si può notare che la maggior parte del codice [CoreFX](https://github.com/dotnet/corefx) è indipendente dalla piattaforma ed è condiviso tra tutte le piattaforme. Il codice indipendente dalla piattaforma può essere implementato come assembly portabile individuale da usare su tutte le piattaforme.

![CoreFX: righe di codice per ogni piattaforma](../images/corefx-platforms-loc.png)

Le implementazioni Windows e Unix hanno dimensioni simili. Windows dispone di un'implementazione più vasta poiché CoreFX implementa alcune funzionalità esclusive di Windows, ad esempio [Microsoft.Win32.Registry](https://github.com/dotnet/corefx/tree/master/src/Microsoft.Win32.Registry), ma non implementa i concetti esclusivi di Unix. Si può inoltre notare che la maggior parte delle implementazioni di Linux e macOS sono condivise con un'implementazione di Unix, mentre le implementazioni specifiche di Linux e macOS sono analoghe nella dimensione.


In .NET Core è disponibile una combinazione di librerie specifiche della piattaforma e indipendenti dalla piattaforma. È possibile visualizzarne le caratteristiche in alcuni esempi:

- [CoreCLR](https://github.com/dotnet/coreclr) è specifica della piattaforma. Viene compilata in C/C++, pertanto è specifica della piattaforma per costruzione.
- [System.IO](https://github.com/dotnet/corefx/tree/master/src/System.IO) e [System.Security.Cryptography.Algorithms](https://github.com/dotnet/corefx/tree/master/src/System.Security.Cryptography.Algorithms) sono specifiche della piattaforma, dato che le API di archiviazione e crittografia differiscono in modo significativo in ogni sistema operativo. 
- [System.Collections](https://github.com/dotnet/corefx/tree/master/src/System.Collections) e [System.Linq](https://github.com/dotnet/corefx/tree/master/src/System.Linq) sono indipendenti dalla piattaforma, dato che creano e operano su strutture di dati.

## <a name="comparisons-to-other-net-platforms"></a>Confronto con altre piattaforme .NET

Per semplificare la comprensione dell'importanza di .NET Core, può essere utile un confronto con altre piattaforme .NET esistenti. 

### <a name="comparison-with-net-framework"></a>Confronto con .NET Framework

La piattaforma .NET è stata annunciata per la prima volta da Microsoft nel 2000 e da quel momento ha conosciuto una notevole evoluzione. .NET Framework è stato il prodotto .NET principale prodotto da Microsoft durante oltre 15 anni. 

Differenze principali tra .NET Core e .NET Framework: 

- **Modelli di app**: .NET Core non supporta tutti i modelli di app di .NET Framework, in parte perché molti di questi si basano sulle tecnologie Windows, ad esempio WPF (basato su DirectX). La console e i modelli di app ASP.NET Core sono supportati sia da .NET Core che da .NET Framework. 
- **API**: .NET Core contiene molte delle API di .NET Framework, ma in numero inferiore e con caratteristiche diverse (i nomi degli assembly sono diversi; il tipo è diverso nei casi principali). Queste differenze attualmente richiedono modifiche all'origine della porta per .NET Core. .NET Core implementa l'API della [libreria .NET Standard](../standard/library.md), che nel tempo potrà includere un numero maggiore di API BCL di .NET Framework.
- **Sottosistemi**: .NET Core implementa un sottoinsieme dei sottosistemi di .NET Framework, al fine di ottenere un'implementazione più semplice e un modello di programmazione. Ad esempio, la sicurezza dall'accesso di codice non è supportata, mentre la reflection lo è.
- **Piattaforme**: .NET Framework supporta Windows e Windows Server, mentre .NET Core supporta anche macOS e Linux.
- **Open Source**: .NET Core è open source, mentre in [.NET Framework è open source un sottoinsieme di sola lettura](https://github.com/microsoft/referencesource).

.NET Core è univoco e presenta differenze significative rispetto a .NET Framework e altre piattaforme .NET, ma consente di condividere il codice in modo molto semplice tramite l'origine o tecniche di condivisione binaria. 

### <a name="comparison-with-mono"></a>Confronto con Mono

[Mono](http://www.mono-project.com/) è la multipiattaforma originale e [open source](https://github.com/mono/mono) dell'implementazione .NET, rilasciata nel 2004. Può essere considerato un duplicato della community di .NET Framework. Il team di progetto di Mono si basava sugli [standard .NET](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) open source (in particolare ECMA 335) pubblicati da Microsoft per fornire un'implementazione compatibile.

Le differenze principali tra .NET Core e Mono sono:

- **Modelli di app**: Mono supporta un sottoinsieme dei modelli di app di .NET Framework (ad esempio, Windows Form) e alcuni modelli aggiuntivi (ad esempio, [Xamarin.IOS](https://www.xamarin.com/platform)) attraverso il prodotto Xamarin. .NET Core non li supporta.
- **API**: Mono supporta un [ampio sottoinsieme](http://docs.go-mono.com/?link=root%3a%2fclasslib) delle API di .NET Framework e usa gli stessi nomi di assembly e le stesse caratteristiche.
- **Piattaforme**: Mono supporta molte piattaforme e CPU.
- **Open source**: Mono e .NET Core usano entrambi la licenza MIT e sono progetti di .NET Foundation.
- **Obiettivo**: l'obiettivo principale di Mono negli ultimi anni sono le piattaforme per dispositivi mobili, mentre quello di .NET Core sono i carichi di lavoro cloud.

