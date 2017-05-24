---
title: Comando dotnet-new - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-new consente di creare nuovi progetti .NET Core nella directory corrente.
keywords: dotnet-new, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
ms.translationtype: Human Translation
ms.sourcegitcommit: 68fbe2e9895825bbbb41cfe025bfdf1d4f9d3d04
ms.openlocfilehash: 14279ea6fdf4af52c0492f2dad1171d8150ac95b
ms.contentlocale: it-it
ms.lasthandoff: 05/05/2017

---

# <a name="dotnet-new"></a>dotnet-new

## <a name="name"></a>Nome

`dotnet-new`: crea un nuovo progetto, un file di configurazione o una soluzione sulla base del modello specificato.

## <a name="synopsis"></a>Riepilogo

```
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet new` rappresenta un modo pratico per inizializzare un progetto .NET Core valido. 

Questo comando chiama il [motore del modello](https://github.com/dotnet/templating) per creare gli elementi su disco in base alle opzioni e al modello specificati.

## <a name="arguments"></a>Argomenti

`TEMPLATE`

Modello di cui creare un'istanza quando viene richiamato il comando. Ogni modello può avere opzioni specifiche che è possibile passare. Per altre informazioni, vedere [Opzioni del modello](#template-options).

Il comando contiene un elenco predefinito di modelli. Usare `dotnet new -all` per ottenere un elenco dei modelli disponibili. La tabella seguente descrive i modelli preinstallati nell'SDK. Il linguaggio predefinito per il modello è indicato tra parentesi quadre.

|Descrizione del modello  | Nome del modello  | Linguaggi |
|----------------------|----------------|-----------|
| Applicazione console  | console        | [C#], F#  |
| Libreria di classi        | classlib       | [C#], F#  |
| Progetto di unit test    | mstest         | [C#], F#  |
| Progetto di xUnit test   | xunit          | [C#], F#  |
| ASP.NET Core vuoto   | Web            | [C#]      |
| App Web ASP.NET Core | mvc            | [C#], F#  |
| API Web ASP.NET Core | webapi         | [C#]      |
| Configurazione Nuget         | nugetconfig    |           |
| Configurazione Web           | webconfig      |           |
| File di soluzione        | sln            |           |

## <a name="options"></a>Opzioni

`-h|--help`

Stampa la Guida per il comando. Può essere richiamato per il comando `dotnet new` stesso o per qualsiasi modello, ad esempio `dotnet new mvc --help`.

`-l|--list`

Elenca i modelli contenenti il nome specificato. Se richiamato per il comando `dotnet new`, elenca i possibili modelli disponibili per la directory specificata. Se ad esempio la directory contiene già un progetto, non elenca tutti i modelli di progetto.

`-lang|--language {C#|F#}`

Linguaggio del modello da creare. Il linguaggio accettato varia a seconda del modello. Vedere i valori predefiniti nella sezione [Argomenti](#arguments). Non è valido per alcuni modelli.

`-n|--name <OUTPUT_NAME>`

Nome dell'output creato. Se non viene specificato alcun nome, viene usato il nome della directory corrente.

`-o|--output <OUTPUT_DIRECTORY>`

Percorso in cui posizionare l'output generato. Il valore predefinito è la directory corrente.

`-all|--show-all`

Mostra tutti i modelli per un tipo di progetto specifico durante l'esecuzione nel contesto del comando `dotnet new` senza altri elementi. Durante l'esecuzione nel contesto di un modello specifico, ad esempio `dotnet new web -all`, `-all` viene interpretato come un flag di imposizione della creazione. Questo è necessario quando la directory di output contiene già un progetto.

## <a name="template-options"></a>Opzioni del modello

Per ogni modello di progetto potrebbero essere disponibili opzioni aggiuntive. I modelli principali includono le opzioni seguenti:

**console, xunit, mstest, web, webapi**

`-f|--framework`: specifica il [framework](../../standard/frameworks.md) di destinazione. Valori: `netcoreapp1.0` o `netcoreapp1.1` (impostazione predefinita: `netcoreapp1.0`)

**mvc**

`-f|--framework`: specifica il [framework](../../standard/frameworks.md) di destinazione. Valori: `netcoreapp1.0` o `netcoreapp1.1` (`Default: netcoreapp1.0`)

`-au|--auth`: tipo di autenticazione da usare. Valori: `None` o `Individual` (impostazione predefinita: `None`)

`-uld|--use-local-db`: indica se usare o meno LocalDB invece di SQLite. Valori: `true` o `false` (impostazione predefinita: `false`)

**classlib**

`-f|--framework`: specifica il [framework](../../standard/frameworks.md) di destinazione. Valori: `netcoreapp1.0`, `netcoreapp1.1` o da `netstandard1.0` a `netstandard1.6` (impostazione predefinita: `netstandard1.4`)

## <a name="examples"></a>Esempi

Creare un progetto di applicazione console F# nella directory corrente:

`dotnet new console -lang f#` 
   
Creare un nuovo progetto di applicazione MVC ASP.NET Core C# nella directory corrente senza autenticazione con destinazione .NET Core 1.0:  

`dotnet new mvc -au None -f netcoreapp1.0`
 
Creare una nuova applicazione xUnit con destinazione .NET Core 1.1:

`dotnet new xunit --Framework netcoreapp1.1`

Elencare tutti i modelli disponibili per MVC:

`dotnet new mvc -l`

