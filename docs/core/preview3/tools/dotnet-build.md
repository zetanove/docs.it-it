---
title: Comando dotnet-build | .NET Core SDK
description: Il comando dotnet-build consente di compilare un progetto e tutte le relative dipendenze.
keywords: dotnet-build, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: mairaw
manager: wpickett
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 70285a83-4103-4617-be8b-d0e1e9a4a91d
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 04c4d77b31bf4a1bdb425d837c490440e7312e57

---

#<a name="dotnet-build"></a>dotnet-build

## <a name="name"></a>Nome 
dotnet-build: consente di compilare un progetto e tutte le relative dipendenze 

## <a name="synopsis"></a>Riepilogo

`dotnet build [--help] [--output]  [--framework]  
    [--configuration]  [--runtime] [--version-suffix]
    [--build-profile]  [--no-incremental] [--no-dependencies]
    [<project>]`

## <a name="description"></a>Descrizione

Il comando `dotnet build` consente di compilare più file di origine da un progetto di origine e le relative dipendenze in un file binario. Per impostazione predefinita, il file binario risultante è scritto in linguaggio intermedio (IL, Intermediate Language) e ha l'estensione DLL. 
`dotnet build` rilascia inoltre un file `\*.deps` che descrive gli elementi necessari all'host per eseguire l'applicazione.  

Per la compilazione è necessario un file di asset (un file che elenca tutte le dipendenze dell'applicazione). È quindi necessario eseguire [`dotnet restore`](dotnet-restore.md) prima della compilazione del codice.

Prima che inizi la compilazione, il verbo `build` analizza il progetto e le relative dipendenze per i controlli incrementali di sicurezza.
Se vengono superati tutti i controlli, viene eseguita la compilazione incrementale del progetto e delle relative dipendenze. In caso contrario, viene usata la compilazione non incrementale. Tramite un flag del profilo, gli utenti possono scegliere di ricevere altre informazioni su come migliorare i tempi di compilazione.

Per compilare un'applicazione eseguibile anziché una raccolta, è necessario impostare la proprietà `<OutputType>`:

```xml
<PropertyGroup>
    <OutputType>Exe</OutputType>
</PropertyGroup>
```

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui inserire i file binari compilati. È necessario definire anche `--framework` quando si specifica questa opzione.

`-f|--framework <FRAMEWORK>`

Esegue la compilazione per un framework specifico. Il framework deve essere definito nel [file di progetto](csproj.md).

`-c|--configuration [Debug|Release]`

Definisce una configurazione in cui eseguire la compilazione.  Se omessa, il valore predefinito è `Debug`.

`-r|--runtime [RUNTIME_IDENTIFIER]`

Runtime di destinazione per cui eseguire la compilazione. Per un elenco degli identificatori di runtime (RID, Runtime Identifier) che è possibile usare, vedere il [catalogo RID](../../rid-catalog.md). 

`--version-suffix [VERSION_SUFFIX]`

Definisce l'elemento che deve sostituire `*` nel campo relativo alla versione del file di progetto. Il formato rispetta le linee guida della versione NuGet. 

`--build-profile`

Stampa i controlli incrementali di sicurezza che gli utenti devono eseguire affinché la compilazione incrementale venga attivata automaticamente.

`--no-incremental`

Contrassegna la compilazione come non sicura per la compilazione incrementale. Disattiva la compilazione incrementale e impone una ricompilazione pulita del grafico delle dipendenze del progetto.

`--no-dependencies`

Ignora i riferimenti da progetto a progetto e compila solo il progetto radice specificato per la compilazione.

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet build`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet build --configuration Release`

Compilare un progetto e le relative dipendenze per un runtime specifico ( in questo esempio, Ubuntu 16.04):

`dotnet build --runtime ubuntu.16.04-x64`



<!--HONumber=Nov16_HO3-->


