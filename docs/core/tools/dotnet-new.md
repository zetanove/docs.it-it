---
title: Comando dotnet-new | Microsoft Docs
description: Il comando dotnet-new consente di creare nuovi progetti .NET Core nella directory corrente.
keywords: dotnet-new, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 263c3d05-3a47-46a6-8023-3ca16b488410
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: a49fe94ca8f678c614fb7f58767693c73e34c737

---

#<a name="dotnet-new"></a>dotnet-new

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 2 di .NET Core. Per gli strumenti di .NET Core versione RC4, vedere l'argomento [dotnet-new (strumenti di .NET Core RC4)](../preview3/tools/dotnet-new.md).

## <a name="name"></a>Nome
`dotnet-new`: consente di creare un nuovo progetto .NET Core nella directory corrente.

## <a name="synopsis"></a>Riepilogo
`dotnet new [--help] [--type] [--lang]`

## <a name="description"></a>Descrizione
Il comando `dotnet new` rappresenta un modo pratico per inizializzare un progetto .NET Core valido e include l'esempio di codice sorgente per provare il set di strumenti dell'interfaccia della riga di comando. 

Questo comando viene richiamato nel contesto di una directory. Quando richiamato, il comando avrà come risultato il rilascio dei due elementi principali nella directory corrente: 

1. Un file `Program.cs` (o `Program.fs`) contenente un programma "Hello World" di esempio.
2. Un file `project.json` valido.

Dopo questa operazione, il progetto è pronto per essere compilato e/o ulteriormente modificato. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-l|--lang <C#|F#>`

Linguaggio del progetto. Il valore predefinito è `C#`. Altri valori validi sono `csharp`, `fsharp`, `cs` e `fs`.

`-t|--type`

Tipo di progetto. I valori validi per C# sono `console`, `web`, `lib` e `xunittest`, mentre per F# è valido solo `console`. 

## <a name="examples"></a>Esempi

Creare un progetto di applicazione console C# nella directory corrente:

`dotnet new` o `dotnet new --lang c#` 
   
Creare un progetto di applicazione console F# nella directory corrente:

`dotnet new --lang f#`
  
Creare un nuovo progetto di applicazione console ASP.NET Core C# nella directory corrente:

`dotnet new -t web`


<!--HONumber=Feb17_HO2-->


