---
title: script dotnet-install | Microsoft Docs
description: Informazioni sugli script dotnet-install per l&quot;installazione degli strumenti dell&quot;interfaccia della riga di comando di .NET Core e del runtime condiviso.
keywords: dotnet-install, script dotnet-install, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: b64e7e6f-ffb4-4fc8-b43b-5731c89479c2
translationtype: Human Translation
ms.sourcegitcommit: 99254f84873003496ee00214d55ff908f9fd47d3
ms.openlocfilehash: 6301fb61be27d7dac6ead57159c0d9461b3eacb5
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-install-scripts-reference"></a>Riferimento agli script dotnet-install

## <a name="name"></a>Nome

`dotnet-install.ps1` | `dotnet-install.sh`: script usato per l'installazione degli strumenti dell'interfaccia della riga di comando e del runtime condiviso di .NET Core.

## <a name="synopsis"></a>Riepilogo
Windows:

```
dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture]
    [-SharedRuntime] [-DebugSymbols] [-DryRun] [-NoPath] [-AzureFeed] [-ProxyAddress]
```

macOS/Linux:

```
dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture]
    [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]
```

## <a name="description"></a>Descrizione
Gli script `dotnet-install` vengono usati per eseguire un'installazione senza privilegi di amministratore della toolchain dell'interfaccia della riga di comando e del runtime condiviso. È possibile scaricare gli script dal [repository dell'interfaccia della riga di comando di GitHub](https://github.com/dotnet/cli/tree/rel/1.0.0/scripts/obtain). 

Gli script vengono usati principalmente negli scenari di automazione e nelle installazioni senza privilegi di amministratore. Sono disponibili due script, uno per PowerShell, che funziona in Windows, e uno script Bash, che funziona in Linux o in OS X. I due script hanno un comportamento analogo. Lo script Bash "legge" anche i commutatori PowerShell, pertanto è possibile usarli in tutte le piattaforme. 

Gli script di installazione scaricheranno il file ZIP/tarball da destinazioni di compilazione dell'interfaccia della riga di comando e lo installeranno nel percorso predefinito o in un percorso specificato da `--install-dir`. Per impostazione predefinita, lo script di installazione scaricherà e installerà l'SDK. Se si vuole ottenere solo il runtime condiviso, è possibile specificare l'argomento `--shared-runtime`. 

Per impostazione predefinita, lo script aggiungerà il percorso di installazione a $PATH per la sessione corrente. Questo percorso può essere sostituito se viene usato l'argomento `--no-path`. 

Prima di eseguire lo script, installare tutte le [dipendenze](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md) necessarie.

È possibile installare una versione specifica usando l'argomento `--version`. La versione deve essere specificata come versione a tre parti (ad esempio, 1.0.0-13232). Se omesso, per impostazione predefinita sarà il primo file [global.json](global-json.md) nella gerarchia al di sopra della cartella in cui è stato richiamato lo script contenente la proprietà `version`. Se non è presente, verrà usato il valore Ultima versione.

È inoltre possibile usare questo script per ottenere l'SDK o i file binari di debug del runtime condiviso con simboli di debug usando l'argomento `--debug`. Se non si esegue questa operazione durante la prima installazione e ci si rende conto in un secondo momento che i simboli di debug sono necessari, è possibile eseguire nuovamente lo script con questo argomento e la versione dei bit installata. 

## <a name="options"></a>Opzioni
Le opzioni variano a seconda delle implementazioni degli script. 

### <a name="powershell-windows"></a>PowerShell (Windows)
`-Channel [CHANNEL]`

Canale da cui eseguire l'installazione, ad esempio `future`, `preview`, `production`. Il valore predefinito è `production`.

`-Version [VERSION]`

Versione dell'interfaccia della riga di comando da installare. È necessario specificare la versione come versione in 3 parti, ad esempio 1.0.0-13232. Se omessa, per impostazione predefinita verrà usato il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usato il valore Ultima versione.

`-InstallDir [DIR]`

Percorso in cui eseguire l'installazione. Se la directory non esiste, verrà creata. Il valore predefinito è *%LocalAppData%\.dotnet*.

`-Architecture [ARCH]`

Architettura dei file binari di .NET Core da installare. I valori possibili sono &lt;auto&gt;, x64 e x86. Il valore predefinito è &lt;auto&gt; che rappresenta l'architettura del sistema operativo attualmente in esecuzione.

`-SharedRuntime`

Se impostata, installa solo i bit del runtime condiviso, non l'intero SDK.

`-DebugSymbols`

Se impostata, il programma di installazione includerà i simboli di debug nell'installazione.

> [!NOTE]
> Questa opzione non funziona ancora.

`-DryRun`

Se impostata, lo script non esegue l'installazione ma visualizza la riga di comando da usare per installare in modo coerente la versione attualmente richiesta dell'interfaccia della riga di comando .NET. Ad esempio, se si specifica la versione `latest`, viene visualizzato un collegamento con la versione specifica in modo che questo comando possa essere usato in modo deterministico in uno script di compilazione.
Viene visualizzato anche il percorso dei file binari per poterli installare o scaricare manualmente.

`-NoPath`

Se impostata, il prefisso o la directory di installazione non viene esportata nel percorso per la sessione corrente. Per impostazione predefinita, lo script modifica il percorso rendendo disponibili gli strumenti dell'interfaccia della riga di comando immediatamente dopo l'installazione.

`-AzureFeed`

URL per il feed di Azure che deve essere usato dal programma di installazione. È consigliabile non modificare questa opzione. Il valore predefinito è `https://dotnetcli.azureedge.net/dotnet`.

`-ProxyAddress`

Se impostata, il programma di installazione usa il proxy durante le richieste Web.

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture]
    [--shared-runtime] [--debug-symbols] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--help]
`

`--channel [CHANNEL]`

Canale da cui eseguire l'installazione, ad esempio "future", "dev", "production". Il valore predefinito è "Production".

`--version [VERSION]`

Versione dell'interfaccia della riga di comando da installare. È necessario specificare la versione come versione in 3 parti, ad esempio 1.0.0-13232. Se omessa, per impostazione predefinita verrà usato il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usato il valore Ultima versione.

`--install-dir [DIR]`

Percorso in cui eseguire l'installazione. Se la directory non esiste, verrà creata. Il valore predefinito è `$HOME/.dotnet`.

`--architecture [ARCH]`

Architettura dei file binari di .NET da installare. I valori possibili sono &lt;auto&gt;, x64 e amd64. Il valore predefinito è &lt;auto&gt; che rappresenta l'architettura del sistema operativo attualmente in esecuzione.

`--shared-runtime`

Se impostata, installa solo i bit del runtime condiviso, non l'intero SDK.

`--debug-symbols`

Se impostata, il programma di installazione includerà i simboli di debug nell'installazione.

> [!NOTE]
> Questa opzione non funziona ancora.

`--dry-run`

Se impostata, lo script non esegue l'installazione ma visualizza la riga di comando da usare per installare in modo coerente la versione attualmente richiesta dell'interfaccia della riga di comando .NET. Ad esempio, se si specifica la versione `latest`, viene visualizzato un collegamento con la versione specifica in modo che questo comando possa essere usato in modo deterministico in uno script di compilazione.
Viene visualizzato anche il percorso dei file binari per poterli installare o scaricare manualmente.

`--no-path`

Se impostata, il prefisso o la directory di installazione non viene esportata nel percorso per la sessione corrente. Per impostazione predefinita, lo script modifica il percorso rendendo disponibili gli strumenti dell'interfaccia della riga di comando immediatamente dopo l'installazione.

`--verbose`

Visualizza le informazioni di diagnostica.

`--azure-feed`

URL per il feed di Azure che deve essere usato dal programma di installazione. È consigliabile non modificare questa opzione. Il valore predefinito è `https://dotnetcli.azureedge.net/dotnet`.

`--help`

Stampa la Guida per lo script.

## <a name="examples"></a>Esempi

Installare la versione più recente per sviluppatori nel percorso predefinito:

Windows:

`./dotnet-install.ps1 -Channel Future`

macOS/Linux:

`./dotnet-install.sh --channel Future`

Installare l'anteprima più recente nel percorso specificato:

Windows:

`./dotnet-install.ps1 -Channel preview -InstallDir C:\cli`

macOS/Linux:

`./dotnet-install.sh --channel preview --install-dir ~/cli`
