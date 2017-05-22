---
title: Espressioni C# | Panoramica del linguaggio C#
description: Le espressioni, gli operandi e gli operatori sono blocchi predefiniti del linguaggio C#
keywords: .NET, csharp, espressione, operatore, operando
author: BillWagner
ms.author: wiwagn
ms.date: 11/06/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 20d5eb10-7381-47b9-ad90-f1cc895aa27e
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ce5f71ab3e797015a26dddbf0579c84dec580750
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

# <a name="expressions"></a>Espressioni

Le *espressioni* sono costituite da *operandi* e *operatori*. Gli operatori di un'espressione indicano le operazioni che devono essere eseguite sugli operandi. Alcuni esempi di operatori sono `+`, `-`, `*`, `/` e `new`, mentre i valori effettivi, i campi, le variabili locali e le espressioni sono esempi di operandi.

Se un'espressione contiene più operatori, la *precedenza* degli operatori determina l'ordine in cui vengono valutati i singoli operatori. L'espressione `x + y * z`, ad esempio, viene valutata come `x + (y * z)` poiché l'operatore `*` ha la precedenza sull'operatore `+`.

Quando un operando si trova tra due operatori con la stessa precedenza, l'ordine di esecuzione delle operazioni viene determinato dall'*associatività* degli operatori:

*    Ad eccezione degli operatori di assegnazione, tutti gli operatori binari *prevedono l'associazione all'operando a sinistra*. In altri termini, le operazioni vengono eseguite da sinistra a destra. L'espressione `x + y + z` viene ad esempio valutata come `(x + y) + z`.
*    Gli operatori di assegnazione e gli operatori condizionali (`?:`) *prevedono l'associazione all'operando a destra*. In altri termini, le operazioni vengono eseguite da destra a sinistra. L'espressione `x = y = z` viene ad esempio valutata come `x = (y = z)`.

È possibile controllare la precedenza e l'associatività usando le parentesi. Ad esempio, `x + y * z` prima moltiplica `y` per `z` e quindi somma il risultato a `x`, ma `(x + y) * z` prima somma `x` e `y` e quindi moltiplica il risultato per `z`.

La maggior parte degli operatori può essere*in overload*. L'overload degli operatori consente di specificare implementazioni di operatori definite dall'utente per le operazioni in cui uno o entrambi gli operandi appartengono a un tipo struct o a una classe definita dall'utente.

Di seguito sono riepilogati gli operatori di C# e sono elencate le categorie di operatori in ordine di precedenza, a partire da quella più alta. Gli operatori della stessa categoria hanno uguale precedenza. Sotto ciascuna categoria è riportato il relativo elenco di espressioni e la descrizione di ogni tipo di espressione.

* Primario
    - `x.m`: accesso a membri
    - `x(...)`: chiamata a metodi e delegati
    - `x[...]`: accesso a matrici e indicizzatori
    - `x++`: post-incremento
    - `x--`: post-decremento
    - `new T(...)`: creazione di oggetti e delegati
    - `new T(...){...}`: creazione di oggetti con inizializzatole
    - `new {...}`: inizializzatore di oggetti anonimo
    - `new T[...]`: creazione di matrici
    - `typeof(T)`: ottiene l'oggetto @System.Type per `T`
    - `checked(x)`: valuta l'espressione in un contesto controllato
    - `unchecked(x)`: valuta l'espressione in un contesto non controllato
    - `default(T)`: ottiene un valore predefinito di tipo `T`
    - `delegate {...}`: funzione anonima (metodo anonimo)
* Unario
    - `+x`: identità
    - `-x`: negazione
    - `!x`: negazione logica
    - `~x`: negazione bit per bit
    - `++x`: pre-incremento
    - `--x`: pre-decremento
    - `(T)x`: converte in modo esplicito `x` al tipo `T`
    - `await x`: attende in modo asincrono il completamento di `x`
* Moltiplicazione
    - `x * y`: moltiplicazione
    - `x / y`: divisione
    - `x % y`: resto
* Addizione
    - `x + y`: addizione, concatenazione di stringhe, combinazione di delegati
    - `x – y`: sottrazione, rimozione di delegati
* Shift
    - `x << y`: spostamento a sinistra
    - `x >> y`: spostamento a destra
* Operatori relazionali e operatori di test del tipo
    - `x < y`: minore di
    - `x > y`: maggiore di
    - `x <= y`: minore o uguale a
    - `x >= y`: maggiore o uguale a
    - `x is T`: restituisce `true` se `x` è un oggetto `T`, altrimenti `false`
    - `x as T`: restituisce `x` tipizzato come `T` oppure `null` se `x` non è un oggetto `T`
* Uguaglianza
    - `x == y`: uguale
    - `x != y`: non uguale
* AND logico
    - `x & y`: AND Integer bit per bit, AND logico booleano
* XOR logico
    - `x ^ y`: XOR Integer bit per bit, XOR logico booleano
* OR logico
    - `x | y`: OR Integer bit per bit, OR logico booleano
* AND condizionale
    - `x && y`: restituisce `y` solo se `x` non è `false`
* OR condizionale
    - `x || y`: restituisce `y` solo se `x` non è `true`
* Null-coalescing
    - `x ?? y`: Restituisce `y` se `x` è null, altrimenti `x`
* Condizionale
    - `x ? y : z`: restituisce `y` se `x` è `true`, `z` se `x` è `false`
* Assegnazione o funzione anonima
    - `x = y`: assegnazione
    - `x op= y`: assegnazione composta. Gli operatori supportati sono
        - `*=`   `/=`   `%=`   `+=`   `-=`   `<<=`   `>>=`   `&=`  `^=`  `|=`
    - `(T x) => y`: funzione anonima (espressione lambda)

>[!div class="step-by-step"]
[Precedente](types-and-variables.md)
[Successivo](statements.md)

