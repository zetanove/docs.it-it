---
title: Funzioni locali ed espressioni lambda
description: "Perché le funzioni locali possono essere una scelta migliore rispetto alle espressioni lambda"
keywords: "C#, .NET, .NET Core, funzionalità recenti, novità, funzioni locali, espressioni lambda"
author: BillWagner
ms.author: wiwagn
ms.date: 10/27/2016
ms.topic: article
ms.prod: visual-studio-dev-15
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 368d1752-3659-489a-97b4-f15d87e49ae3
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 4b2fdc86a3b2485f6177112a584291558fb76984
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

### <a name="local-functions-compared-to-lambda-expressions"></a>Confronto tra funzioni locali ed espressioni lambda

In alcuni casi d'uso è possibile creare un'espressione lambda e usarla senza la necessità di creare una funzione locale. Il metodo asincrono seguente esegue questa operazione:

[!code-csharp[TaskLambdaExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "Metodo con restituzione di Task con espressione lambda")]

Esistono tuttavia diversi motivi per preferire l'uso di funzioni locali alla definizione e alla chiamata di espressioni lambda.

Innanzitutto, per le espressioni lambda il compilatore deve creare una classe anonima e un'istanza della classe per archiviare eventuali variabili acquisite dalla chiusura. La chiusura per questa espressione lambda contiene le variabili `address`, `index` e `name`. 

In secondo luogo, le espressioni lambda vengono implementate creando un'istanza di un delegato e richiamando il delegato. Le funzioni locali sono implementate come chiamate al metodo.
La creazione di istanze necessaria per le espressioni lambda comporta allocazioni di memoria aggiuntive che possono ridurre le prestazioni nei percorsi di codice in cui il tempo è un fattore cruciale.
Questo sovraccarico non si verifica per le funzioni locali.

In terzo luogo, le funzioni locali possono essere chiamate prima che vengano definite. Le espressioni lambda devono essere dichiarate prima di essere definite. Per questa ragione, le funzioni locali sono più semplici da usare negli algoritmi ricorsivi:

[!code-csharp[LocalFunctionFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "Fattoriale ricorsivo che usa una funzione locale")]

Confrontare l'implementazione con una versione che usa le espressioni lambda:

[!code-csharp[26_LambdaFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "Fattoriale ricorsivo che usa le espressioni lambda")]

Si noti che la versione che usa l'espressione lambda deve dichiarare e inizializzare l'espressione lambda `nthFactorial` prima di definirla. In caso contrario, si verifica un errore di compilazione per fare riferimento a `nthFactorial` prima di assegnarla.
Gli algoritmi ricorsivi sono più facili da creare usando le funzioni locali. 

Sebbene le funzioni locali possano apparire ridondanti rispetto alle espressioni lambda, in realtà hanno finalità e usi diversi.
Le funzioni locali sono più efficienti nel caso si voglia scrivere una funzione che viene chiamata solo dal contesto di un altro metodo.


