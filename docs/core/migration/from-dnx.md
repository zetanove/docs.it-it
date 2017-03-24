---
title: Migrazione da DNX all&quot;interfaccia della riga di comando .NET Core
description: Migrazione da DNX all&quot;interfaccia della riga di comando .NET Core
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c0d70120-78c8-4d26-bb3c-801f42fc2366
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: a6f90a43b5f129cd246546f2cc36c4b97c3fb15c
ms.lasthandoff: 03/07/2017

---

# <a name="migrating-from-dnx-to-net-core-cli-projectjson"></a>Migrazione da DNX all'interfaccia della riga di comando di .NET Core (project.json)

## <a name="overview"></a>Panoramica
La versione RC1 di .NET Core e ASP.NET Core 1.0 Microsoft hanno presentato gli strumenti DNX. La versione RC2 di .NET Core e ASP.NET Core 1.0 hanno eseguito il passaggio da DNX all'interfaccia della riga di comando di .NET Core.

Di seguito è riportato un breve riepilogo delle caratteristiche di DNX. DNX è un runtime e un set di strumenti usati per creare applicazioni .NET Core e, più specificamente, ASP.NET Core 1.0. È costituito da tre componenti principali:

1. DNVM: uno script di installazione per l'acquisizione di DNX
2. DNX (Dotnet Execution Runtime): il runtime che esegue il codice
3. DNU (Dotnet Developer Utility): strumenti per la gestione delle dipendenze e per la creazione e la pubblicazione di applicazioni

Con l'introduzione dell'interfaccia della riga di comando, tutti gli elementi sopra elencati sono parte di un unico set di strumenti. Tuttavia, poiché DNX era disponibile durante il periodo di commercializzazione della versione RC1, è possibile che gli utenti dispongano di progetti creati con DNX di cui vogliono eseguire la migrazione ai nuovi strumenti dell'interfaccia della riga di comando. 

Questa guida fornisce le istruzioni di base per la migrazione dei progetti da DNX all'interfaccia della riga di comando di .NET Core. Se si sta iniziando un progetto direttamente in .NET Core, è possibile ignorare questo documento. 

## <a name="main-changes-in-the-tooling"></a>Principali modifiche apportate agli strumenti
Riguardo agli strumenti sono state apportate alcune modifiche di carattere generale che devono essere descritte per prime. 

### <a name="no-more-dnvm"></a>DNVM non più disponibile
DNVM, acronimo di *DotNet Version Manager*, era uno script bash/PowerShell usato per installare un'istanza di DNX nel computer in uso. DNVM consentiva agli utenti di ottenere il DNX necessario dal feed specificato o dai feed predefiniti. Permetteva inoltre di contrassegnare un determinato DNX come "attivo", inserendolo in $PATH per la sessione in oggetto. Questo consentiva di usare i diversi strumenti.

DNVM è stato messo fuori produzione perché il relativo set di funzionalità è ormai ridondante a causa delle modifiche apportate agli strumenti dell'interfaccia della riga di comando di .NET Core.

Gli strumenti dell'interfaccia della riga di comando vengono distribuiti in pacchetti in due modi principali:

1. Programmi di installazione nativi per una determinata piattaforma
2. Script di installazione per altre situazioni, ad esempio server CI

Tenendo conto di quanto affermato sopra, le funzionalità di installazione DNVM non sono necessarie. Qual è tuttavia la situazione per le funzionalità di selezione del runtime? 

Si fa riferimento a un runtime in `project.json` aggiungendo alle dipendenze un pacchetto di una determinata versione. Con questa modifica, l'applicazione sarà in grado di usare i nuovi componenti di runtime. L'installazione di questi componenti nel computer in uso è analoga all'installazione con l'interfaccia della riga di comando: è possibile installare il runtime tramite uno dei programmi di installazione nativi oppure tramite lo script di installazione. 

### <a name="different-commands"></a>Comandi differenti
Se si usa DNX, sono disponibili i comandi di uno dei tre componenti (DNX, DNU o DNVM). Con l'interfaccia della riga di comando, alcuni di questi comandi risultano diversi, alcuni non sono disponibili e altri infine sono uguali ma con una semantica leggermente differente. 

La tabella seguente mostra il mapping tra i comandi DNX/DNU e i corrispondenti comandi dell'interfaccia della riga di comando.


| Comando DNX                        | Comando dell'interfaccia della riga di comando        | Descrizione                                                                                                         |
|--------------------------------    |----------------    |-----------------------------------------------------------------------------------------------------------------    |
| dnx run                            | dotnet run         | Esegue il codice dall'origine.                                                                                               |
| dnu build                          | dotnet build       | Crea un file binario IL (Intermediate Language) del codice.                                                                                    |
| dnu pack                           | dotnet pack        | Crea un pacchetto NuGet del codice.                                                                            |
| dnx \[command] (ad esempio, "dnx web")     | N/D\*              | In DNX esegue un comando in base a quanto definito nel file project.json.                                                         |
| dnu install                        | N/D\*              | In DNX installa un pacchetto come dipendenza.                                                                |
| dnu restore                        | dotnet restore     | Ripristina le dipendenze specificate nel file project.json.                                                                |
| dnu publish                        | dotnet publish     | Pubblica l'applicazione per la distribuzione in una delle tre forme possibili: portabile, portabile con nativo e autonoma.     |
| dnu wrap                           | N/D\*              | In DNX esegue il wrapping di un file project.json in csproj.                                                                        |
| dnu commands                       | N/D\*              | In DNX gestisce i comandi installati a livello globale.                                                               |

(\*) Queste funzionalità non sono supportate nell'interfaccia della riga di comando in base alla progettazione. 

## <a name="dnx-features-that-are-not-supported"></a>Funzionalità DNX non supportate
Come mostrato dalla tabella sopra riportata, esistono alcune funzionalità di DNX che, almeno per il momento, si è deciso di non supportare nell'interfaccia della riga di comando. Questa sezione indica le più importanti di queste funzionalità e descrive i motivi per cui non sono supportate. Illustra inoltre le soluzioni alternative da adottare nel caso in cui sia comunque necessario usare queste funzionalità.

### <a name="global-commands"></a>Comandi globali
DNU integrava un concetto denominato "comandi globali". Si trattava essenzialmente di applicazioni console create come pacchetti NuGet con uno script della shell che richiamava il DNX specificato per l'esecuzione dell'applicazione. 

L'interfaccia della riga di comando non supporta questo concetto. Supporta tuttavia l'aggiunta di comandi per progetto che è possibile richiamare usando la comune sintassi `dotnet <command>`. Per altre informazioni, vedere [Extensibility overview](../tools/index.md#extensibility) (Panoramica sull'estendibilità). 

### <a name="installing-dependencies"></a>Installazione delle dipendenze
A partire dalla versione&1;, gli strumenti dell'interfaccia della riga di comando di .NET Core non dispongono di un comando `install` per l'installazione delle dipendenze. Per installare un pacchetto da NuGet, è necessario aggiungerlo come dipendenza al file `project.json` e quindi eseguire `dotnet restore`. 

### <a name="running-your-code"></a>Esecuzione del codice
È possibile eseguire il codice in due modi: Dal sorgente, con `dotnet run`. A differenza di `dnx run`, questo comando non esegue alcuna compilazione in memoria, ma richiama `dotnet build` per compilare il codice e quindi eseguire il file binario compilato. 

Un altro modo consiste nell'usare `dotnet` per eseguire il codice. A tale scopo, fornire un percorso all'assembly: `dotnet path/to/an/assembly.dll`. 

## <a name="migrating-your-dnx-project-to-net-core-cli"></a>Migrazione di un progetto DNX all'interfaccia della riga di comando di .NET Core
Oltre all'uso di nuovi comandi per la gestione del codice, la migrazione da DNX consente anche le tre operazioni seguenti:

1. Migrazione del file `global.json` se tale file è in grado di usare l'interfaccia della riga di comando.
2. Migrazione del file di progetto stesso (`project.json`) agli strumenti dell'interfaccia della riga di comando.
3. Migrazione di qualsiasi API DNX alla corrispondente controparte BCL. 

### <a name="changing-the-globaljson-file"></a>Modifica del file global.json
Il file `global.json` funge da file di soluzione sia per progetti RC1 che per progetti RC2 (o versioni successive). Per consentire agli strumenti dell'interfaccia della riga di comando (oltre che a Visual Studio) di distinguere tra RC1 e le versioni successive, viene usata la proprietà `"sdk": { "version" }`. Tale proprietà consente di stabilire se un progetto è stato creato con RC1 o una versione successiva. Se il file `global.json` non dispone affatto di questo nodo, presuppone che si tratti della versione più recente. 

Per aggiornare il file `global.json`, rimuovere la proprietà o impostarla sulla versione esatta degli strumenti che si intende usare, in questo caso **1.0.0-preview2-003121**:

```json
{
    "sdk": {
        "version": "1.0.0-preview2-003121"
    }
}
```

### <a name="migrating-the-project-file"></a>Migrazione del file di progetto
L'interfaccia della riga di comando e DNX usano entrambi lo stesso sistema di progetto basato sul file `project.json`. La sintassi e la semantica del file di progetto sono molto simili, a parte alcune differenze dipendenti dallo scenario. Sono presenti anche alcune modifiche dello schema che è possibile vedere nel [file di schema](http://json.schemastore.org/project) o, in modo più semplice, nell'argomento [project.json reference](../tools/project-json.md) (Riferimento project.json). 

Se si sta creando un'applicazione console, è necessario aggiungere al file di progetto il frammento seguente:

```json
"buildOptions": {
    "emitEntryPoint": true
}
```

Questo frammento indica a `dotnet build` di creare un punto di ingresso per l'applicazione, consentendo così l'esecuzione del codice. Se si sta creando una libreria di classi, ignorare semplicemente questa sezione. Naturalmente, dopo aver aggiunto al file `project.json` il frammento sopra riportato, è necessario aggiungere un punto di ingresso statico. Con la sospensione di DNX, i servizi DI forniti da quest'ultimo non sono più disponibili e il punto di ingresso statico deve essere un punto di ingresso .NET di base: `static void Main()`.

Se nel file `project.json` è presente una sezione "commands", è possibile rimuoverla. Alcuni comandi usati per rappresentare comandi DNU, ad esempio comandi dell'interfaccia della riga di comando di Entity Framework, vengono trasferiti nell'interfaccia della riga di comando come estensioni per progetto. Se sono stati creati comandi personalizzati che vengono usati nei progetti, è necessario sostituirli con estensioni dell'interfaccia della riga di comando. In questo caso, il nodo `commands` di `project.json` deve essere sostituito dal nodo `tools`. Tale nodo deve elencare le dipendenze degli strumenti, come illustrato nella sezione [CLI extensibility](../tools/index.md#extensibility) (Estendibilità dell'interfaccia della riga di comando). 

Al termine di queste operazioni, è necessario decidere il tipo di portabilità per l'app. Con .NET Core, Microsoft ha reso disponibile un'ampia gamma di opzioni di portabilità. È possibile, ad esempio, creare un'applicazione completamente *portabile* o un'applicazione *autonoma*. Il funzionamento di un'applicazione portabile è simile a quello delle applicazioni .NET Framework: è necessario un componente condiviso (.NET Core) da eseguire nel computer di destinazione. L'applicazione autonoma non richiede l'installazione di .NET Core nel computer di destinazione, ma è necessario creare un'applicazione per ogni sistema operativo che si vuole supportare. Questi e altri tipi di portabilità sono discussi nel documento  [Application portability type](../deploying/index.md) (Tipo di portabilità delle applicazioni). 

Una volta deciso il tipo di portabilità, è necessario modificare i framework di destinazione. Se si stanno creando applicazioni per .NET Core, è probabile che come framework di destinazione venga usato `dnxcore50`. Con l'interfaccia della riga di comando e i cambiamenti apportati dalla nuova [libreria .NET Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md), è necessario che il framework sia uno dei seguenti:

1. `netcoreapp1.0`: se si stanno creando applicazioni in .NET Core (incluse applicazioni ASP.NET Core)
2. `netstandard1.6`: se si stanno creando librerie di classi per .NET Core

Se si usano altre destinazioni `dnx`, ad esempio `dnx451`, sarà necessario modificare anche tali destinazioni. `dnx451` deve essere modificato in `net451`. Per altre informazioni, vedere il [documento della libreria .NET Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md). 

Il file `project.json` è ora praticamente pronto. È necessario scorrere l'elenco delle dipendenze e aggiornarle alle versioni più recenti, in particolare se si usano dipendenze ASP.NET Core. Se si usano pacchetti separati per le API BCL, è possibile usare il pacchetto di runtime, come spiegato nel documento [Application portability type](../deploying/index.md) (Tipo di portabilità delle applicazioni). 

Al termine, è possibile tentare il ripristino con `dotnet restore`. A seconda della versione delle dipendenze, si potrebbero verificare errori se NuGet non è in grado di risolvere le dipendenze stesse per uno dei framework di destinazione sopra indicati. Si tratta di un problema momentaneo: con il passare del tempo saranno sempre di più i pacchetti che includono il supporto per questi framework. Per ora, se si verifica questo problema, è possibile usare l'istruzione `imports` all'interno del nodo `framework` per indicare a NuGet che può ripristinare i pacchetti che hanno come destinazione il framework indicato nell'istruzione "imports". I messaggi di errore di ripristino visualizzati in questo caso dovrebbero fornire informazioni sufficienti per stabilire quali framework è necessario importare. In caso di dubbi o se si esegue questa operazione per la prima volta, come indicazione generale specificare `dnxcore50` e `portable-net45+win8` nell'istruzione `imports`. Il frammento JSON seguente mostra un esempio di questo scenario:

```json
    "frameworks": {
        "netcoreapp1.0": { 
            "imports": ["dnxcore50", "portable-net45+win8"]
        }
    }
```

L'esecuzione di `dotnet build` mostrerà eventuali errori di compilazione, che tuttavia non dovrebbero essere numerosi. Dopo aver compilato ed eseguito correttamente il codice, è possibile testarlo con Test Runner. Eseguire `dotnet <path-to-your-assembly>` e osservare l'esecuzione.
