---
title: Struttura del programma C# | Panoramica del linguaggio C#
description: Informazioni sui blocchi predefiniti di un programma C#
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 984f0314-507f-47a0-af56-9011243f5e65
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9ef19d7fa2164990edd5e27651d28aa085ec90ad
ms.lasthandoff: 03/13/2017

---

# <a name="program-structure"></a>Struttura del programma

I concetti organizzativi chiave di C# sono i ***programmi***, gli ***spazi dei nomi***, i ***tipi***, i ***membri*** e gli ***assembly***. I programmi C# sono costituiti da uno o più file di origine. I programmi dichiarano i tipi, che contengono i membri e possono essere organizzati in spazi dei nomi. Le classi e le interfacce sono esempi di tipi. I campi, i metodi, le proprietà e gli eventi sono esempi di membri. Quando vengono compilati, i programmi C# vengono inseriti fisicamente in assembly. Gli assembly in genere hanno l'estensione `.exe` o `.dll`, a seconda che implementino rispettivamente ***applicazioni*** o ***librerie***.

Nell'esempio viene dichiarata una classe denominata `Stack` in uno spazio dei nomi denominato `Acme.Collections`:

[!code-csharp[Stack](../../../samples/snippets/csharp/tour/program-structure/program.cs#L1-L34)]

Il nome completo di questa classe è `Acme.Collections.Stack`. La classe contiene vari membri: un campo `top`, due metodi `Push` e `Pop` e una classe annidata `Entry`. La classe `Entry` contiene altri tre membri: un campo `next`, un campo `data` e un costruttore. Supponendo che il codice sorgente dell'esempio sia archiviato nel file `acme.cs`, la riga di comando

```
csc /t:library acme.cs
```

compila l'esempio come libreria (codice senza un punto di ingresso `Main`) e genera un assembly denominato `acme.dll`.

> [!IMPORTANT]
> Negli esempi precedenti viene usato `csc` come compilatore C# della riga di comando. Questo compilatore è un eseguibile Windows. Per usare C# in altre piattaforme, è necessario usare gli strumenti per .NET Core. L'ecosistema .NET Core usa l'interfaccia della riga di comando `dotnet` per gestire le compilazioni della riga di comando e anche per gestire le dipendenze e richiamare il compilatore C#. Per una descrizione completa di tali strumenti sulle piattaforme supportate da .NET Core, vedere [questa esercitazione](../../core/tutorials/using-with-xplat-cli.md).

Gli assembly contengono codice eseguibile sotto forma di istruzioni di linguaggio intermedio (Intermediate Language, IL) e informazioni simboliche sotto forma di metadati. Prima di essere eseguito, il codice IL presente in un assembly viene convertito automaticamente nel codice specifico del processore dal compilatore JIT (Just-In-Time) di .NET Common Language Runtime.

Poiché un assembly è un'unità autodescrittiva di funzionalità contenente codice e metadati, in C# non sono necessari file di intestazione e direttive `#include`. I membri e i tipi pubblici contenuti in un determinato assembly vengono resi disponibili in un programma C# semplicemente facendo riferimento a tale assembly durante la compilazione del programma. Questo programma usa ad esempio la classe `Acme.Collections.Stack` dell'assembly `acme.dll`:

[!code-csharp[UsingStack](../../../samples/snippets/csharp/tour/program-structure/Program.cs#L38-L52)]

Se il programma è archiviato nel file `example.cs`, quando `example.cs` viene compilato è possibile fare riferimento all'assembly acme.dll usando l'opzione /r del compilatore:

```
csc /r:acme.dll example.cs
```

In questo modo verrà creato un assembly eseguibile denominato `example.exe` che, quando viene eseguito, genera l'output:

```
100
10
1
```

C# consente di archiviare il testo di origine di un programma in vari file di origine. Quando viene compilato un programma C# costituito da più file, tutti i file di origine vengono elaborati insieme e possono fare riferimento l'uno all'altro. A livello concettuale è come se tutti i file di origine fossero concatenati in un unico grande file prima di essere elaborati. Le dichiarazioni con prototipo non sono mai necessarie in C# perché, tranne che in rare eccezioni, l'ordine di dichiarazione non è significativo. C# non limita un file di origine alla dichiarazione di un solo tipo pubblico e non richiede che il nome del file di origine corrisponda a un tipo dichiarato nel file di origine.

>[!div class="step-by-step"]
[Precedente](index.md)
[Successivo](types-and-variables.md)

