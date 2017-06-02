---
title: Gestione delle eccezioni (F#)
description: Gestione delle eccezioni (F#)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: ad475c4a-d94e-47d9-b27b-3ff000b65f8e
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: d95aca8c511524f0b9af67b34a5999f885cf3aaf
ms.lasthandoff: 04/05/2017

---

# <a name="exception-handling"></a>Gestione delle eccezioni

Questa sezione contiene informazioni sul supporto di gestione delle eccezioni nel linguaggio F#.


## <a name="exception-handling-basics"></a>Nozioni fondamentali sulla gestione delle eccezioni
La gestione delle eccezioni è il modo standard per la gestione delle condizioni degli errori in .NET Framework. Qualsiasi linguaggio .NET deve quindi supportare questo meccanismo, incluso F#. Un'*eccezione* è un oggetto che incapsula informazioni su un errore. Quando si verificano errori, vengono generate eccezioni e viene interrotta l'esecuzione normale. Il runtime cerca invece un gestore appropriato per l'eccezione. La ricerca inizia nella funzione corrente e procede verso l'alto attraverso i livelli di chiamanti fino a quando non viene trovato un gestore corrispondente. Quindi viene eseguito il gestore.

Mentre lo stack viene rimosso, il runtime esegue anche tutti i codice nei blocchi `finally` per garantire che gli oggetti vengano puliti correttamente durante il processo di rimozione.


## <a name="related-topics"></a>Argomenti correlati

|Titolo|Descrizione|
|-----|-----------|
|[Tipi di eccezione](exception-types.md)|Descrive come dichiarare un tipo di eccezione.|
|[Eccezioni: espressione `try...with`](the-try-with-expression.md)|Descrive il costrutto di linguaggio che supporta la gestione delle eccezioni.|
|[Eccezioni: espressione `try...finally`](the-try-finally-expression.md)|Descrive il costrutto di linguaggio che consente di eseguire il codice di pulizia mentre lo stack viene rimosso se viene generata un'eccezione.|
|[Eccezioni: funzione `raise`](the-raise-Function.md)|Descrive come generare un oggetto eccezione.|
|[Eccezioni: funzione `failwith`](the-failwith-function.md)|Descrive come generare un'eccezione F# generale.|
|[Eccezioni: funzione `invalidArg`](the-invalidArg-function.md)|Descrive come generare un'eccezione di argomento non valido.|
