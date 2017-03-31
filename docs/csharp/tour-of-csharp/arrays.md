---
title: Matrici C# | Panoramica del linguaggio C#
description: Le matrici costituiscono il tipo di raccolta di base del linguaggio C#
keywords: .NET, csharp, matrice, raccolta
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a440704c-9e88-4c75-97dd-bfe30ca0fb97
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e3a029a1199c32cf2d943a02ce196512e44bd79a
ms.lasthandoff: 03/13/2017

---

# <a name="arrays"></a>Matrici

Una ***matrice*** è una struttura di dati contenente una serie di variabili accessibili tramite indici calcolati. Le variabili contenute in una matrice, chiamate anche ***elementi*** della matrice, sono tutte dello stesso tipo, definito ***tipo di elemento*** della matrice.

Poiché i tipi di matrice sono tipi di riferimento, la dichiarazione di una variabile di matrice si limita a riservare spazio per un riferimento a un'istanza di matrice. Le istanze di matrice effettive vengono create dinamicamente in fase di esecuzione tramite l'operatore new. L'uso dell'operatore new consente di specificare la ***lunghezza*** della nuova istanza di matrice, che viene fissata per l'intera durata dell'istanza. Gli indici degli elementi di una matrice sono compresi tra `0` e `Length - 1`. L'operatore `new` inizializza automaticamente gli elementi di una matrice sul rispettivo valore predefinito che, ad esempio, equivale a zero per tutti i tipi numerici e a `null` per tutti i tipi di riferimento.

Nell'esempio seguente viene creata una matrice di elementi `int`, viene inizializzata la matrice e ne viene stampato il contenuto.

[!code-csharp[ArraySample](../../../samples/snippets/csharp/tour/arrays/Program.cs#L3-L18)]

In questo esempio viene creata e usata una ***matrice unidimensionale***. C# supporta anche ***matrici multidimensionali***. Il numero di dimensioni di un tipo di matrice, chiamato anche ***rango*** del tipo di matrice, è pari a uno più il numero di virgole tra parentesi quadre del tipo di matrice. Nell'esempio seguente vengono allocate, rispettivamente, una matrice unidimensionale, una bidimensionale e una tridimensionale.

[!code-csharp[ArrayRank](../../../samples/snippets/csharp/tour/arrays/Program.cs#L24-L26)]

La matrice `a1` contiene 10 elementi, la matrice `a2` contiene 50 (10 × 5) elementi e la `a3` matrice contiene 100 (10 × 5 × 2) elementi.
L'elemento di una matrice può essere di qualsiasi tipo, anche di tipo matrice. Una matrice con elementi di tipo matrice viene chiamata talvolta ***matrice di matrici***, poiché le lunghezze delle matrici elemento non devono essere tutte uguali. Nell'esempio seguente viene allocata una matrice di matrici di `int`:

[!code-csharp[ArrayAllocation](../../../samples/snippets/csharp/tour/arrays/Program.cs#L31-L34)]

La prima riga crea una matrice con tre elementi, ognuno di tipo `int[]` e con un valore iniziale di `null`. Le righe successive inizializzano quindi i tre elementi con riferimenti a singole istanze di matrice di lunghezza variabile.

L'operatore new consente di specificare i valori iniziali degli elementi di matrice usando un ***inizializzatore di matrice***, ovvero un elenco di espressioni scritte tra i delimitatori `{` e `}`. Nell'esempio seguente viene allocata e inizializzata una matrice `int[]` con tre elementi.

[!code-csharp[ArrayInitialization](../../../samples/snippets/csharp/tour/arrays/Program.cs#L39-L39)]

La lunghezza della matrice viene dedotta dal numero di espressioni comprese tra { e }. Per evitare di ridefinire il tipo di matrice, è possibile abbreviare le dichiarazioni di campo e variabile locale.

[!code-csharp[ArrayInitialization](../../../samples/snippets/csharp/tour/arrays/Program.cs#L44-L44)]

Entrambi gli esempi precedenti equivalgono a quello seguente:

[!code-csharp[ArrayAssignment](../../../samples/snippets/csharp/tour/arrays/Program.cs#L49-L53)]

>[!div class="step-by-step"]
[Precedente](structs.md)
[Successivo](interfaces.md)

