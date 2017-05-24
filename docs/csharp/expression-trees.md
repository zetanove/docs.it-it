---
title: Expression Trees
description: Expression Trees
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: aceb4719-0d5a-4b19-b01f-b51063bcc54f
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e6ec60b6cdbe29def719f7970dad15fad65902e7
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

# <a name="expression-trees"></a>Expression Trees

Se si è usato LINQ, si ha esperienza con una ricca libreria in cui i tipi `Func` fanno parte del set di API. (Se non si ha familiarità con LINQ, è consigliabile prima leggere l'[esercitazione LINQ](linq/index.md) e l'esercitazione sulle [espressioni lambda](lambda-expressions.md).) Gli *alberi delle espressioni* offrono maggiore interazione con gli argomenti che sono funzioni.

Scrivere gli argomenti della funzione, in genere usando le espressioni lambda, quando si creano query LINQ. In una tipica query LINQ, tali argomenti delle funzioni vengono trasformati in un delegato che viene creato dal compilatore. 

Quando si vuole usare una maggiore interazione, è necessario usare gli *alberi delle espressioni*.
Gli alberi delle espressioni rappresentano il codice come una struttura che è possibile esaminare, modificare o eseguire. Questi strumenti offrono la possibilità di modificare il codice in fase di esecuzione. È possibile scrivere codice che esamina gli algoritmi in esecuzione o inserisce nuove funzionalità. Negli scenari più avanzati, è possibile modificare gli algoritmi in esecuzione e anche convertire espressioni C# in un altro formato per l'esecuzione in un altro ambiente.

Si è probabilmente già scritto codice che usa gli alberi delle espressioni. Le API LINQ di Entity Framework accettano gli alberi delle espressioni come argomenti per il criterio di espressione di query LINQ.
Ciò consente a [Entity Framework](http://docs.efproject.net/en/latest/) di convertire la query scritta in C# in SQL che viene eseguito nel motore di database. Un altro esempio è [Moq](https://github.com/Moq/moq), che è un framework di simulazione tra i più diffusi per .NET.

Le sezioni rimanenti di questa esercitazione illustreranno che cosa sono gli alberi delle espressioni, esamineranno le classi di framework che supportano gli alberi delle espressioni e spiegheranno come lavorare con gli alberi delle espressioni. Si apprenderà come leggere gli alberi delle espressioni, come creare alberi delle espressioni, come creare alberi delle espressioni modificati e come eseguire il codice rappresentato dagli alberi delle espressioni. Al termine, sarà possibile usare queste strutture per creare algoritmi adattivi completi.
<style type="text/css"> ol { list-style-type: upper-roman; } </style>
1. [Nozioni di base sugli alberi delle espressioni](expression-trees-explained.md)

    Understand the structure and concepts behind *Expression Trees*.
    
2. [Tipi di framework che supportano alberi delle espressioni](expression-classes.md)
    
    Informazioni sulle strutture e le classi che definiscono e modificano gli alberi delle espressioni.
    
3. [Esecuzione di espressioni](expression-trees-execution.md)

    Informazioni su come convertire un albero delle espressioni rappresentato come un'espressione lambda in un delegato ed eseguire il delegato risultante.

4. [Interpretazione di espressioni](expression-trees-interpreting.md)

    Informazioni su come attraversare ed esaminare gli *alberi delle espressioni* per comprendere quale codice rappresenta l'albero delle espressioni.

5. [Creazione di espressioni](expression-trees-building.md)

    Informazioni su come costruire i nodi per un albero delle espressioni e creare alberi delle espressioni.

6. [Conversione di espressioni](expression-trees-translating.md)

    Informazioni su come creare una copia modificata di un albero delle espressioni o convertire un albero delle espressioni in un formato diverso.

7. [Conclusioni](expression-trees-summary.md)

    Esaminare le informazioni sugli alberi delle espressioni.
    

