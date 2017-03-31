---
title: Enumerazioni C# | Panoramica del linguaggio C#
description: Informazioni sulle enumerazioni, costanti discrete denominate in C#
keywords: .NET, csharp
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 7faba1cc-6ea9-4a19-adb9-0335e4b132e5
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 677fd5fb931cca704fa6a0550a229ebb2fccdd7a
ms.lasthandoff: 03/13/2017

---
    
# <a name="enums"></a>Enumerazioni

Un ***tipo enum*** è un tipo valore distinto con un set di costanti denominate. Le enumerazioni vengono definite quando è necessario specificare un tipo che può avere un set di valori discreti. Le enumerazioni usano uno dei tipi valore integrali come archiviazione sottostante e offrono significato semantico ai valori discreti.

Nell'esempio seguente viene dichiarato e usato un tipo `enum` denominato `Color` con tre valori di costante, `Red`, `Green` e `Blue`.

[!code-csharp[Esempio enum](../../../samples/snippets/csharp/tour/enums/Program.cs#L3-L36)]

Ogni tipo `enum` ha un tipo integrale corrispondente, denominato ***tipo sottostante*** del tipo `enum`. Un tipo `enum` che non dichiara in modo esplicito un tipo sottostante ha un tipo sottostante di `int`. Il formato di archiviazione di un tipo `enum` e l'intervallo di valori possibili sono determinati dal tipo sottostante. Il set di valori che un tipo `enum` può richiedere non è limitato dai relativi membri `enum`. In particolare, è possibile eseguire il cast di qualsiasi valore del tipo sottostante di un tipo `enum` al tipo `enum`. Si tratta di un valore valido distinto del tipo `enum` in questione.

Nell'esempio seguente viene dichiarato un tipo `enum` denominato `Alignment` con un tipo sottostante di `sbyte`.

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L38-L43)]

Come mostrato dall'esempio precedente, una dichiarazione di membro `enum` può includere un'espressione costante che specifica il valore del membro stesso. Il valore della costante di ciascun membro `enum` deve essere compreso nell'intervallo del tipo sottostante di `enum`. Quando una dichiarazione di membro `enum` non specifica in modo esplicito un valore, al membro viene assegnato il valore zero (se è il primo membro del tipo `enum`) o il valore del membro `enum` testualmente precedente più uno.

I valori `Enum` possono essere convertiti in valori integrali e viceversa usando i cast di tipo. Ad esempio:

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L49-L50)]

Il valore predefinito di qualsiasi tipo `enum` è il valore integrale zero convertito nel tipo `enum`. Nei casi in cui le variabili vengono inizializzate automaticamente con un valore predefinito, tale valore viene assegnato alle variabili dei tipi `enum`. Per rendere facilmente disponibile il valore predefinito di un tipo `enum`, il valore letterale `0` viene implicitamente convertito in qualsiasi tipo `enum`. Di conseguenza, quanto riportato di seguito è consentito.

[!code-csharp[Enum zero](../../../samples/snippets/csharp/tour/enums/Program.cs#L58-L58)]

>[!div class="step-by-step"]
[Precedente](interfaces.md)
[Successivo](delegates.md)

