---
title: Comando dotnet-build | Microsoft Docs
description: Il comando dotnet-build consente di compilare un progetto e tutte le relative dipendenze.
keywords: dotnet-build, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e1a2bc4-a919-4a86-8f33-a9b218b1fcb3
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: d2eeeccd6b3bdf82ba02fea6ce89785ef19d4116

---

#<a name="dotnet-build-tooling-preview-4"></a>dotnet-build (strumenti dell'anteprima 4)

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 4 di .NET Core (Visual Studio 2017 RC). Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [dotnet-build](../../tools/dotnet-build.md).

## <a name="name"></a>Nome 
dotnet-build: consente di compilare un progetto e tutte le relative dipendenze 

## <a name="synopsis"></a>Riepilogo

`dotnet build [--help] [--output]  [--framework]  
    [--configuration]  [--runtime] [--version-suffix]
    [--build-profile]  [--no-incremental] [--no-dependencies]
    [<project>]`

## <a name="description"></a>Descrizione

Il comando `dotnet build` consente di compilare più file di origine da un progetto di origine e le relative dipendenze in un file binario. Per impostazione predefinita, il file binario risultante è scritto in linguaggio intermedio (IL, Intermediate Language) e ha l'estensione DLL. 
`dotnet build` rilascia inoltre un file `*.deps` che descrive gli elementi necessari all'host per eseguire l'applicazione.  

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



<!--HONumber=Jan17_HO3-->


