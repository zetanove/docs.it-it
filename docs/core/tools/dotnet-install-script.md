---
title: script dotnet-install | Microsoft Docs
description: Informazioni sugli script dotnet-install per l&quot;installazione degli strumenti dell&quot;interfaccia della riga di comando di .NET Core e del runtime condiviso.
keywords: dotnet-install, script dotnet-install, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: b64e7e6f-ffb4-4fc8-b43b-5731c89479c2
translationtype: Human Translation
ms.sourcegitcommit: 4a1f0c88fb1ccd6694f8d4f5687431646adbe000
ms.openlocfilehash: fbc1ce8d864a5c2150c61f4b8bf7cb8544921634
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-install-scripts-reference"></a>Riferimento agli script dotnet-install

## <a name="name"></a>Nome

`dotnet-install.ps1` | `dotnet-install.sh`: script usato per l'installazione degli strumenti dell'interfaccia della riga di comando e del runtime condiviso di .NET Core.

## <a name="synopsis"></a>Riepilogo

Windows:

`dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture] [-SharedRuntime] [-DebugSymbols] [-DryRun] [-NoPath] [-AzureFeed] [-ProxyAddress]`

macOS/Linux:

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]`

## <a name="description"></a>Descrizione

Gli script `dotnet-install` vengono usati per eseguire un'installazione senza privilegi di amministratore della toolchain dell'interfaccia della riga di comando e del runtime condiviso. È possibile scaricare gli script dal [repository di GitHub dell'interfaccia della riga di comando](https://github.com/dotnet/cli/tree/rel/1.0.0/scripts/obtain). 

Gli script vengono usati principalmente negli scenari di automazione e nelle installazioni senza privilegi di amministratore. Sono disponibili due script, uno per PowerShell, che funziona in Windows, e uno script Bash, che funziona in Linux o in OS X. I due script presentano lo stesso comportamento. Lo script Bash legge anche le opzioni PowerShell, che possono quindi essere usate con lo script in sistemi Linux/OS X. 

Gli script di installazione scaricano il file ZIP/tarball da destinazioni di compilazione dell'interfaccia della riga di comando e lo installano nel percorso predefinito o in un percorso specificato da `-InstallDir|--install-dir`. Per impostazione predefinita, lo script di installazione scarica e installa l'SDK. Se si vuole ottenere solo il runtime condiviso, è possibile specificare l'argomento `--shared-runtime`. 

Per impostazione predefinita, lo script aggiunge il percorso di installazione a $PATH per la sessione corrente. Eseguire l'override di questo comportamento predefinito specificando l'argomento `--no-path`. 

Prima di eseguire lo script, installare le [dipendenze](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md) necessarie.

È possibile installare una versione specifica usando l'argomento `--version`. La versione deve essere specificata con un numero a tre parti (ad esempio, 1.0.0-13232). Se omessa, per impostazione predefinita viene usato il primo file [global.json](global-json.md) della gerarchia al di sopra della cartella in cui è stato richiamato lo script contenente la proprietà `version`. Se non è presente, verrà usata l'ultima versione.

È anche possibile usare questo script per ottenere l'SDK o i file binari di debug del runtime condiviso insieme ai simboli di debug usando l'argomento `--debug`. Se non si esegue questa operazione durante la prima installazione e ci si rende conto in un secondo momento che sono necessari i simboli di debug, è possibile ottenerli eseguendo nuovamente lo script con l'argomento `--debug` e la versione dell'SDK installata. 

## <a name="options"></a>Opzioni

Nota: le opzioni variano a seconda delle implementazioni degli script. 

### <a name="powershell-windows"></a>PowerShell (Windows)

`-Channel <CHANNEL>`

Specifica il canale di origine per l'installazione. I valori sono `future`, `preview` e `production`. Il valore predefinito è `production`.

`-Version <VERSION>`

Specifica la versione dell'interfaccia della riga di comando da installare. La versione deve essere specificata con un numero a tre parti (ad esempio, 1.0.0-13232). Se omessa, per impostazione predefinita viene usato il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usata l'ultima versione.

`-InstallDir <DIRECTORY>`

Specifica il percorso di installazione. Se la directory non esiste, verrà creata. Il valore predefinito è *%LocalAppData%\.dotnet*.

`-Architecture <ARCHITECTURE>`

Architettura dei file binari di .NET Core da installare. I valori possibili sono `auto`, `x64` e `x86`. Il valore predefinito è `auto`, che rappresenta l'architettura del sistema operativo attualmente in esecuzione.

`-SharedRuntime`

Se impostata, questa opzione limita l'installazione al runtime condiviso. Non viene installato l'intero SDK.

`-DebugSymbols` (vedere la nota)

Se impostata, il programma di installazione include i simboli di debug nell'installazione.

> [!NOTE]
> L'opzione `-DebugSymbols` non è attualmente disponibile ma è pianificata per una versione successiva.

`-DryRun`

Se impostata, lo script non esegue l'installazione ma visualizza la riga di comando da usare per installare in modo coerente la versione attualmente richiesta dell'interfaccia della riga di comando .NET. Se ad esempio si specifica la versione `latest`, verrà visualizzato un collegamento con la versione specifica in modo che questo comando possa essere usato in modo deterministico in uno script di compilazione. Viene visualizzato anche il percorso del file binario se si preferisce installarlo o scaricarlo manualmente.

`-NoPath`

Se impostata, il prefisso o la directory di installazione non viene esportata nel percorso per la sessione corrente. Per impostazione predefinita, lo script modifica il percorso rendendo disponibili gli strumenti dell'interfaccia della riga di comando immediatamente dopo l'installazione.

`-AzureFeed`

Specifica l'URL del feed di Azure per il programma di installazione. È consigliabile non modificare questo valore. Il valore predefinito è `https://dotnetcli.azureedge.net/dotnet`.

`-ProxyAddress`

Se impostata, il programma di installazione usa il proxy durante le richieste Web.

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]`

`--channel <CHANNEL>`

Specifica il canale di origine per l'installazione. I valori sono `future`, `dev` e `production`. Il valore predefinito è `production`.

`--version <VERSION>`

Specifica la versione dell'interfaccia della riga di comando da installare. La versione deve essere specificata con un numero a tre parti (ad esempio, 1.0.0-13232). Se omessa, per impostazione predefinita viene usato il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usata l'ultima versione.

`--install-dir <DIRECTORY>`

Specifica il percorso di installazione. Se la directory non esiste, verrà creata. Il valore predefinito è `$HOME/.dotnet`.

`--architecture <ARCHITECTURE>`

Architettura dei file binari di .NET Core da installare. I valori possibili sono `auto`, `x64` e `amd64`. Il valore predefinito è `auto`, che rappresenta l'architettura del sistema operativo attualmente in esecuzione.

`--shared-runtime`

Se impostata, questa opzione limita l'installazione al runtime condiviso. Non viene installato l'intero SDK.

`--debug-symbols`

Se impostata, il programma di installazione include i simboli di debug nell'installazione.

> [!NOTE]
> Questa opzione non è attualmente disponibile ma è pianificata per una versione successiva.

`--dry-run`

Se impostata, lo script non esegue l'installazione ma visualizza la riga di comando da usare per installare in modo coerente la versione attualmente richiesta dell'interfaccia della riga di comando .NET. Se ad esempio si specifica la versione `latest`, verrà visualizzato un collegamento con la versione specifica in modo che questo comando possa essere usato in modo deterministico in uno script di compilazione. Viene visualizzato anche il percorso del file binario se si preferisce installarlo o scaricarlo manualmente.

`--no-path`

Se impostata, il prefisso o la directory di installazione non viene esportata nel percorso per la sessione corrente. Per impostazione predefinita, lo script modifica il percorso rendendo disponibili gli strumenti dell'interfaccia della riga di comando immediatamente dopo l'installazione.

`--verbose`

Visualizza le informazioni di diagnostica.

`--azure-feed`

Specifica l'URL del feed di Azure per il programma di installazione. È consigliabile non modificare questo valore. Il valore predefinito è `https://dotnetcli.azureedge.net/dotnet`.

`--help`

Stampa la Guida per lo script.

## <a name="examples"></a>Esempi

Installare la versione per sviluppatori più recente nel percorso predefinito:

Windows:

`./dotnet-install.ps1 -Channel Future`

macOS/Linux:

`./dotnet-install.sh --channel Future`

Installare l'anteprima più recente nel percorso specificato:

Windows:

`./dotnet-install.ps1 -Channel preview -InstallDir C:\cli`

macOS/Linux:

`./dotnet-install.sh --channel preview --install-dir ~/cli`
