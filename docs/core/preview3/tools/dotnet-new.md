---
title: Comando dotnet-new | Microsoft Docs
description: Il comando dotnet-new consente di creare nuovi progetti .NET Core nella directory corrente.
keywords: dotnet-new, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 02/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
translationtype: Human Translation
ms.sourcegitcommit: 96fd8ea3e55ea33e0bdd0bf3c50a10d0de6db1a1
ms.openlocfilehash: f0c62647c5817db2057c60a7a95a62f08f7889a5

---
#<a name="dotnet-new-net-core-tools-rc4"></a>dotnet-new (Strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [dotnet-new](../../tools/dotnet-new.md).

## <a name="name"></a>Nome
dotnet-new: consente di creare un nuovo progetto .NET Core nella directory corrente

## <a name="synopsis"></a>Riepilogo
```
dotnet new [template] [-lang|--language] [-n|--name] [-o|--output] [-h|--help]
dotnet new [template] [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

## <a name="description"></a>Descrizione
Il comando `dotnet new` rappresenta un modo pratico per inizializzare un progetto .NET Core valido e include l'esempio di codice sorgente per provare il set di strumenti dell'interfaccia della riga di comando. 

Questo comando viene richiamato nel contesto di una directory. Quando viene richiamato, il comando eseguirà lo scaffolding delle risorse e dei file in base al modello e alle opzioni passate al comando. 

Dopo questa operazione, il progetto è pronto per essere compilato e/o ulteriormente modificato. 

## <a name="arguments"></a>Argomenti
template: modello di cui creare un'istanza quando viene richiamato il comando.

Il comando contiene un elenco predefinito di modelli. Usare `dotnet new --help`. 

## <a name="options"></a>Opzioni

`-l|--list`         

Elenca i modelli contenenti il nome specificato.

`-lang|--language`  

Specifica il linguaggio del modello da creare.

`-n|--name`         

Nome per l'output da creare. Se non viene specificato alcun nome, viene usato il nome della directory corrente.

`-o|--output`       

Percorso in cui posizionare l'output generato.

`-all|--show-all`   

Mostra tutti i modelli per un tipo specifico di progetto.

`-h|--help`

Stampa la Guida per il comando.

## <a name="template-options"></a>Opzioni del modello
Per ogni modello di progetto potrebbero essere disponibili opzioni aggiuntive. I modelli principali, ad esempio, includono le opzioni seguenti.

**console, xunit, mstest**

`-f|--framework`: specifica il framework di destinazione. Valori : netcoreapp1.0 o netcoreapp1.1 (valore predefinito: netcoreapp1.0)

**web, webapi**

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


<!--HONumber=Feb17_HO3-->


