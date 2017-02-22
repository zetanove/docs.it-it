---
title: Telemetria degli strumenti di .NET Core | Microsoft Docs
description: .NET Core
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 480df976-7568-4df4-9d26-9911357b5a31
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 697382a215a45fae159df62e7e9f4c73f5907d8f

---

# <a name="net-core-tools-telemetry-net-core-tools-rc4"></a>Telemetria degli strumenti di .NET Core (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [Telemetria degli strumenti di .NET Core](../../tools/telemetry.md).

Gli strumenti di .NET Core includono una [funzionalità di telemetria](https://github.com/dotnet/cli/pull/2145) che raccoglie le informazioni sull'utilizzo. È importante che il team di .NET comprenda come vengono usati gli strumenti per consentire a Microsoft di migliorarne le funzionalità.

I dati raccolti sono anonimi e verranno pubblicati in forma aggregata per l'uso da parte dei tecnici Microsoft e della community in base alla [licenza Creative Commons Attribution](https://creativecommons.org/licenses/by/4.0/).

## <a name="scope"></a>Ambito

Il comando `dotnet` viene usato per avviare sia le applicazioni sia gli strumenti di .NET Core. La raccolta dei dati di telemetria non viene eseguita dal comando `dotnet` stesso, ma dagli strumenti di .NET Core tramite il comando `dotnet`.

Comandi di .NET Core (con funzionalità di telemetria non abilitata):

- `dotnet`
- `dotnet [path-to-app]`

[Comandi](index.md) degli strumenti di .NET Core (con funzionalità di telemetria abilitata):

- `dotnet build`
- `dotnet pack`
- `dotnet restore`
- `dotnet run`

##<a name="behavior"></a>Comportamento

La funzionalità di telemetria degli strumenti di .NET Core è abilitata per impostazione predefinita. È possibile rifiutare esplicitamente questa funzionalità impostando una variabile di ambiente DOTNET_CLI_TELEMETRY_OPTOUT (ad esempio, `export` in macOS/Linux, `set` in Windows) su true (ad esempio, "true", 1).

##<a name="data-points"></a>Punti dati

La funzionalità raccoglie i dati seguenti:

- Il comando usato (ad esempio, "build", "restore")
- Il codice di uscita del comando
- Per i progetti di test, il Test Runner usato
- Il timestamp della chiamata
- Il framework usato
- L'eventuale presenza di ID di runtime nel nodo "runtimes"
- La versione dell'interfaccia della riga di comando usata

La funzionalità non raccoglie invece i dati personali, ad esempio i nomi utente o gli indirizzi di posta elettronica. Non esegue l'analisi del codice e non estrae i dati a livello di progetto che possono essere considerati sensibili, ad esempio nome, repository o autore (se si impostano quelli in project.json). Microsoft è interessata a conoscere come vengono usati gli strumenti e non i progetti realizzati con gli strumenti. Se si riscontra un caso in cui vengono raccolti dati sensibili, il problema è dovuto a un bug. Si invitano gli utenti a [segnalare problemi](https://github.com/dotnet/cli/issues) di questo tipo affinché possano essere corretti.

##<a name="license"></a>Licenza

La distribuzione Microsoft di .NET Core è concessa in base alle [condizioni di licenza di MICROSOFT .NET LIBRARY](https://aka.ms/dotnet-core-eula). Nelle condizioni è inclusa la sezione "DATA", riportata anche di seguito, che prevede l'abilitazione della funzionalità di telemetria.

Questa licenza viene usata anche dai [pacchetti NuGet .NET](https://www.nuget.org/profiles/dotnetframework) per i quali, tuttavia, la funzionalità di telemetria non è abilitata (vedere la precedente sezione [Ambito](#scope)).

```text
2.      DATA.  The software may collect information about you and your use of
the software, and send that to Microsoft. Microsoft may use this information
to improve our products and services. You can learn more about data collection
and use in the help documentation and the privacy statement at
http://go.microsoft.com/fwlink/?LinkId=528096 . Your use of the software
operates as your consent to these practices.
```

## <a name="disclosure"></a>Divulgazione

La prima volta che si esegue uno dei comandi, ad esempio `dotnet restore`, gli strumenti di .NET Core visualizzano il testo seguente. Questa prima esperienza riguarda la modalità di notifica della raccolta dei dati da parte di Microsoft. Inizialmente viene anche popolata la cache NuGet con le librerie di .NET Core SDK, evitando così l'invio di richieste relative a queste librerie a NuGet.org (o altri feed NuGet).

```text
Welcome to .NET Core!
---------------------
Learn more about .NET Core @ https://aka.ms/dotnet-docs. Use dotnet --help to 
see available commands or go to https://aka.ms/dotnet-cli-docs.

Telemetry
--------------
The .NET Core tools collect usage data in order to improve your experience. 
The data is anonymous and does not include command-line arguments. The data is 
collected by Microsoft and shared with the community.
You can opt out of telemetry by setting a DOTNET_CLI_TELEMETRY_OPTOUT 
environment variable to 1 using your favorite shell.
You can read more about .NET Core tools telemetry @ https://aka.ms/dotnet-cli-telemetry.

Configuring...
-------------------
A command is running to initially populate your local package cache, to 
improve restore speed and enable offline access. This command will take up to 
a minute to complete and will only happen once. 
```


<!--HONumber=Feb17_HO2-->


