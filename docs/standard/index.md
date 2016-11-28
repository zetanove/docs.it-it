---
title: Informazioni su .NET
description: Informazioni su .NET Framework.
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 10/31/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
translationtype: Human Translation
ms.sourcegitcommit: 254e89abefd28419bd2f36a047e4df939f7ff8da
ms.openlocfilehash: 8eb9274def2683fae20765cbf701b706293744fc

---

# <a name="net-platform-guide"></a>Guida alla piattaforma .NET

> [!NOTE]
Questo articolo verrà riscritto.

> Per imparare a creare una semplice applicazione .NET Core, consultare le [esercitazioni introduttive di .NET Core](../core/getting-started.md). Sono necessari pochi minuti per realizzare ed eseguire la prima app.

.NET è una piattaforma di sviluppo con finalità generali che può essere usata per qualsiasi tipo di app o carico di lavoro compatibile con questo genere di soluzioni. Integra diverse funzionalità chiave interessanti per molti sviluppatori, come la gestione automatica della memoria e il supporto per moderni linguaggi di programmazione, che permettono di creare in modo efficiente applicazioni di alta qualità. .NET fornisce agli ambienti di programmazione di alto livello diverse funzionalità pratiche, consentendo al tempo stesso l'accesso a basso livello alla memoria e alle API native.

C#, F# e Visual Basic sono linguaggi diffusi che si basano sulla piattaforma .NET e la usano come destinazione. I linguaggi .NET sono noti per alcune funzionalità chiave come il modello di programmazione asincrona, LINQ (Language-Integrated Query), i tipi generici e la reflection del sistema di tipi. Offrono inoltre numerose opzioni per i paradigmi di programmazione funzionale e orientata agli oggetti.

Questi linguaggi presentano notevoli differenze, a livello di filosofia e sintassi, ma anche diverse simmetrie grazie un sistema di tipi condiviso, che viene fornito dall'ambiente di runtime sottostante. .NET è stato progettato in base al concetto di "common language runtime" che può supportare i requisiti di diversi linguaggi, ad esempio quelli tipizzati in modo statico e dinamico, e consentirne l'interoperabilità. Ad esempio, è possibile passare una raccolta di oggetti `People` tra lingue senza perdita di semantica o funzionalità.

Sono disponibili diversi [prodotti e implementazioni .NET](components.md), basati su [standard .NET](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) aperti che specificano i concetti chiave della piattaforma. Questi standard sono ottimizzati in modo separato per i diversi tipi di applicazione (desktop, dispositivi mobili, giochi, cloud) e supportano numerosi chip, ad esempio x86/x64 e ARM, e sistemi operativi, ad esempio Windows, Linux, iOS, Android e macOS. Anche i componenti open source costituiscono una parte importante dell'ecosistema .NET: diverse implementazioni e librerie .NET, infatti, sono disponibili con licenze approvate da OSI (Open Source Initiative).

- Informazioni su [C#](../csharp/index.md)
- Informazioni su [F#](../fsharp/index.md)
- Sfogliare la [libreria di API .NET](../../api/index.md)
- [Introduction to the Common Language Runtime](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/intro-to-clr.md) (Introduzione a Common Language Runtime)

<a name="fundamentals"></a>Concetti fondamentali
------------

**Più linguaggi**: .NET fornisce un sistema di tipi, formati di file, runtime, framework e strumenti ben definiti che possono essere usati da più linguaggi, sia per l'esecuzione indipendente sia per l'interoperabilità con altri linguaggi usando gli stessi componenti .NET come valuta condivisa.

**Gestione della memoria**: .NET gestisce automaticamente la memoria per l'utente tramite un Garbage Collector. In questo modo si ha la sicurezza di poter fare sempre riferimento a oggetti attivi, evitando spiacevoli problemi come i sovraccarichi del buffer e le violazioni di accesso. È inclusa anche la verifica dei limiti di matrice.

**Indipendenza dai tipi**: il modello .NET principale per la rappresentazione di funzionalità e memoria è costituito dai "tipi". I tipi definiscono la forma e, facoltativamente, il comportamento. Il runtime garantisce che il codice chiamante possa solo agire sui tipi in base alla definizione e alla visibilità specificata dei membri, fornendo risultati coerenti, affidabili e sicuri.

<a name="features"></a>Funzionalità
--------

**Tipi di valore definiti dall'utente**: i tipi di valore sono una categoria di tipi utile poiché offrono la semantica del "passaggio per valore" anziché quella del "passaggio per riferimento", come avviene per le classi. I tipi di valore sono ovviamente utili per i dati numerici. .NET supporta i tipi di valore per i tipi primitivi, ad esempio integer, e per quelli definiti dall'utente.

**Tipi generici**: i tipi generici sono tipi con uno o più parametri di tipo che possono essere specificati in base a istanze. Questa caratteristica è utile per molti tipi, che altrimenti esporrebbero i contenuti come il tipo Object o richiederebbero più definizioni di tipo. Ad esempio, una determinata istanza di un tipo di raccolta può essere specificata in base a persone, località GPS o stringhe.

**Reflection**: .NET definisce un formato di metadati che descrive i tipi all'interno di un file binario. Il sottosistema di reflection usa questi dati esponendo API per la lettura e la creazione di istanze di tipi in fase di esecuzione. Questa funzionalità è particolarmente utile per scenari dinamici in cui non è utile conoscere in anticipo l'implementazione esatta di un programma.

**Generazione di codice flessibile**: .NET non prevede un approccio specifico per la trasformazione di file binari .NET in codice macchina. Molti approcci sono stati applicati con successo, tra cui l'interpretazione, la compilazione JIT (Just-In-Time), la compilazione AOT (Ahead of Time) con fallback JIT e la compilazione AOT senza fallback JIT. Ognuna di queste strategie può essere utile ed esiste la possibilità di usarle insieme.

**Multipiattaforma**: fin dall'inizio, .NET è stato pensato come soluzione multipiattaforma. Il formato binario e il set di istruzioni sono indipendenti dal sistema operativo, dalla CPU e dalla dimensione del puntatore. Un file binario .NET creato nel 2000 per l'esecuzione in un computer Windows a 32 bit può essere eseguito sul dispositivo iOS ARM64 nel 2016 senza alcuna modifica.

<a name="open-source"></a>Open source
-----------

Le implementazioni [.NET Core](https://github.com/dotnet/core) e [Mono](https://github.com/mono/mono) di .NET sono open source e usano la licenza MIT. La documentazione usa la licenza [Creative Commons CC BY](https://creativecommons.org/licenses/by/4.0/). Le implementazioni .NET Core e Mono sono sponsorizzate da Microsoft e hanno molti collaboratori della community. 

Questi runtime con finalità generali possono essere usati come base per la ricerca accademica, per l'insegnamento o la formazione o per i prodotti commerciali. La loro natura aperta offre a chiunque la possibilità di contribuire al codice di prodotto upstream per la risoluzione di un bug o per l'introduzione di una nuova funzionalità.

<a name="projects"></a>Progetti
--------

- [CoreCLR](https://github.com/dotnet/coreclr): runtime .NET, usato da .NET Core.
- [Mono](https://github.com/mono/mono): runtime .NET, usato da Xamarin e altri.
- [CoreFX](https://github.com/dotnet/coreclr): librerie di classi .NET, usate da .NET Core e, fino a un certo livello, da Mono tramite la condivisione del codice di origine.
- [Roslyn](https://github.com/dotnet/roslyn): compilatori C# e Visual Basic, usati dalla maggior parte degli strumenti e delle piattaforme .NET. Espone le API per la lettura, la scrittura e l'analisi del codice sorgente.
- [F#](https://github.com/microsoft/visualfsharp): compilatore F#.
- [SDK Xamarin](http://open.xamarin.com): librerie e strumenti necessari per scrivere codice Android, iOS e macOS in C# e F#.

<a name="standardized"></a>Standardizzato
------------

.NET è basato su [standard ECMA](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) aperti che ne delineano le funzionalità e possono essere usati per creare una nuova implementazione. Esistono altre implementazioni di .NET, tra cui Mono e Unity, che sono le più diffuse oltre a quelle Microsoft.




<!--HONumber=Nov16_HO3-->


