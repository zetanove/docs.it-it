---
title: Informazioni di riferimento di csproj | Microsoft Docs
description: Informazioni sulle differenze tra i file csproj esistenti e .NET Core
keywords: informazioni di riferimento, csproj, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/03/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: b4fb772973607b94e120377879a5dbdde2a25271
ms.openlocfilehash: cd0b59b4a91dc4a83d73db55d8d0e611f73f63a6
ms.lasthandoff: 03/15/2017

---

# <a name="additions-to-the-csproj-format-for-net-core"></a>Aggiunte al formato csproj per .NET Core

Questo documento descrive le modifiche aggiunte ai file di progetto nell'ambito del passaggio da *project.json* a *csproj* e a [MSBuild](https://github.com/Microsoft/MSBuild). Per altre informazioni sulla sintassi generale dei file di progetto e informazioni di riferimento, vedere la documentazione del [file di progetto MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference).  

## <a name="implicit-package-references"></a>Riferimenti impliciti al pacchetto
È ora possibile fare riferimento ai metapacchetti in modo implicito in base al framework di destinazione specificato nella proprietà `<TargetFramework>` o `<TargetFrameworks>` del file di progetto. Se il framework di destinazione è `netcoreap1.x`, viene fatto riferimento alla versione appropriata del metapacchetto `Microsoft.NETCore.App`. Se invece il framework di destinazione è `netstandard1.x`, viene fatto riferimento alla versione appropriata del metapacchetto `NetStandard.Library`.

Per quanto riguarda il resto del comportamento, gli strumenti funzionano come previsto e la maggior parte dei movimenti, ad esempio `dotnet restore`, rimangono invariati. 

### <a name="recommendations"></a>Suggerimenti
Poiché ora si fa riferimento ai metapacchetti `Microsoft.NETCore.App` o `NetStandard.Library` in modo implicito, ecco le procedure consigliate:

* Non fare mai riferimento in modo esplicito ai metapacchetti `Microsoft.NETCore.App` o `NetStandard.Library` tramite la proprietà `<PackageReference>` nel file di progetto.
* Se occorre una versione specifica del runtime, è necessario usare la proprietà `<RuntimeFrameworkVersion>` del progetto, ad esempio, `1.0.4`, anziché fare riferimento al metapacchetto.
    * Ciò può avvenire se si usano [distribuzioni autosufficienti](../deploying/index.md#self-contained-deployments-scd) e occorre una versione specifica, ad esempio, della patch del runtime 1.0.0 LTS.
* Se occorre una versione specifica del metapacchetto `NetStandard.Library`, è possibile usare la proprietà `<NetStandardImplicitPackageVersion>` e impostare la versione necessaria. 

## <a name="default-compilation-includes-in-net-core-projects"></a>Dichiarazioni Include di compilazione predefinite nei progetti .NET Core
Con il passaggio al formato *csproj* nelle ultime versioni dell'SDK, per gli elementi di compilazione e le risorse incorporate le dichiarazioni Include ed Exclude predefinite sono state spostate nei file delle proprietà dell'SDK. Ciò significa che non è più necessario specificare queste dichiarazioni nel file di progetto. 

Il motivo principale di questo cambiamento è la riduzione del disordine nel file di progetto. Le dichiarazioni predefinite presenti nell'SDK coprono i casi di utilizzo più comuni, pertanto non c'è alcuna necessità di ripeterle per ogni progetto creato. Di conseguenza, i file di progetto sono più piccoli e molto più semplici da comprendere e, se necessario, da modificare manualmente. 

La tabella seguente mostra gli elementi e i [GLOB](https://en.wikipedia.org/wiki/Glob_(programming)) Include ed Exclude nell'SDK: 

| Elemento              | GLOB Include                               | GLOB Exclude                                                     | GLOB Remove                  |
|-------------------|-------------------------------------------|---------------------------------------------------------------|----------------------------|
| Compile              | \*\*/\*.cs (o altre estensioni del linguaggio) | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | N/D                          |
| EmbeddedResource     | \*\*/\*.resx                                 | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | N/D                          |
| Nessuno                 | \*\*/\*                                      | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | - \*\*/\*.cs; \*\*/\*.resx |

Se si tenta di compilare un progetto contenente GLOB con l'SDK più recente, viene visualizzato l'errore seguente:

> Duplicate Compile items were included. (Sono stati inclusi elementi di compilazione duplicati) The .NET SDK includes Compile items from your project directory by default. (Per impostazione predefinita, .NET SDK include elementi Compile della directory di progetto) You can either remove these items from your project file, or set the 'EnableDefaultCompileItems' property to 'false' if you want to explicitly include them in your project file. (Rimuovere questi elementi dal file di progetto o impostare la proprietà 'EnableDefaultCompileItems' su 'false' se li si vuole includere esplicitamente nel file di progetto) 

Per ovviare a questo errore, è possibile rimuovere gli elementi `Compile` corrispondenti a quelli elencati nella tabella precedente oppure impostare la proprietà `<EnableDefaultCompileItems>` su `false`, come segue:

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```
Se si imposta questa proprietà su `false`, si esegue l'override dell'inclusione implicita e viene ripristinato il comportamento degli SDK precedenti, in cui era necessario specificare i GLOB predefiniti nel progetto. 

Questa modifica non influisce sulle funzioni principali delle altre dichiarazioni Include. Se tuttavia si vogliono specificare, ad esempio, alcuni file da pubblicare con l'app, è ancora possibile usare i meccanismi noti in *csproj*, ad esempio l'elemento `<Content>`.

### <a name="recommendation"></a>Consiglio
Con csproj è consigliabile rimuovere i GLOB predefiniti dal progetto e aggiungere i percorsi di file con GLOB solo per gli artifact necessari all'app o alla libreria per diversi scenari (runtime, creazione di pacchetti NuGet e così via).


## <a name="additions"></a>Aggiornamenti

### <a name="sdk-attribute"></a>Attributo Sdk 
L'elemento `<Project>` del file *.csproj* ha un nuovo attributo, denominato `Sdk`. `Sdk` specifica l'SDK che viene usato dal progetto. l'SDK, come descritto dal [documento sui livelli](cli-msbuild-architecture.md), è un set di [attività](https://docs.microsoft.com/visualstudio/msbuild/msbuild-tasks) e [destinazioni](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) di MSBuild che consente di compilare codice .NET Core. Con gli strumenti di .NET Core vengono forniti due SDK principali:

1. .NET Core SDK con l'ID di `Microsoft.NET.Sdk`
2. .NET Core Web SDK con l'ID di `Microsoft.NET.Sdk.Web`

Per usare gli strumenti di .NET Core e compilare il codice, è necessario impostare l'attributo `Sdk` su uno di questi ID nell'elemento `<Project>`. 

### <a name="packagereference"></a>PackageReference
Elemento che specifica una dipendenza NuGet nel progetto. L'attributo `Include` specifica l'ID del pacchetto. 

```xml
<PackageReference Include="<package-id>" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

#### <a name="version"></a>Versione
`Version` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

#### <a name="includeassets-excludeassets-and-privateassets"></a>IncludeAssets, ExcludeAssets e PrivateAssets
L'attributo `IncludeAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` devono essere usati. 

L'attributo `ExcludeAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` non devono essere usati.

L'attributo `PrivateAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` devono essere usati. Specifica, inoltre, che tali asset non devono essere trasmessi al progetto successivo. 

> [!NOTE]
> `PrivateAssets` equivale all'elemento *project.json*/*xproj* `SuppressParent`.

Questi attributi possono contenere uno o più degli elementi seguenti:

* `Compile`: i contenuti della cartella lib sono disponibili per la compilazione.
* `Runtime`: vengono distribuiti i contenuti della cartella runtime.
* `ContentFiles`: vengono usati i contenuti della cartella *contentfiles*.
* `Build`: vengono usate le proprietà/destinazioni nella cartella build.
* `Native`: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* `Analyzers`: vengono usati gli analizzatori.

In alternativa, l'attributo può contenere:

* `None`: nessuno degli asset viene usato.
* `All`: vengono usati tutti gli asset.

### <a name="dotnetclitoolreference"></a>DotNetCliToolReference
L'elemento `<DotNetCliToolReference>` specifica lo strumento dell'interfaccia della riga di comando che si vuole ripristinare nel contesto del progetto. Si tratta di una sostituzione per il nodo `tools` in *project.json*. 

```xml
<DotNetCliToolReference Include="<package-id>" Version="" />
```

#### <a name="version"></a>Versione
`Version` specifica la versione del pacchetto da ripristinare. L'attributo rispetta le regole dello schema di numerazione delle versioni NuGet.

### <a name="runtimeidentifiers"></a>Identificatori di runtime
L'elemento `<RuntimeIdentifiers>` consente di specificare un elenco delimitato da punto e virgola di [identificatori di runtime (RID)](../rid-catalog.md) per il progetto. I RID consentono di pubblicare distribuzioni autonome. 

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```


### <a name="runtimeidentifier"></a>RuntimeIdentifier
L'elemento `<RuntimeIdentifier>` consente di specificare un solo [identificatore di runtime (RID)](../rid-catalog.md) per il progetto. I RID consentono di pubblicare una distribuzione autonoma. 

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```


### <a name="packagetargetfallback"></a>PackageTargetFallback 
L'elemento `<PackageTargetFallback>` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti. È progettato per consentire ai pacchetti che usano il [TxM (Target x Moniker)](https://docs.microsoft.com/nuget/schema/target-frameworks) di .NET di interagire con pacchetti che non dichiarano un TxM di .NET. Se il progetto usa il TxM di .NET, devono averlo anche tutti i pacchetti da cui il progetto dipende, a meno che non si aggiunga `<PackageTargetFallback>` al progetto, in modo da rendere compatibili con .NET le piattaforme che non lo sono. 

L'esempio seguente include i fallback per tutte le destinazioni nel progetto: 

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

L'esempio seguente specifica i fallback solo per la destinazione `netcoreapp1.0`:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp1.0'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="nuget-metadata-properties"></a>Proprietà dei metadati NuGet
Con il passaggio a MSbuild, i metadati di input usati per la creazione di un pacchetto NuGet sono stati spostati da file *project.json* a file *.csproj*. Gli input sono proprietà di MSBuild, quindi devono trovarsi all'interno di un gruppo `<PropertyGroup>`. L'elenco seguente include le proprietà usate come input per il processo di creazione del pacchetto quando si usa il comando `dotnet pack` o la destinazione di MSBuild `Pack` che fa parte dell'SDK. 

### <a name="ispackable"></a>IsPackable
Valore booleano che specifica se dal progetto può essere creato un pacchetto. Il valore predefinito è `true`. 

### <a name="packageversion"></a>PackageVersion
Specifica la versione che avrà il pacchetto risultante. Accetta tutte le forme della stringa di versione NuGet. Il valore predefinito corrisponde al valore di `$(Version)`, vale a dire della proprietà `Version` nel progetto. 

### <a name="packageid"></a>PackageId
Specifica il nome del pacchetto risultante. Se non specificato, l'impostazione predefinita per l'operazione `pack` corrisponde all'uso di `AssemblyName` o del nome della directory come nome del pacchetto. 

### <a name="title"></a>Titolo
Titolo del pacchetto facilmente comprensibile per l'utente, usato di solito per la visualizzazione dell'interfaccia utente, ad esempio in nuget.org e in Gestione pacchetti in Visual Studio. Se non specificato, viene usato l'ID del pacchetto.

### <a name="authors"></a>Autori
Elenco con valori delimitati da punto e virgola di autori di pacchetti, corrispondenti ai nomi di profilo in nuget.org. Questi, visualizzati nella raccolta NuGet in nuget.org, vengono usati per creare riferimenti incrociati ai pacchetti dello stesso autore.

### <a name="description"></a>Descrizione
Descrizione lunga del pacchetto per la visualizzazione dell'interfaccia utente.

### <a name="copyright"></a>Copyright
Informazioni sul copyright per il pacchetto.

### <a name="packagerequirelicenseacceptance"></a>PackageRequireLicenseAcceptance
Valore booleano che specifica se il client deve richiedere al consumer di accettare la licenza del pacchetto prima di installarlo. Il valore predefinito è `false`.

### <a name="packagelicenseurl"></a>PackageLicenseUrl
URL della licenza applicabile al pacchetto.

### <a name="packageprojecturl"></a>PackageProjectUrl
URL della pagina iniziale del pacchetto, spesso visualizzato nell'interfaccia utente e in nuget.org.

### <a name="packageiconurl"></a>PackageIconUrl
URL di un'immagine 64 x 64 con sfondo trasparente da usare come icona per il pacchetto nella visualizzazione dell'interfaccia utente.

### <a name="packagereleasenotes"></a>PackageReleaseNotes
Note sulla versione per il pacchetto.

### <a name="packagetags"></a>PackageTags
Elenco di tag con valori delimitati da punto e virgola che designa il pacchetto.

### <a name="packageoutputpath"></a>PackageOutputPath
Determina il percorso di output in cui verrà rilasciato il pacchetto creato. Il valore predefinito è `$(OutputPath)`. 

### <a name="includesymbols"></a>IncludeSymbols
Valore booleano che indica se al momento della creazione del pacchetto deve essere creato un pacchetto aggiuntivo di simboli. Questo pacchetto, con estensione *.symbols.nupkg*, copierà i file PDB insieme ai file DLL e ad altri file di output.

### <a name="includesource"></a>IncludeSource
Valore booleano che indica se il processo di creazione del pacchetto deve creare un pacchetto di origine. Il pacchetto di origine contiene il codice sorgente della libreria, nonché i file PDB. I file di origine vengono posizionati nella directory `src/ProjectName` del file del pacchetto risultante. 

### <a name="istool"></a>IsTool
Specifica se tutti i file di output devono essere copiati nella cartella *tools* anziché nella cartella *lib*. È diverso da `DotNetCliTool`, che viene specificato impostando `PackageType` nel file *.csproj*.

### <a name="repositoryurl"></a>RepositoryUrl
Specifica l'URL per l'archivio in cui si trova il codice sorgente per il pacchetto e/o da cui il codice sorgente viene compilato. 

### <a name="repositorytype"></a>RepositoryType
Specifica il tipo dell'archivio. Il valore predefinito è "git". 

### <a name="nopackageanalysis"></a>NoPackageAnalysis
Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo.

### <a name="minclientversion"></a>MinClientVersion
Specifica la versione minima del client NuGet, imposta da nuget.exe e da Gestione pacchetti di Visual Studio, che può installare questo pacchetto.

### <a name="includebuildoutput"></a>IncludeBuildOutput
Valore booleano che specifica se gli assembly di output di compilazione devono essere compresi nel file *.nupkg*.

### <a name="includecontentinpack"></a>IncludeContentInPack
Questo valore booleano specifica se gli elementi con tipo `Content` verranno inclusi automaticamente nel pacchetto risultante. Il valore predefinito è `true`. 

### <a name="buildoutputtargetfolder"></a>BuildOutputTargetFolder
Specifica la cartella in cui posizionare gli assembly di output. Gli assembly di output (e altri file di output) vengono copiati nelle rispettive cartelle per framework.

### <a name="contenttargetfolders"></a>ContentTargetFolders
Questa proprietà specifica il percorso predefinito in cui devono essere posizionati tutti i file di contenuto se per tali file `PackagePath` non è specificato. Il valore predefinito è "content;contentFiles".

### <a name="nuspecfile"></a>NuspecFile
Percorso relativo o assoluto per il file *.nuspec* usato per la creazione del pacchetto. 

> [!NOTE]
> Se il file *.nuspec* è specificato, viene usato **esclusivamente** per le informazioni di creazione del pacchetto e le informazioni nei progetti non vengono usate. 

### <a name="nuspecbasepath"></a>NuspecBasePath
Percorso di base per il file *.nuspec*.

### <a name="nuspecproperties"></a>NuspecProperties
Elenco con valori delimitati da punto e virgola di coppie chiave=valore.

