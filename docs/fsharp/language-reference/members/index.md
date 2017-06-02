---
title: Membri (F#)
description: Membri (F#)
keywords: visual f#, f#, programmazione funzionale
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: e472f50a-4939-4e62-abbc-471f8f265790
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: fe14657b25d122296a6826daba37ea99b6ee64b4
ms.lasthandoff: 04/05/2017

---

# <a name="members"></a>Membri

Questa sezione illustra i membri dei tipi di oggetto F#.


## <a name="remarks"></a>Note
I *membri* sono funzionalità che fanno parte di una definizione di tipo e vengono dichiarati con la parola chiave `member`. I tipi di oggetto F#, ad esempio record, classi, unioni discriminate, interfacce e strutture, supportano i membri. Per altre informazioni, vedere [Record](../records.md), [Classi](../classes.md), [Unioni discriminate](../discriminated-Unions.md), [Interfacce](../interfaces.md) e [Strutture](../structures.md).

I membri in genere costituiscono l'interfaccia pubblica per un tipo, e per questo motivo sono pubblici, se non diversamente specificato. I membri possono anche essere dichiarati privati o interni. Per altre informazioni, vedere [Controllo di accesso](../access-Control.md). Le firme per i tipi possono anche essere usate per esporre o meno determinati membri di un tipo. Per altre informazioni, vedere [Firme](../signatures.md).

I campi privati e le associazioni `do`, usati solo con le classi, non sono membri veri, perché non fanno mai parte dell'interfaccia pubblica di un tipo e non sono dichiarati con la parola chiave `member`, però vengono descritti in questa sezione.


## <a name="related-topics"></a>Argomenti correlati


|Argomento|Descrizione|
|-----|-----------|
|[Associazioni `let` nelle classi](let-bindings-in-classes.md)|Descrive la definizione dei campi privati e le funzioni nelle classi.|
|[Associazioni `do` nelle classi](do-bindings-in-classes.md)|Descrive la specifica del codice di inizializzazione dell'oggetto.|
|[Proprietà](properties.md)|Descrive i membri di proprietà nelle classi e altri tipi.|
|[Proprietà indicizzate](indexed-properties.md)|Descrive le proprietà di tipo matrice nelle classi e altri tipi.|
|[Metodi](methods.md)|Descrive funzioni che sono membri di un tipo.|
|[Costruttori](constructors.md)|Descrive funzioni speciali che inizializzano oggetti di un tipo.|
|[Overload degli operatori](../operator-overloading.md)|Descrive la definizione di operatori personalizzati per i tipi.|
|[Eventi](events.md)|Descrive la definizione di eventi e il supporto di gestione degli eventi in F# .|
|[Campi espliciti: parola chiave `val`](explicit-fields-the-val-keyword.md)|Descrive la definizione dei campi non inizializzati in un tipo.|

