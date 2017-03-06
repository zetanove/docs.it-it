---
title: "Portabilità in .NET Core - Analisi delle dipendenze di terze parti"
description: "Portabilità in .NET Core - Analisi delle dipendenze di terze parti"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: b446e9e0-72f6-48f6-92c6-70ad0ce3f86a
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 5b7bbc0718817365df63db4d8ca7e4cf8871abae
ms.lasthandoff: 03/02/2017

---

# <a name="porting-to-net-core---analyzing-your-third-party-party-dependencies"></a>Portabilità in .NET Core - Analisi delle dipendenze di terze parti

Il primo passaggio nel processo di trasferimento consiste nel comprendere le dipendenze di terze parti.  È necessario capire se alcune di esse non vengono ancora eseguite su .NET Core e sviluppare un piano di emergenza adeguato.

## <a name="prerequisites"></a>Prerequisiti

Questo articolo presuppone che si usino Windows e Visual Studio e che si disponga di codice attualmente in esecuzione su .NET Framework.

## <a name="analyzing-nuget-packages"></a>Analisi dei pacchetti NuGet

L'analisi dei pacchetti NuGet per la portabilità è molto semplice.  Poiché un pacchetto NuGet è un set di cartelle che contengono gli assembly specifici della piattaforma, è sufficiente verificare se è presente una cartella che contiene un assembly .NET Core.

L'esplorazione delle cartelle del pacchetto NuGet è più semplice con lo strumento [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).  Ecco come eseguire questa operazione.

1. Scaricare e aprire NuGet Package Explorer.
2. Fare clic su "Open package from online feed" (Apri il pacchetto dal feed online).
3. Cercare il nome del pacchetto.
4. Espandere la cartella "lib" sul lato destro e osservare i nomi delle cartelle.

È inoltre possibile visualizzare gli elementi supportati da un pacchetto in [nuget.org](https://www.nuget.org/) nella sezione **Dependencies** (Dipendenze) della pagina del pacchetto.

In entrambi i casi, è necessario cercare una cartella o una voce in [nuget.org](https://www.nuget.org/) con uno qualsiasi dei nomi seguenti:

```
netstandard1.0
netstandard1.1
netstandard1.2
netstandard1.3
netstandard1.4
netstandard1.5
netstandard1.6
netcoreapp1.0
portable-net45-win8
portable-win8-wpa8
portable-net451-win81
portable-net45-win8-wpa8-wpa81
```

Si tratta dei Target Framework Moniker (TFM) che corrispondono alle versioni della [libreria .NET Standard](../../standard/library.md) e dei profili tradizionali della libreria di classi portabile compatibili con .NET Core.  Si noti che `netcoreapp1.0`, anche se compatibile, è adatto alle applicazioni non alle librerie.  Anche se non vi sono problemi con l'uso di una libreria basata su `netcoreapp1.0`, è possibile che tale libreria non sia prevista per un utilizzo *diverso* da quello per le applicazioni `netcoreapp1.0`.

Sono disponibili anche alcuni TFM legacy usati nelle versioni provvisorie di .NET Core che possono essere compatibili:

```
dnxcore50
dotnet5.0
dotnet5.1
dotnet5.2
dotnet5.3
dotnet5.4
dotnet5.5
```

**Anche se questi funzioneranno con il codice, non esiste alcuna garanzia di compatibilità**.  I pacchetti con questi TFM sono stati creati con le versioni provvisorie dei pacchetti di .NET Core.  Prendere nota di quando (o se) pacchetti come questo sono aggiornati per essere basati su `netstandard`.

> [!NOTE]
> Per usare un pacchetto che ha come destinazione una libreria di classi portabile tradizionale o una versione provvisoria di .NET Core, è necessario usare la direttiva `imports` nel file `project.json`.

### <a name="what-to-do-when-your-nuget-package-dependency-doesnt-run-on-net-core"></a>Operazioni da eseguire quando una dipendenza del pacchetto NuGet non viene eseguita in .NET Core

Se la dipendenza da un pacchetto NuGet non viene eseguita in .NET Core, è possibile effettuare alcune operazioni.

1. Se il progetto è open source e ospitato in una posizione come GitHub, è possibile coinvolgere direttamente gli sviluppatori.
2. È possibile contattare l'autore direttamente su [nuget.org](https://www.nuget.org/) cercando il pacchetto e facendo clic su "Contact Owners" (Contatta i proprietari) sul lato sinistro della pagina del pacchetto.
3. È possibile cercare un altro pacchetto che viene eseguito in .NET Core e che esegue la stessa attività del pacchetto in uso.
4. È possibile tentare di scrivere autonomamente il codice eseguito dal pacchetto.
5. È inoltre possibile eliminare la dipendenza del pacchetto modificando la funzionalità dell'app, almeno fino a quando una versione compatibile del pacchetto non diventa disponibile.

Si ricordi che i gestori di progetti open source e gli autori di pacchetti NuGet sono spesso volontari che contribuiscono perché interessati a un determinato dominio, lo fanno gratuitamente e spesso si occupano di altro. Se si riesce a mettersi in comunicazione, è consigliabile iniziare con un'affermazione positiva sulla libreria prima di chiedere supporto per .NET Core.

Se non si riesce a risolvere il problema con nessuna delle indicazioni precedenti, è possibile che si debba eseguire il trasferimento in .NET Core in un altro momento.

Per il team di .NET è molto importante sapere quali librerie risultano più importanti, al fine di migliorare il supporto di .NET Core. È possibile anche inviare un messaggio di posta elettronica sulle librerie preferite all'indirizzo dotnet@microsoft.com.

## <a name="analyzing-dependencies-which-arent-nuget-packages"></a>Analisi delle dipendenze non appartenenti ai pacchetti NuGet

È possibile disporre di dipendenze non appartenenti a un pacchetto NuGet, ad esempio una DLL nel file system.  L'unico modo per determinare la portabilità di tale dipendenza è l'esecuzione dello [strumento ApiPort](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/).

## <a name="next-steps"></a>Passaggi successivi

Se si esegue il trasferimento di una libreria, consultare [Porting your Libraries](libraries.md) (Portabilità delle librerie).

