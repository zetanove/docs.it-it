---
title: Nozioni di base sugli alberi delle espressioni
description: Nozioni di base sugli alberi delle espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: bbcdd339-86eb-4ae5-9911-4c214a39a92d
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c1d8a3f8d0627de9e1de4a8c360cf1a56b0ee1d0
ms.lasthandoff: 03/13/2017

---

# <a name="expression-trees-explained"></a>Nozioni di base sugli alberi delle espressioni

[Precedente -- Panoramica](expression-trees.md)

Un albero delle espressioni è una struttura dei dati che definisce il codice. Si basa sulle stesse strutture usate da un compilatore per analizzare il codice e generare l'output compilato. Nel corso di questa esercitazione si noterà una certa similarità tra gli alberi delle espressioni e i tipi usati nelle API di Roslyn per compilare [analizzatori e correzioni di codice](https://github.com/dotnet/roslyn-analyzers).
Gli analizzatori e le correzioni di codice sono pacchetti NuGet che eseguono l'analisi statica sul codice e possono suggerire potenziali correzioni agli sviluppatori. I concetti sono simili e il risultato finale è una struttura dei dati che consente di esaminare il codice sorgente in modo significativo. Gli alberi delle espressioni si basano tuttavia su un set di classi e API completamente diverso dalle API di Roslyn.
    
Si osservi l'esempio seguente.
Ecco una riga di codice:
```csharp
var sum = 1 + 2;
```
Analizzando la riga come se fosse un albero delle espressioni, si nota che l'albero contiene numerosi nodi.
Il nodo più esterno è un'istruzione di dichiarazione di variabile con assegnazione (`var sum = 1 + 2;`). Tale nodo contiene più nodi figlio: una dichiarazione di variabile, un operatore di assegnazione e un'espressione che rappresenta la parte a destra del segno di uguale. Questa espressione è a sua volta suddivisa in espressioni che rappresentano l'operazione di addizione e gli operandi sinistro e destro dell'addizione.

Di seguito vengono esaminate in dettaglio le espressioni che costituiscono la parte a destra del segno di uguale.
L'espressione è `1 + 2`. Si tratta di un'espressione binaria. Nello specifico, è un'espressione di addizione binaria. Un'espressione di addizione binaria ha due figli, che rappresentano i nodi sinistro e destro dell'espressione di addizione. In questo caso, entrambi i nodi sono espressioni costanti: l'operando sinistro è il valore `1` e l'operando destro è il valore `2`.

A livello visivo, l'intera istruzione è una struttura ad albero: è possibile iniziare dal nodo radice e passare a ogni nodo nell'albero per visualizzare il codice che costituisce l'istruzione:

- Istruzione di dichiarazione di variabili con assegnazione (`var sum = 1 + 2;`)
    * Dichiarazione di variabili implicite (`var sum`)
        - Parola chiave di variabile implicita (`var`)
        - Dichiarazione del nome di variabile (`sum`)
    * Operatore di assegnazione (`=`)
    * Espressione di addizione binaria (`1 + 2`)
        - Operando sinistro (`1`)
        - Operatore di addizione (`+`)
        - Operando destro (`2`)

Tutto ciò può apparire complicato, ma è molto funzionale. Seguendo la stessa procedura, è possibile scomporre espressioni molto più complesse. Si consideri l'espressione seguente:
```csharp
var finalAnswer = this.SecretSauceFuncion(
    currentState.createInterimResult(), currentState.createSecondValue(1, 2),
    decisionServer.considerFinalOptions("hello")) +
    MoreSecretSauce('A', DateTime.Now, true);
```

Anche l'espressione precedente è una dichiarazione di variabile con un'assegnazione.
In questo caso, il lato destro dell'assegnazione è una struttura ad albero molto più complessa.
Senza procedere con la scomposizione dell'espressione, si considerino i diversi nodi. Questi includono chiamate al metodo che usano l'oggetto corrente come un ricevitore, una che include un ricevitore `this` esplicito, una che non lo usa. Sono presenti chiamate al metodo che usano altri oggetti ricevitore, e argomenti costanti di diversi tipi. Infine, è presente un operatore di addizione binaria. A seconda del tipo restituito di `SecretSauceFunction()` o `MoreSecretSauce()`, l'operatore di addizione binaria può rappresentare una chiamata al metodo a un operatore di addizione con override, risolto in una chiamata al metodo statico dell'operatore di addizione binaria definito per una classe.

Nonostante l'apparente complessità, l'espressione precedente crea una struttura ad albero semplice da esplorare quanto il primo esempio. È possibile continuare ad attraversare i nodi figlio per individuare i nodi foglia nell'espressione. I nodi padre includono riferimenti ai propri elementi figlio e ogni nodo dispone di una proprietà che descrive di che tipo di nodo si tratta.

La struttura di albero delle espressioni è molto coerente. Dopo aver appreso le nozioni di base, è possibile comprendere anche il codice più complesso quando questo viene rappresentato come un albero delle espressioni. L'eleganza nella struttura dei dati spiega come il compilatore C# possa analizzare anche i programmi C# più complessi e creare l'output corretto a partire da un codice sorgente così complesso.

Dopo avere acquisito familiarità con la struttura degli alberi delle espressioni, si noterà che conoscenze acquisite consentono di operare anche con scenari avanzati. Gli alberi delle espressioni hanno capacità straordinarie.

Oltre alla conversione degli algoritmi da eseguire in altri ambienti, essi possono essere usati per semplificare la scrittura di algoritmi che verificano il codice prima che venga eseguito. È possibile scrivere un metodo i cui argomenti sono espressioni e quindi esaminare tali espressioni prima di eseguire il codice. L'albero delle espressioni è una rappresentazione completa del codice e consente quindi di visualizzare i valori di qualsiasi sottoespressione,
i nomi dei metodi e delle proprietà e il valore di qualsiasi espressione costante.
È anche possibile convertire un albero delle espressioni in un delegato eseguibile, ed eseguire il codice.

Le API degli alberi delle espressioni consentono di creare strutture che rappresentano praticamente qualsiasi costrutto di codice valido. Tuttavia, per evitare complicazioni eccessive, in un albero delle espressioni non è possibile creare alcuni idiomi di C#. Ne sono esempi le espressioni asincrone che usano le delle parole chiave `async` e `await`. Se sono necessari gli algoritmi asincroni, modificare direttamente gli oggetti `Task` invece di affidarsi al supporto del compilatore. Un altro metodo è la creazione dei cicli. In genere, i cicli vengono creati usando i cicli `for`, `foreach`, `while` o `do`. Come si vedrà [più avanti in questa serie](expression-trees-building.md), le API degli alberi delle espressioni supportano una singola espressione Loop, con le espressioni `break` e `continue` che controllano il ciclo di ripetizione.

Non è possibile modificare un albero delle espressioni.  Sono infatti strutture dei dati immutabili. Se si vuole modificare un albero delle espressioni, è necessario creare un nuovo albero che sia una copia dell'originale e che contenga le modifiche desiderate. 

[Successivo -- Tipi di framework che supportano alberi delle espressioni](expression-classes.md)

