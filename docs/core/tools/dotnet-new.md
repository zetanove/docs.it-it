---
title: Comando dotnet-new | Microsoft Docs
description: Il comando dotnet-new consente di creare nuovi progetti .NET Core nella directory corrente.
keywords: dotnet-new, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
translationtype: Human Translation
ms.sourcegitcommit: 99254f84873003496ee00214d55ff908f9fd47d3
ms.openlocfilehash: f0df2efe732912abbdb2d63e918b7ee1a4178b07
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-new"></a>dotnet-new

## <a name="name"></a>Nome
`dotnet-new`: crea un nuovo progetto, una file di configurazione o una soluzione basata sul modello specificato.

## <a name="synopsis"></a>Riepilogo
```
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template arguments]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>Descrizione
Il comando `dotnet new` rappresenta un modo pratico per inizializzare un progetto .NET Core valido e include l'esempio di codice sorgente per provare il set di strumenti dell'interfaccia della riga di comando. 

Quando viene richiamato, il comando chiama il [motore del modello](https://github.com/dotnet/templating) per creare gli elementi su disco in base al modello specificato e alle opzioni.

## <a name="arguments"></a>Argomenti

`<TEMPLATE>`

Modello di cui creare un'istanza quando viene richiamato il comando. Ogni modello può avere opzioni specifiche che è possibile passare. Per altre informazioni, vedere [Opzioni del modello](#template-options).

Il comando contiene un elenco predefinito di modelli. Usare `dotnet new -all` per visualizzarli tutti.

La tabella seguente descrive i modelli preinstallati nell'SDK. Il linguaggio predefinito per il modello è indicato tra parentesi quadre, ad esempio `[C#]`.

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

Elenca i modelli contenenti il nome specificato. Se richiamato per il comando `dotnet new` stesso, elenca i possibili modelli da usare nella directory specificata.
Ad esempio, se la directory contiene già un progetto, non elenca tutti i modelli di progetto.

`-lang|--language <C#|F#>`

Linguaggio del modello da creare. Il linguaggio accettato varia a seconda del modello (vedere i valori predefiniti nella sezione [Argomenti](#arguments)). Non è valido per alcuni modelli.

`-n|--name <OUTPUT_NAME>`

Nome per l'output da creare. Se non viene specificato alcun nome, viene usato il nome della directory corrente.

`-o|--output <OUTPUT_DIRECTORY>`

Percorso in cui posizionare l'output generato. Il valore predefinito è la directory corrente.

`-all|--show-all`

Mostra tutti i modelli per un tipo di progetto specifico durante l'esecuzione nel contesto del comando `dotnet new` senza altri elementi. Durante l'esecuzione nel contesto di un modello specifico, ad esempio `dotnet new web -all`, `-all` viene interpretato come un flag di imposizione della creazione. Questa situazione potrebbe verificarsi quando la directory di output contiene già un progetto.

## <a name="template-options"></a>Opzioni del modello
Per ogni modello di progetto potrebbero essere disponibili opzioni aggiuntive. I modelli principali includono le opzioni seguenti:

**console, xunit, mstest, web, webapi **

`-f|--framework`: specifica il framework di destinazione. Valori : netcoreapp1.0 o netcoreapp1.1 (valore predefinito: netcoreapp1.0)

**mvc**

`-f|--framework`: specifica il framework di destinazione. Valori : netcoreapp1.0 o netcoreapp1.1 (valore predefinito: netcoreapp1.0)

`-au|--authentication`: tipo di autenticazione da usare. Valori: None o Individual (valore predefinito: None)

`-uld|--use-local-db`: se usare o meno LocalDB invece di SQLite. Valori: true o false (valore predefinito: false)

**classlib**

`-f|--framework`: specifica il framework di destinazione. Valori: netcoreapp1.0, netcoreapp1.1 e netstandard1.0 - 1.6 (valore predefinito: netstandard1.4).

## <a name="examples"></a>Esempi

Creare un progetto di applicazione console F# nella directory corrente:

`dotnet new console -lang f#` 
   
Creare un nuovo progetto di applicazione MVC ASP.NET Core C# nella directory corrente senza autenticazione con destinazione .NET Core 1.0:  

`dotnet new mvc -au None -f netcoreapp1.0`
 
Creare una nuova applicazione XUnit con destinazione .NET Core 1.1:

`dotnet new xunit --Framework netcoreapp1.1`

Elencare tutti i modelli disponibili per MVC:

`dotnet new mvc -l`

