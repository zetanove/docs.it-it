---
title: Riferimenti di project.json
description: Riferimenti di project.json
keywords: .NET, .NET Core, project.json
author: aL3891
ms.author: mairaw
ms.date: 09/30/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 3aef32bd-ee2a-4e24-80f8-a2b615e0336d
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: ce3dbad938c01fd0f9d79cefb29884be986b8e1f

---

# <a name="projectjson-reference"></a>Riferimenti di project.json

Il file project.json viene usato nei progetti .NET Core per definire i metadati del progetto, le informazioni di compilazione e le dipendenze. In questo argomento di riferimento verrà presentato l'elenco di tutte le proprietà che è possibile definire nel file project.json.

> [!NOTE]
> In una futura versione, gli strumenti di .NET Core passeranno da progetti basati su project.json a progetti basati su MSBuild. È consigliabile usare comunque file project.json per i nuovi progetti .NET Core poiché, quando gli strumenti verranno rilasciati, sarà disponibile una soluzione per convertire i progetti in MSBuild.
>
> Per altre informazioni, vedere il post [Changes to project.json](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/) (Modifiche a project.json) sul blog di .NET e l'argomento [Uso di MSBuild per creare progetti .NET Core](../tutorials/target-dotnetcore-with-msbuild.md).

## <a name="overview"></a>Panoramica

```
{
    "name": String,
    "version": String,
    "description": String,
    "copyright": String,
    "title": String,
    "entryPoint": String,
    "testRunner": String,
    "authors": String[],
    "language": String,
    "embedInteropTypes": Boolean,
    "preprocess": String or String[],
    "shared": String or String[],
    "dependencies": Object {
        version: String,
        type: String,
        target: String,
        include: String,
        exclude: String,
        suppressParent: String
    },
    "tools": Object,
    "scripts": Object,
    "buildOptions": Object {
        "define": String[],
        "nowarn": String[],
        "additionalArguments": String[],
        "warningsAsErrors": Boolean,
        "allowUnsafe": Boolean,
        "emitEntryPoint": Boolean,
        "optimize": Boolean,
        "platform": String,
        "languageVersion": String,
        "keyFile": String,
        "delaySign": Boolean,
        "publicSign": Boolean,
        "debugType": String,
        "xmlDoc": Boolean,
        "preserveCompilationContext": Boolean,
        "outputName": String,
        "compilerName": String,
        "compile": Object {
            "include": String or String[],
            "exclude": String or String[],
            "includeFiles": String or String[],
            "excludeFiles": String or String[],
            "builtIns": Object,
            "mappings": Object
        },
        "embed": Object {
            "include": String or String[],
            "exclude": String or String[],
            "includeFiles": String or String[],
            "excludeFiles": String or String[],
            "builtIns": Object,
            "mappings": Object
        },
        "copyToOutput": Object {
            "include": String or String[],
            "exclude": String or String[],
            "includeFiles": String or String[],
            "excludeFiles": String or String[],
            "builtIns": Object,
            "mappings": Object
        }
    },
    "publishOptions": Object {
        "include": String or String[],
        "exclude": String or String[],
        "includeFiles": String or String[],
        "excludeFiles": String or String[],
        "builtIns": Object,
        "mappings": Object
    },
    "runtimeOptions": Object {
        "configProperties": Object {
            "System.GC.Server": Boolean,
            "System.GC.Concurrent": Boolean,
            "System.GC.RetainVM": Boolean,
            "System.Threading.ThreadPool.MinThreads": Integer,
            "System.Threading.ThreadPool.MaxThreads": Integer
        },
        "framework": Object {
            "name": String,
            "version": String,
        },
        "applyPatches": Boolean
    },
    "packOptions": Object {
        "summary": String,
        "tags": String[],
        "owners": String[],
        "releaseNotes": String,
        "iconUrl": String,
        "projectUrl": String,
        "licenseUrl": String,
        "requireLicenseAcceptance": Boolean,
        "repository": Object {
            "type": String,
            "url": String
        },
        "files": Object {
            "include": String or String[],
            "exclude": String or String[],
            "includeFiles": String or String[],
            "excludeFiles": String or String[],
            "builtIns": Object,
            "mappings": Object
        }
    },
    "analyzerOptions": Object {
        "languageId": String
    },
    "configurations": Object,
    "frameworks": Object {
        "dependencies": Object {
            version: String,
            type: String,
            target: String,
            include: String,
            exclude: String,
            suppressParent: String
        },        
        "frameworkAssemblies": Object,
        "wrappedProject": String,
        "bin": Object {
            assembly: String
        }
    },
    "runtimes": Object,
    "userSecretsId": String
}
```

## <a name="name"></a>name
Tipo: String

Nome del progetto, usato per il nome dell'assembly e per quello del pacchetto. Se questa proprietà non è specificata, viene usato il nome della cartella di livello più alto.

Ad esempio:

```json
{
    "name": "MyLibrary"
}
```

## <a name="version"></a>version
Tipo: String

Versione [Semver](http://semver.org/spec/v1.0.0.html) del progetto, usata anche per il pacchetto NuGet.

Ad esempio:

```json
{
    "version": "1.0.0-*"
}
```

## <a name="description"></a>description
Tipo: String

Descrizione più estesa del progetto. Viene usata nelle proprietà dell'assembly.

Ad esempio:

```json
{
    "description": "This is my library and it's really great!"
}
```

## <a name="copyright"></a>copyright
Tipo: String

Informazioni sul copyright per il progetto. Viene usata nelle proprietà dell'assembly.

Ad esempio:

```json
{
    "copyright": "Fabrikam 2016"
}
```

## <a name="title"></a>title
Tipo: String

Nome descrittivo del progetto. Può contenere spazi e caratteri speciali non consentiti quando si usa la proprietà `name`. Viene usata nelle proprietà dell'assembly.

Ad esempio:

```json
{
    "title": "My Library"
}
```

## <a name="entrypoint"></a>entryPoint
Tipo: String

Metodo del punto di ingresso per il progetto. `Main` per impostazione predefinita.

Ad esempio:

```json
{
    "entryPoint": "ADifferentMethod"
}
```
    
## <a name="testrunner"></a>testRunner
Tipo: String

Nome del Test Runner, ad esempio [NUnit](http://nunit.org/) o [xUnit](http://xunit.github.io/), da usare con il progetto. Se si imposta questa proprietà, il progetto viene contrassegnato come progetto di test.

Ad esempio:

```json
{
    "testRunner": "NUnit"
}
```

## <a name="authors"></a>authors
Tipo: String[]

Matrice di stringhe con i nomi degli autori del progetto.

Ad esempio:

```json
{
    "authors": ["Anne", "Bob"]
}
```

## <a name="language"></a>language
Tipo: String

Lingua del progetto. Corrisponde all'argomento "neutral-language" del compilatore.

Ad esempio:

```json
{
    "language": "en-US"
}
```

## <a name="embedinteroptypes"></a>embedInteropTypes
Tipo: Boolean

`true` per incorporare i tipi di interoperabilità COM nell'assembly. In caso contrario, `false`. 

Ad esempio:

```json
{
    "embedInteropTypes": true
}
```

## <a name="preprocess"></a>preprocess
Tipo: String o String [] con modello di caratteri jolly

Specifica quali file sono inclusi nella pre-elaborazione.

Ad esempio:

```json
{
    "preprocess": "compiler/preprocess/**/*.cs"
}
```

## <a name="shared"></a>shared
Tipo: String o String [] con modello di caratteri jolly

Specifica quali file sono condivisi. Viene usata per l'esportazione della libreria.

Ad esempio:

```json
{
    "shared": "shared/**/*.cs"
}
```

## <a name="dependencies"></a>dependencies
Tipo: Object

Oggetto che definisce le dipendenze dei pacchetti del progetto. Ogni chiave di questo oggetto è il nome di un pacchetto e ogni valore contiene le informazioni sulla versione.
Per altre informazioni, vedere l'articolo [Dependency resolution](https://docs.nuget.org/ndocs/consume-packages/dependency-resolution#dependency-resolution-in-nuget-3-x) (Risoluzione delle dipendenze) sul sito della documentazione di NuGet.

Ad esempio:

```json
    "dependencies": {
        "System.Reflection.Metadata": "1.3.0",
        "Microsoft.Extensions.JsonParser.Sources": {
          "type": "build",
          "version": "1.0.0-rc2-20221"
        },
        "Microsoft.Extensions.HashCodeCombiner.Sources": {
          "type": "build",
          "version": "1.1.0-alpha1-21456"
        },
        "Microsoft.Extensions.DependencyModel": "1.0.0-*"
    }
```

### <a name="version"></a>version
Tipo: String

Versione o intervallo di versioni della dipendenza. Usare il carattere jolly \* per specificare una [versione di dipendenza mobile](https://docs.nuget.org/ndocs/consume-packages/dependency-resolution#floating-versions).

Ad esempio:

```json
"dependencies": { 
    "Newtonsoft.Json": { 
        "version": "9.0.1" 
    }
}
```

### <a name="type"></a>type
Tipo: String

Tipo della dipendenza. Può essere uno dei valori seguenti: `default`, `build` o `platform`. Il valore predefinito è `default`.

`build` è nota come dipendenza di sviluppo e viene usata solo per la fase di compilazione. Ciò significa che il pacchetto non deve essere pubblicato o aggiunto come dipendenza al file `.nupkg` di output. Ha lo stesso effetto dell'impostazione di [supressParent](#supressparent) su `all`.

`platform` fa riferimento all'SDK condiviso. Per altre informazioni, vedere la sezione in "Deploying a framework-dependent deployment with third-party dependencies" (Pubblicazione di una distribuzione dipendente dal framework con dipendenze di terze parti) dell'argomento [.NET Core application deployment](../deploying/index.md) (Distribuzione di applicazioni .NET Core).

Ad esempio:

```json
 "dependencies": {
   "Microsoft.NETCore.App": {
     "type": "platform",
     "version": "1.0.0"
   }
 }
```

### <a name="target"></a>target
Tipo: String

Limita la dipendenza in modo che corrisponda solo a un `project` o `package`.

### <a name="include"></a>include
Tipo: String

Include parti dei pacchetti con dipendenze. Può usare uno o più flag tra i seguenti: `all`, `runtime`, `compile`, `build`, `contentFiles`, `native`, `analyzers` o `none`.
Per definire più flag, delimitarli con virgole.
Per altre informazioni, vedere la specifica [Managing dependency package assets](https://github.com/NuGet/Home/wiki/%5BSpec%5D-Managing-dependency-package-assets) (Gestione delle risorse dei pacchetti con dipendenze) nel repository NuGet.

Ad esempio:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "runtime"
    }
  }
}
```

### <a name="exclude"></a>exclude
Tipo: String

Esclude parti dei pacchetti con dipendenze. Può essere uno o più flag tra i seguenti: `all`, `runtime`, `compile`, `build`, `contentFiles`, `native`, `analyzers` o `none`.
Per definire più flag, delimitarli con virgole.
Per altre informazioni, vedere la specifica [Managing dependency package assets](https://github.com/NuGet/Home/wiki/%5BSpec%5D-Managing-dependency-package-assets) (Gestione delle risorse dei pacchetti con dipendenze) nel repository NuGet.

Ad esempio:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles"
    }
  }
}
```

### <a name="supressparent"></a>supressParent
Tipo: String

Definisce esclusioni aggiuntive per gli utenti del progetto. Può essere uno dei flag seguenti: `all`, `runtime`, `compile`, `build`, `contentFiles`, `native`, `analyzers` o `none`.
Per altre informazioni, vedere la specifica [Managing dependency package assets](https://github.com/NuGet/Home/wiki/%5BSpec%5D-Managing-dependency-package-assets) (Gestione delle risorse dei pacchetti con dipendenze) nel repository NuGet.

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "suppressParent": "compile"
    }
  }
}
```

## <a name="tools"></a>tools
Tipo: Object

Oggetto che definisce le dipendenze dei pacchetti che vengono usate come strumenti per il progetto corrente, non come riferimenti. I pacchetti definiti in questo oggetto sono disponibili negli script eseguiti durante il processo di compilazione, ma non sono accessibili al codice nel progetto stesso. Tra gli strumenti possono essere inclusi i generatori di codice o gli strumenti di post-compilazione che eseguono attività correlate alla compressione.

Ad esempio:

```json
{
    "tools": {
    "MyObfuscator": "1.2.4"
    }
}
```

## <a name="scripts"></a>script
Tipo: Object

Oggetto che definisce gli script eseguiti durante il processo di compilazione. Ogni chiave di questo oggetto identifica il punto della compilazione in cui viene eseguito lo script. Ogni valore è una stringa con lo script da eseguire o una matrice di stringhe contenente gli script che verranno eseguiti nell'ordine specificato.
Sono supportati gli eventi seguenti:
* precompile
* postcompile
* prepublish
* postpublish

Ad esempio:

```json
{
    "scripts": {
        "precompile": "generateCode.cmd",
        "postcompile": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
    }
}
```

## <a name="buildoptions"></a>buildOptions
Tipo: Object

Oggetto in cui sono incluse le proprietà che controllano vari aspetti della compilazione. Le proprietà valide sono elencate di seguito. Può anche essere specificato in base al framework di destinazione, come descritto nella [sezione Framework](#frameworks).

Ad esempio:

```json
    "buildOptions": {
      "allowUnsafe": true,
      "emitEntryPoint": true
    }
```

### <a name="define"></a>define
Tipo: String[]

Elenco di definizioni, ad esempio "DEBUG" o "TRACE", che possono essere usate durante la compilazione condizionale nel codice.

Ad esempio:

```json
{
    "buildOptions": {
        "define": ["TEST", "OTHERCONDITION"]
    }
}
```

### <a name="nowarn"></a>nowarn
Tipo: String[]

Elenco di avvisi da ignorare.

Ad esempio:

```json
{
    "buildOptions": {
        "nowarn": ["CS0168", "CS0219"]
    }
}
```

Questo esempio consente di ignorare gli avvisi `The variable 'var' is assigned but its value is never used` e `The variable 'var' is assigned but its value is never used`

### <a name="additionalarguments"></a>additionalArguments
Tipo: String[]

Elenco di argomenti aggiuntivi che verranno passati al compilatore.

Ad esempio:

```json
{
    "buildOptions": {
        "additionalArguments": ["/parallel", "/nostdlib"]
    }
}
```

### <a name="warningsaserrors"></a>warningsAsErrors
Tipo: Boolean

`true` per considerare gli avvisi come errori. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "warningsAsErrors": true
    }
}
```

### <a name="allowunsafe"></a>allowUnsafe
Tipo: Boolean

`true` per consentire codice unsafe nel progetto. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "allowUnsafe": true
    }
}
```

### <a name="emitentrypoint"></a>emitEntryPoint
Tipo: Boolean

`true` per creare un file eseguibile. `false` per generare una libreria. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "emitEntryPoint": true
    }
}
```

### <a name="optimize"></a>optimize
Tipo: Boolean

`true` per consentire al compilatore di ottimizzare il codice nel progetto. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "optimize": true
    }
}
```

### <a name="platform"></a>platform
Tipo: String

Nome della piattaforma di destinazione, ad esempio AnyCpu, x86 o x64.

Ad esempio:

```json
{
    "buildOptions": {
        "platform": "x64"
    }
}
```

### <a name="languageversion"></a>languageVersion
Tipo: String

Versione del linguaggio usato dal compilatore: ISO-1, ISO-2, 3, 4, 5, 6 o Default.

Ad esempio:

```json
{
    "buildOptions": {
        "languageVersion": "5"
    }
}
```

### <a name="keyfile"></a>keyFile
Tipo: String

Percorso del file di chiave usato per firmare l'assembly.

Ad esempio:

```json
{
    "buildOptions": {
        "keyFile": "../keyfile.snk"
    }
}
```

### <a name="delaysign"></a>delaySign
Tipo: Boolean

`true` per ritardare la firma. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "delaySign": true
    }
}
```

### <a name="publicsign"></a>publicSign
Tipo: Boolean

`true` per abilitare la firma dell'assembly risultante. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "publicSign": true
    }
}
```

### <a name="debugtype"></a>debugType
Tipo: String

Indica il tipo di file di simboli (PDB) da generare. Le opzioni sono "portable" (per i progetti .NET Core) o "full" (i file PDB tradizionali solo per Windows).

Ad esempio:

```json
{
    "buildOptions": {
        "debugType": "portable"
    }
}
```

### <a name="xmldoc"></a>xmlDoc
Tipo: Boolean

`true` per generare la documentazione XML dai commenti con barra tripla nel codice sorgente. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "xmlDoc": true
    }
}
```

### <a name="preservecompilationcontext"></a>preserveCompilationContext
Tipo: Boolean

`true` per mantenere gli assembly di riferimento e altri dati di contesto per consentire la compilazione di runtime. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "buildOptions": {
        "preserveCompilationContext": true
    }
}
```

### <a name="outputname"></a>outputName
Tipo: String

Nome del file di output. 

Ad esempio:

```json
{
    "buildOptions": {
        "outputName": "MyApp"
    }
}
```

### <a name="compilername"></a>compilerName
Tipo: String

Nome del compilatore usato per il progetto. `csc` per impostazione predefinita. Sono attualmente supportati `csc` (compilatore C#) e `fsc` (compilatore F#).
 
Ad esempio:

```json
{
    "compilerName": "fsc"
}
```
    
### <a name="compile"></a>compile
Tipo: Object

Oggetto contenente le proprietà per la configurazione di compilazione.

#### <a name="include"></a>include
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da includere nella compilazione. La radice dei modelli corrisponde alla cartella del progetto. Il valore predefinito è none.

Ad esempio:

```json
{
    "include":["wwwroot", "Views"]
}
```

#### <a name="exclude"></a>exclude
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da escludere dalla compilazione. I modelli di esclusione hanno maggiore priorità rispetto a quelli di inclusione. Pertanto, un file presente in entrambi i modelli verrà escluso. La radice dei modelli corrisponde alla cartella del progetto. Il valore predefinito è none.

Ad esempio:

```json
{
    "exclude": ["bin/**", "obj/**"]
}
```

#### <a name="includefiles"></a>includeFiles

Tipo: String o String [] con modello di caratteri jolly.

Elenco di percorsi di file da includere. La radice dei percorsi corrisponde alla cartella del progetto. Questo elenco ha maggiore priorità rispetto ai modelli di inclusione ed esclusione con caratteri jolly. Pertanto, un file presente sia in questo elenco sia nel modello di esclusione verrà comunque incluso. Il valore predefinito è none.

Ad esempio:

```json
{
    "includeFiles": []
}
```

#### <a name="excludefiles"></a>excludeFiles

Tipo: String o String [] con modello di caratteri jolly.

Elenco di percorsi di file da escludere. La radice dei percorsi corrisponde alla cartella del progetto. Questo elenco ha maggiore priorità rispetto ai modelli con caratteri jolly e ai percorsi di inclusione. Pertanto, un file presente in tutti verrà escluso. Il valore predefinito è none.

Ad esempio:

```json
{
    "excludeFiles":[],
}
```

#### <a name="builtins"></a>builtIns

Tipo: Object

Impostazioni predefinite del sistema. Può avere modelli di tipo `include` e `exclude` con caratteri jolly, uniti ai valori corrispondenti delle proprietà `include` e `exclude`.

Ad esempio:

```json
{
    "builtIns":{}
}
```

#### <a name="mappings"></a>mappings
Tipo: Object

Le chiavi dell'oggetto rappresentano i percorsi di destinazione nel layout di output.

I valori sono una stringa o un oggetto che rappresenta il percorso di origine dei file da includere.  La rappresentazione dell'oggetto può avere specifiche sezioni `include`, `exclude`, `includeFiles` e `excludeFiles`.

Esempio di stringa:

```json
{
    "mappings": {
        "dest/path": "./src/path"
    }
}
```

Esempio di oggetto:

```json
{
    "mappings": {
        "dest/path":{
            "include":"./src/path"
        }
    }
}
```

### <a name="embed"></a>embed
Tipo: Object

Oggetto contenente le proprietà per la configurazione di compilazione.

#### <a name="include"></a>include
Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "include":["wwwroot", "Views"]
}
```

#### <a name="exclude"></a>exclude
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da escludere dalla compilazione.

Ad esempio:

```json
{
    "exclude": ["bin/**", "obj/**"]
}
```

#### <a name="includefiles"></a>includeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "includeFiles":[],
}
```

#### <a name="excludefiles"></a>excludeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "excludeFiles":[],
}
```

#### <a name="builtins"></a>builtIns
Tipo: Object

```json
{
    "builtIns":{}
}
```

#### <a name="mappings"></a>mappings
Tipo: Object

Le chiavi dell'oggetto rappresentano i percorsi di destinazione nel layout di output.

I valori sono una stringa o un oggetto che rappresenta il percorso di origine dei file da includere.  La rappresentazione dell'oggetto può avere specifiche sezioni `include`, `exclude`, `includeFiles` e `excludeFiles`.

Esempio di stringa:

```json
{
    "mappings": {
        "dest/path": "./src/path"
    }
}
```

Esempio di oggetto:

```json
{
    "mappings": {
        "dest/path":{
            "include":"./src/path"
        }
    }
}
```

### <a name="copytooutput"></a>copyToOutput
Tipo: Object

Oggetto contenente le proprietà per la configurazione di compilazione.

#### <a name="include"></a>include
Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "include":["wwwroot", "Views"]
}
```

#### <a name="exclude"></a>exclude
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da escludere dalla compilazione.

Ad esempio:

```json
{
    "exclude": ["bin/**", "obj/**"]
}
```

#### <a name="includefiles"></a>includeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "includeFiles":[],
}
```

#### <a name="excludefiles"></a>excludeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "excludeFiles":[],
}
```

#### <a name="builtins"></a>builtIns
Tipo: Object

```json
{
    "builtIns":{}
}
```

#### <a name="mappings"></a>mappings
Tipo: Object

Le chiavi dell'oggetto rappresentano i percorsi di destinazione nel layout di output.

I valori sono una stringa o un oggetto che rappresenta il percorso di origine dei file da includere.  La rappresentazione dell'oggetto può avere specifiche sezioni `include`, `exclude`, `includeFiles` e `excludeFiles`.

Esempio di stringa:

```json
{
    "mappings": {
        "dest/path": "./src/path"
    }
}
```

Esempio di oggetto:

```json
{
    "mappings": {
        "dest/path":{
            "include":"./src/path"
        }
    }
}
```

## <a name="publishoptions"></a>publishOptions
Tipo: Object

Oggetto contenente le proprietà per la configurazione di compilazione.

### <a name="include"></a>include
Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "include":["wwwroot", "Views"]
}
```

### <a name="exclude"></a>exclude
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da escludere dalla compilazione.

Ad esempio:

```json
{
    "exclude": ["bin/**", "obj/**"]
}
```

### <a name="includefiles"></a>includeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "includeFiles":[],
}
```

### <a name="excludefiles"></a>excludeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "excludeFiles":[],
}
```

### <a name="builtins"></a>builtIns
Tipo: Object

```json
{
    "builtIns":{}
}
```

### <a name="mappings"></a>mappings
Tipo: Object

Le chiavi dell'oggetto rappresentano i percorsi di destinazione nel layout di output.

I valori sono una stringa o un oggetto che rappresenta il percorso di origine dei file da includere.  La rappresentazione dell'oggetto può avere specifiche sezioni `include`, `exclude`, `includeFiles` e `excludeFiles`.

Esempio di stringa:

```json
{
    "mappings": {
        "dest/file": "./src/file",
        "dest/folder/": "./src/folder/**/*"
    }
}
```

Esempio di oggetto:

```json
{
    "mappings": {
        "dest/file":{
            "include":"./src/file"
        },
        "dest/folder/":{
            "include":"./src/folder/**/*"
        }
    }
}
```

## <a name="runtimeoptions"></a>runtimeOptions
Tipo: Object

Specifica i parametri da passare al runtime durante l'inizializzazione.

### <a name="configproperties"></a>configProperties
Tipo: Object

Contiene le proprietà di configurazione per il runtime e il framework.

#### <a name="systemgcserver"></a>System.GC.Server
Tipo: Boolean

`true` per abilitare la procedura di Garbage Collection del server. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "runtimeOptions": {
        "configProperties": {
            "System.GC.Server": true
        }
    }
}
```

#### <a name="systemgcconcurrent"></a>System.GC.Concurrent
Tipo: Boolean

`true` per abilitare la procedura simultanea di Garbage Collection. In caso contrario, `false`. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "runtimeOptions": {
        "configProperties": {
            "System.GC.Concurrent": true
        }
    }
}
```

#### <a name="systemgcretainvm"></a>System.GC.RetainVM
Tipo: Boolean

`true` per inserire i segmenti da eliminare in un elenco di standby per un uso futuro anziché rilasciarli nuovamente al sistema operativo (OS). In caso contrario, `false`.
Il valore predefinito è `false`.

Ad esempio:

```json
{
    "runtimeOptions": {
        "configProperties": {
            "System.GC.RetainVM": true
        }
    }
}
```

#### <a name="systemthreadingthreadpoolminthreads"></a>System.Threading.ThreadPool.MinThreads
Tipo: Integer

Esegue l'override del numero minimo di thread per il pool di lavoro ThreadPool.

```json
{
    "runtimeOptions": {
        "configProperties": {
            "System.Threading.ThreadPool.MinThreads": 4
        }
    }
}
```

#### <a name="systemthreadingthreadpoolmaxthreads"></a>System.Threading.ThreadPool.MaxThreads
Tipo: Integer

Esegue l'override del numero massimo di thread per il pool di lavoro ThreadPool.

```json
{
    "runtimeOptions": {
        "configProperties": {
            "System.Threading.ThreadPool.MaxThreads": 25
        }
    }
}
```

### <a name="framework"></a>framework
Tipo: Object

Contiene le proprietà del framework condiviso da usare durante l'attivazione dell'applicazione. La presenza di questa sezione indica che si tratta di un'applicazione portabile, progettata per l'uso di un framework ridistribuibile condiviso.

#### <a name="name"></a>name
Tipo: String

Nome del framework condiviso.

```json
{
    "runtimeOptions": {
        "framework": {
            "name": "Microsoft.DotNetCore"
        }
    }
}
```

#### <a name="version"></a>version
Tipo: String

Versione del framework condiviso.

```json
{
    "runtimeOptions": {
        "framework": {
            "version": "1.0.1"
        }
    }
}
```

### <a name="applypatches"></a>applyPatches
Tipo: Boolean

`true` per usare il framework con la stessa versione o con una versione successiva che differisce solo per il campo patch `SemVer`. `false` per consentire all'host di usare solo la versione esatta del framework. Il valore predefinito è `true`.

```json
{
    "runtimeOptions": {
        "applyPatches": false
    }
}
```

## <a name="packoptions"></a>packOptions
Tipo: Object

Definisce le opzioni relative alla creazione di un pacchetto NuGet per l'output del progetto.

### <a name="summary"></a>summary
Tipo: String

Breve descrizione del progetto.

Ad esempio:

```json
{
    "packOptions": {
        "summary": "This is my library."
    }
}
```

### <a name="tags"></a>tag
Tipo: String[]

Matrice di stringhe con tag per il progetto, usata per la ricerca in NuGet.

Ad esempio:

```json
{
    "packOptions": {
        "tags": ["hyperscale", "cats"]
    }
}
```

### <a name="owners"></a>owners
Tipo: String[]

Matrice di stringhe con i nomi dei proprietari del progetto.

Ad esempio:

```json
{
    "packOptions": {
        "owners": ["Fabrikam", "Microsoft"]
    }
}
```

### <a name="releasenotes"></a>releaseNotes
Tipo: String

Note sulla versione per il progetto.

Ad esempio:

```json
{
    "packOptions": {
        "releaseNotes": "Initial version, implemented flimflams."
    }
}
```

### <a name="iconurl"></a>iconUrl
Tipo: String

URL relativo a un'icona che verrà usata in varie posizioni, ad esempio in Package Explorer.

Ad esempio:

```json
{
    "packOptions": {
        "iconUrl": "http://www.mylibrary.gov/favicon.ico"
    }
}
```

### <a name="projecturl"></a>projectUrl
Tipo: String

URL relativo alla home page del progetto.

Ad esempio:

```json
{
    "packOptions": {
        "projectUrl": "http://www.mylibrary.gov"
    }
}
```

### <a name="licenseurl"></a>licenseUrl
Tipo: String

URL relativo alla licenza usata dal progetto.

Ad esempio:

```json
{
    "packOptions": {
        "licenseUrl": "http://www.mylibrary.gov/licence"
    }
}
```

### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Tipo: Boolean

`true` per accettare automaticamente la licenza di pacchetto durante l'installazione del pacchetto da visualizzare. In caso contrario, `false`. Questa proprietà viene usata solo per i pacchetti NuGet e viene ignorata in altri casi. Il valore predefinito è `false`.

Ad esempio:

```json
{
    "packOptions": {
        "requireLicenseAcceptance": true
    }
}
```
   
### <a name="repository"></a>repository
Tipo: Object

Contiene informazioni sul repository in cui è archiviato il progetto.

#### <a name="type"></a>type
Tipo: String

Tipo del repository. Il valore predefinito è "git".

Ad esempio:

```json
{
    "packOptions": {
        "repository": {
            "type": "git"
        }
    }
}
```

#### <a name="url"></a>url
Tipo: String

URL del repository in cui è archiviato il progetto.

Ad esempio:

```json
{
    "packOptions": {
        "repository": {
            "url": "http://github.com/dotnet/corefx"
        }
    }
}
```

### <a name="files"></a>file
Tipo: Object

#### <a name="include"></a>include
Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "include":["wwwroot", "Views"]
}
```

#### <a name="exclude"></a>exclude
Tipo: String o String [] con modello di caratteri jolly.

Specifica i file da escludere dalla compilazione.

Ad esempio:

```json
{
    "exclude": ["bin/**", "obj/**"]
}
```

#### <a name="includefiles"></a>includeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "includeFiles":[]
}
```

#### <a name="excludefiles"></a>excludeFiles

Tipo: String o String [] con modello di caratteri jolly.

```json
{
    "excludeFiles":[]
}
```

#### <a name="builtins"></a>builtIns
Tipo: Object

```json
{
    "builtIns":{}
}
```

#### <a name="mappings"></a>mappings
Tipo: Object

Le chiavi dell'oggetto rappresentano i percorsi di destinazione nel layout di output.

I valori sono una stringa o un oggetto che rappresenta il percorso di origine dei file da includere.  La rappresentazione dell'oggetto può avere specifiche sezioni `include`, `exclude`, `includeFiles` e `excludeFiles`. 

Esempio di stringa:

```json
{
    "mappings": {
        "dest/path": "./src/path"
    }
}
```

Esempio di oggetto:

```json
{
    "mappings": {
        "dest/path":{
            "include":"./src/path"
        }
    }
}
```

## <a name="analyzeroptions"></a>analyzerOptions
Tipo: Object

Oggetto con le proprietà usate dagli analizzatori di codice.

Ad esempio:

```json
{
    "analyzerOptions": { }
}
```

### <a name="languageid"></a>languageId
Tipo: String

ID del linguaggio da analizzare. "cs" rappresenta C#, "vb" rappresenta Visual Basic e "fs" rappresenta F#.

Ad esempio:

```json
"analyzerOptions": {
    "languageId": "vb"
}
```

## <a name="configurations"></a>configurations
Tipo: Object

Oggetto le cui proprietà definiscono diverse configurazioni per il progetto, ad esempio Debug e Release. Ogni valore è un oggetto che può contenere un oggetto `buildOptions` con le opzioni specifiche per la configurazione.

Ad esempio:

```json
"configurations": {
    "Release": {
        "buildOptions": {
            "allowUnsafe": false
        }
    }
}
```

## <a name="frameworks"></a>frameworks
Tipo: Object

Specifica i framework supportati dal progetto, ad esempio .NET Framework o Universal Windows Platform (UWP). Deve essere un Target Framework Moniker (TFM) valido. Ogni valore è un oggetto che può contenere informazioni specifiche del framework, ad esempio `buildOptions`, `analyzerOptions`, `dependencies` e le proprietà descritte nelle sezioni seguenti.

Ad esempio:

```json
"frameworks": {
    "netcoreapp1.0": {
        "buildOptions": {
            "define": ["FOO", "BIZ"]
        }
    }
}
```

### <a name="dependencies"></a>dependencies
Tipo: Object

Dipendenze specifiche del framework. Questa impostazione è utile quando non è possibile specificare semplicemente una dipendenza a livello di pacchetto fra tutte le destinazioni. Questo problema può verificarsi, ad esempio, perché una destinazione è priva del supporto incorporato che hanno altre destinazioni oppure richiede una diversa versione di una dipendenza rispetto ad altre destinazioni. Per visualizzare un elenco delle proprietà per questo nodo, vedere la precedente sezione [dependencies](#dependencies).

Ad esempio:

```json
    "frameworks": {
        "netstandard1.5": {
        "dependencies": {
            "Microsoft.Extensions.JsonParser.Sources": "1.0.0-rc2-20221"
        }
    }
}
```

### <a name="frameworkassemblies"></a>frameworkAssemblies
Tipo: Object

Oggetto simile alle dipendenze, ma che contiene riferimenti ad assembly nella Global Assembly Cache che non sono pacchetti NuGet. È anche possibile specificare la versione da usare e il tipo di dipendenza. Questo oggetto viene usato quando si definiscono .NET Framework e la libreria di classi portabile come destinazioni. È possibile creare un progetto con questa impostazione solo in Windows.

Ad esempio:

```json
"frameworks": {
    "net451": {
        "frameworkAssemblies": {
            "System.Runtime": {
                "type": "build",
                "version": "4.0.0"
            }
        }
    }
}
```

### <a name="wrappedproject"></a>wrappedProject
Tipo: String

Specifica la posizione del progetto con dipendenze. 

Ad esempio:

```json
"frameworks": {
    "net451": {
        "wrappedProject": "MyProject.csproj"
    }
}
```

### <a name="bin"></a>bin
Tipo: Object

Oggetto usato per eseguire il wrapping di un file DLL. È possibile fare riferimento a un pacchetto contenente questa DLL e generarlo. 

Contiene una singola proprietà di tipo String, `assembly`, il cui valore corrisponde al percorso dell'assembly.   

Ad esempio:

```json
"frameworks": {
    "netcoreapp1.0": {
        "bin": {
            "assembly": "c:/otherProject/otherdll.dll"
        }
    }
}
```

## <a name="runtimes"></a>runtimes
Tipo: Object

Elenco di [identificatori di runtime (RID)](../rid-catalog.md) supportati dal progetto (usato per la pubblicazione di [distribuzioni autonome](../deploying/index.md#self-contained-deployments-scd)).

Ad esempio:

```json
"runtimes": {
    "win7-x64": {},
    "win8-x64": {},
    "win81-x64": {},
    "win10-x64": {},
    "osx.10.11-x64": {},
    "ubuntu.16.04-x64": {}
}
```

## <a name="usersecretsid"></a>userSecretsId
Tipo: String

Specifica un identificatore di segreto utente da usare in fase di sviluppo. Per altre informazioni, vedere [Safe storage of app secrets during development](https://docs.asp.net/en/latest/security/app-secrets.html) (Archiviazione sicura dei segreti dell'app durante lo sviluppo).

Ad esempio:

```json
{
    "userSecretsId": "aspnet-WebApp1-c23d27a4-eb88-4b18-9b77-2a93f3b15119"
}
```



<!--HONumber=Nov16_HO3-->


