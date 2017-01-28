---
title: Script dotnet-install | .NET Core SDK
description: Informazioni sugli script dotnet-install per l&quot;installazione degli strumenti dell&quot;interfaccia della riga di comando di .NET Core e del runtime condiviso.
keywords: dotnet-install, script dotnet-install, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 59b9c456-2bfd-4adc-8202-a1c6a0a6c787
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 08a401abed36e68caa7172e05184d18469fef48f

---

#<a name="dotnet-install-scripts-reference"></a>Riferimento agli script dotnet-install

## <a name="name"></a>Nome
dotnet-install.ps1 | dotnet-install.sh: script usato per l'installazione degli strumenti dell'interfaccia della riga di comando e del runtime condiviso

## <a name="synopsis"></a>Riepilogo
Windows:

`dotnet-install.ps1 [-Channel] [-Version]
    [-InstallDir] [-Debug] [-NoPath] 
    [-SharedRuntime]`

macOS/Linux:

`dotnet-install.sh [--channel] [--version]
    [--install-dir] [--debug] [--no-path] 
    [--shared-runtime]`

## <a name="description"></a>Descrizione
Gli script `dotnet-install` vengono usati per eseguire un'installazione senza privilegi di amministratore della toolchain dell'interfaccia della riga di comando e del runtime condiviso. È possibile scaricare gli script dal [repository dell'interfaccia della riga di comando di GitHub](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/scripts/obtain). 

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

Versione dell'interfaccia della riga di comando da installare. È necessario specificare la versione come versione a tre parti, ad esempio 1.0.0-13232. Se omesso, per impostazione predefinita sarà il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usato il valore Ultima versione.     

`-InstallDir [DIR]`

Percorso in cui eseguire l'installazione. Se la directory non esiste, verrà creata. Il valore predefinito è *%LocalAppData%\.dotnet*.

`-Debug`

`true` per indicare che è necessario usare pacchetti più grandi contenenti simboli di debug. In caso contrario, `false`. Il valore predefinito è `false`.

`-NoPath`

`true` per indicare che prefix/installdir non vengono esportati nel percorso per la sessione corrente. In caso contrario, `false`. Il valore predefinito è `false`, pertanto PATH viene modificato. In questo modo gli strumenti dell'interfaccia della riga di comando vengono resi disponibili subito dopo l'installazione. 

`-SharedRuntime`

`true` per installare solo i bit del runtime condiviso. `false` per installare l'intero SDK. Il valore predefinito è `false`.

### <a name="bash-macoslinux"></a>Bash (macOS/Linux)
`--channel [CHANNEL]`

Canale da cui eseguire l'installazione, ad esempio "future", "preview", "production". Il valore predefinito è "Production".

`--version [VERSION]`

Versione dell'interfaccia della riga di comando da installare. È necessario specificare la versione come versione a tre parti, ad esempio 1.0.0-13232. Se omesso, per impostazione predefinita sarà il primo file [global.json](global-json.md) contenente la proprietà `version`. Se non è presente, verrà usato il valore Ultima versione.     

`--install-dir [DIR]`

Percorso in cui eseguire l'installazione. Se la directory non esiste, verrà creata. Il valore predefinito è `$HOME/.dotnet`.

`--debug`

`true` per indicare che è necessario usare pacchetti più grandi contenenti simboli di debug. In caso contrario, `false`. Il valore predefinito è `false`.

`--no-path`

`true` per indicare che prefix/installdir non vengono esportati nel percorso per la sessione corrente. In caso contrario, `false`. Il valore predefinito è `false`, pertanto PATH viene modificato. In questo modo gli strumenti dell'interfaccia della riga di comando vengono resi disponibili subito dopo l'installazione.  

`--shared-runtime`

`true` per installare solo i bit del runtime condiviso. `false` per installare l'intero SDK. Il valore predefinito è `false`.

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



<!--HONumber=Nov16_HO3-->


