---
title: Struct C# | Panoramica del linguaggio C#
description: Informazioni di base sui tipi di valori C# denominati struct
keywords: .NET, C#, struct, tipo valore
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 88a74571-f741-4a31-a2b5-1ccf165535b8
ms.translationtype: Human Translation
ms.sourcegitcommit: 38ce3cdf3aaa033d84bb2c1a421cb04c6f928ab4
ms.openlocfilehash: 04b1784b461961496856d62aa6cb70b5978e2437
ms.contentlocale: it-it
ms.lasthandoff: 05/02/2017

---

# <a name="structs"></a>Struct

Analogamente alle classi, i tipi ***struct*** sono strutture dati che possono contenere membri dati e membri funzione. A differenza delle classi, tuttavia, i tipi struct sono tipi valore e non richiedono l'allocazione dell'heap. Una variabile di un tipo struct archivia direttamente i relativi dati, mentre una variabile di un tipo classe archivia un riferimento a un oggetto allocato in modo dinamico. I tipi struct non supportano l'ereditarietà specificata dall'utente. Tutti i tipi struct ereditano implicitamente dal tipo <xref:System.ValueType>, che a sua volta eredita implicitamente da `object`.

I tipi struct sono particolarmente utili per strutture dati di piccole dimensioni che hanno una semantica di valori. I numeri complessi, i punti di un sistema di coordinate o le coppie chiave-valore di un dizionario sono buoni esempi di struct. L'uso dei tipi struct al posto delle classi può determinare una notevole differenza riguardo al numero di allocazioni di memoria eseguite da un'applicazione. Il programma seguente, ad esempio, crea e inizializza una matrice di 100 punti. Con `Point` implementato come classe, vengono create istanze di 101 oggetti separati, uno per la matrice e uno per ciascuno dei 100 elementi.

[!code-csharp[PointClassUse](../../../samples/snippets/csharp/tour/structs/Program.cs#L5-L13)]

Un'alternativa consiste nel trasformare Point in un tipo struct.

[!code-csharp[PointStruct](../../../samples/snippets/csharp/tour/structs/Point.cs#L3-L11)]

Viene ora creata un'istanza di un solo oggetto, quello relativo alla matrice, e le istanze di `Point` vengono memorizzate inline nella matrice.

Con il nuovo operatore vengono chiamati i costruttori di struct, ma questo non implica l'allocazione della memoria. Anziché allocare dinamicamente un oggetto e restituire un riferimento a quest'ultimo, un costruttore di struct restituisce semplicemente il valore del tipo struct (in genere una posizione temporanea nello stack), che viene quindi copiato in base alle esigenze.

Con le classi, due variabili possono fare riferimento allo stesso oggetto e pertanto le operazioni su una variabile possono influire sull'oggetto a cui fa riferimento l'altra. Con i tipi struct, ogni variabile ha una propria copia dei dati e le operazioni su una variabile non possono influire sull'altra. Ad esempio, l'output generato dal segmento di codice seguente dipende dal fatto che l'oggetto Point sia una classe o un tipo struct.

[!code-csharp[PointUse](../../../samples/snippets/csharp/tour/structs/Program.cs#L19-L22)]

Se `Point` è una classe, l'output è 20 perché a e b fanno riferimento allo stesso oggetto. Se Point è un tipo struct, l'output è 10 perché l'assegnazione di `a` a `b` crea una copia del valore e tale copia non è interessata dalla successiva assegnazione a `a.x`.

L'esempio precedente evidenzia due delle limitazioni dei tipi struct. In primo luogo, la copia di un intero tipo struct è in genere meno efficiente della copia di un riferimento all'oggetto. Di conseguenza, il passaggio dei parametri di assegnazione e valore può risultare molto più costoso con i tipi struct che con i tipi riferimento. In secondo luogo, ad eccezione dei parametri `ref` e `out`, non è possibile creare riferimenti ai tipi struct e questa condizione che ne limita l'uso in varie situazioni.

>[!div class="step-by-step"]
[Precedente](classes-and-objects.md)
[Successivo](arrays.md)

