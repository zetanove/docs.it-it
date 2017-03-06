---
title: Uso di MSBuild per creare progetti .NET Core
description: Uso di MSBuild per creare progetti .NET Core
keywords: .NET, .NET Core
author: dsplaisted
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 13c66464-4f14-4db6-aa8b-06f25e7ba894
translationtype: Human Translation
ms.sourcegitcommit: 098cb31bb79e47ebb2ad2e8c2f56d2d5d6da4079
ms.openlocfilehash: 6a992d985948a22da58db8317bc04d2f1828fc05
ms.lasthandoff: 01/18/2017

---

# <a name="using-msbuild-to-build-net-core-projects"></a>Uso di MSBuild per creare progetti .NET Core

Gli strumenti di .NET Core passeranno presto [da progetti basati su project.json a progetti basati su MSBuild](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/).
Si prevede che la prima versione degli strumenti di .NET Core che usano MSBuild venga distribuita insieme alla prossima versione di Visual Studio.  È tuttavia possibile usare MSBuild per i progetti .NET Core anche oggi, come verrà illustrato in questa pagina.

Per i nuovi progetti con destinazione .NET Core, è consigliabile usare gli strumenti predefiniti con *project.json* per i motivi seguenti:

- MSBuild non supporta ancora molte delle funzionalità di *project.json*.
- Molti degli strumenti basati su ASP.NET non sono attualmente compatibili con i progetti MSBuild.
- Al momento del rilascio degli strumenti .NET Core basati su MSBuild, *project.json* verrà convertito automaticamente per MSBuild.

Prendere in considerazione l'uso di MSBuild nei casi seguenti:

 - Trasferimento di progetti esistenti che usano MSBuild a .NET Core.
 - Progetti che usano l'estendibilità di MSBuild e non sono ben supportati da *project.json*.

## <a name="prerequisites"></a>Prerequisiti

- [Visual Studio 2015 Update 3](https://www.visualstudio.com/en-us/news/releasenotes/vs2015-update3-vs) o versione successiva
- [Strumenti .NET Core per Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs)
- Estensione NuGet di Visual Studio [3.5.0 -beta](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) o versione successiva

## <a name="creating-a-library-targeting-net-core"></a>Creazione di una libreria con destinazione .NET Core

1. Nella barra dei menu di Visual Studio scegliere **File** | **Nuovo** | **Progetto** e quindi selezionare **Libreria di classi (portabile)**.

  ![Nuovo progetto](./media/target-dotnetcore-with-msbuild/new-project-dialog-class-library-portable.png)

2. Scegliere un nome e un percorso per il progetto e fare clic su **OK**.

3. Verrà visualizzata la finestra di dialogo "Aggiungi cartella libreria di classi portabile".  Selezionare **.NET Framework 4.6** e **ASP.NET Core 1.0** come destinazioni e fare clic su **OK**

  ![Finestra di dialogo delle destinazioni portabili](./media/target-dotnetcore-with-msbuild/pcl-targets-dialog-net46-aspnetcore10.png)

4. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà**.
5. Nella scheda **Libreria** delle proprietà del progetto fare clic sul collegamento **Imposta come destinazione la piattaforma standard .NET** e quindi fare clic su **Sì** nella finestra di dialogo visualizzata.
6. Aprire il file `project.json` nel progetto e apportare le modifiche seguenti:
    - Modificare il numero di versione del pacchetto `NETStandard.Library` in `1.6.0` (ossia la versione per .NET Core 1.0 del pacchetto).
    - Aggiungere la definizione `imports` seguente all'interno della definizione del framework `netstandard1.6`.  In questo modo, il progetto può fare riferimento a pacchetti NuGet compatibili con .NET Core che non sono stati aggiornati per l'uso di .NET Standard come destinazione.

        ```json
        "netstandard1.6": {
            "imports": [ "dnxcore50", "portable-net452" ]
        }
        ```

## <a name="creating-a-net-core-console-application"></a>Creazione di un'applicazione console .NET Core
La creazione di un'applicazione console per .NET Core richiede alcune personalizzazioni del processo di compilazione di MSBuild.  È possibile trovare un progetto di esempio di un'applicazione console .NET Core chiamata [CoreApp](https://github.com/dotnet/corefxlab/tree/master/samples/NetCoreSample/CoreApp) nel repository [corefxlab](https://github.com/dotnet/corefxlab).  Un'altra opzione valida consiste nell'iniziare con [coretemplate](https://github.com/mellinoe/coretemplate), che usa file di destinazioni MSBuild separati per definire .NET Core come destinazione anziché inserire le modifiche direttamente nel file di progetto.  

Per iniziare è inoltre possibile creare un progetto in Visual Studio e modificarlo definendo .NET Core come destinazione.  Le istruzioni seguenti mostrano i passaggi minimi da seguire.  A differenza di [CoreApp](https://github.com/dotnet/corefxlab/tree/master/samples/NetCoreSample/CoreApp) o [coretemplate](https://github.com/mellinoe/coretemplate), un progetto creato in questo modo non includerà le configurazioni per la definizione di Linux e macOS come destinazioni.

1. Nella barra dei menu di Visual Studio scegliere **File** | **Nuovo** | **Progetto** e quindi selezionare **Applicazione console**.
2. Scegliere un nome e un percorso per il progetto e fare clic su **OK**.
3. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, scegliere **Proprietà** e quindi aprire la scheda **Compilazione**.
4. Dall'elenco a discesa **Configurazione** (nella parte superiore della pagina delle proprietà) selezionare **Tutte le configurazioni** e quindi impostare **Piattaforma di destinazione** su **x64**.
5. Eliminare il file `app.config` dal progetto.
6. Aggiungere un file `project.json` nel progetto con il contenuto seguente:

    ```json
    {
        "dependencies": {
            "Microsoft.NETCore.App": "1.0.0-rc2-3002702"
        },
        "runtimes": {
            "win7-x64": { },
            "ubuntu.14.04-x64": { },
            "osx.10.10-x64": { }
        },
        "frameworks": {
            "netcoreapp1.0": {
                "imports": [ "dnxcore50", "portable-net452" ]
            }
        }
    }
    ```

7. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Scarica progetto**, quindi fare nuovamente clic con il pulsante destro del mouse e scegliere **Modifica _MyProj.csproj_** e infine apportare le modifiche seguenti:
    - Rimuovere tutti gli elementi `Reference` predefiniti (a `System`, `System.Core` e così via).
    - Aggiungere le proprietà seguenti al primo `PropertyGroup` nel progetto:

        ```xml
        <TargetFrameworkIdentifier>.NETCoreApp</TargetFrameworkIdentifier>
        <TargetFrameworkVersion>v1.0</TargetFrameworkVersion>
        <BaseNuGetRuntimeIdentifier>win7</BaseNuGetRuntimeIdentifier>
        <NoStdLib>true</NoStdLib>
        <NoWarn>$(NoWarn);1701</NoWarn>
        ```

    - Aggiungere il codice seguente alla fine del file (dopo l'importazione di `Microsoft.CSharp.Targets`):

        ```xml
        <PropertyGroup>
            <!-- We don't use any of MSBuild's resolution logic for resolving the framework, so just set these two
                    properties to any folder that exists to skip the GetReferenceAssemblyPaths task (not target) and
                    to prevent it from outputting a warning (MSB3644).
                -->
            <_TargetFrameworkDirectories>$(MSBuildThisFileDirectory)</_TargetFrameworkDirectories>
            <_FullFrameworkReferenceAssemblyPaths>$(MSBuildThisFileDirectory)</_FullFrameworkReferenceAssemblyPaths>

            <!-- MSBuild thinks all EXEs need binding redirects, not so for CoreCLR! -->
            <AutoUnifyAssemblyReferences>true</AutoUnifyAssemblyReferences>
            <AutoGenerateBindingRedirects>false</AutoGenerateBindingRedirects>

            <!-- Set up debug options to run with host, and to use the CoreCLR debug engine -->
            <StartAction>Program</StartAction>
            <StartProgram>$(TargetDir)dotnet.exe</StartProgram>
            <StartArguments>$(TargetPath)</StartArguments>
            <DebugEngines>{2E36F1D4-B23C-435D-AB41-18E608940038}</DebugEngines>
        </PropertyGroup>
        ```

    - Chiudere il file con estensione csproj e ricaricare il progetto in Visual Studio.

8. A questo punto dovrebbe essere possibile eseguire il programma premendo F5 in Visual Studio o dalla riga di comando nella cartella di output con`dotnet MyApp.exe` 

