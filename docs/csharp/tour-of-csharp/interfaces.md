---
title: Interfacce C# | Panoramica del linguaggio C#
description: Le interfacce definiscono contratti implementati dai tipi in C#
keywords: ".NET, csharp, interfacce, ereditarietà multipla, polimorfismo"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a9bf82f4-efd1-4216-bd34-4ef0fa48c968
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 477db71cb3226247c7a13dbd9febd00c87f5c154
ms.lasthandoff: 03/13/2017

---

# <a name="interfaces"></a>Interfacce

Un'***interfaccia*** definisce un contratto che può essere implementato da classi e struct. Può contenere metodi, proprietà, eventi e indicizzatori. Un'interfaccia non fornisce le implementazioni dei membri che definisce, ma specifica semplicemente i membri che devono essere forniti dalle classi o dai tipi struct che la implementano.

Le interfacce possono usare l'***ereditarietà multipla***. Nell'esempio seguente l'interfaccia `IComboBox` eredita da `ITextBox` e `IListBox`.

[!code-csharp[InterfacesOne](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L5-L17)]

Classi e struct possono implementare più interfacce. Nell'esempio seguente la classe `EditBox` implementa `IControl` e `IDataBound`.

[!code-csharp[InterfacesTwo](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L19-L27)]

Quando una classe o un tipo struct implementa un'interfaccia specifica, le istanze di tale classe o struct possono essere convertite in modo implicito in quel tipo di interfaccia. Esempio:

[!code-csharp[InterfacesThree](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L33-L35)]

Nei casi in cui un'istanza non implementa staticamente un'interfaccia specifica è possibile usare cast di tipo dinamico. Le istruzioni seguenti usano ad esempio cast di tipo dinamico per ottenere implementazioni delle interfacce `IControl` e `IDataBound` di un oggetto. Poiché il tipo effettivo in fase di esecuzione dell'oggetto è `EditBox`, i cast vengono eseguiti correttamente.

[!code-csharp[InterfacesFour](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L40-L42)]

Nella classe `EditBox` precedente il metodo `Paint` dell'interfaccia `IControl` e il metodo `Bind` dell'interfaccia `IDataBound` vengono implementati usando membri pubblici. C# supporta anche ***implementazioni di un membro dell'interfaccia*** esplicite, che consentono alla classe o al tipo struct di evitare di rendere pubblici i membri. Un'implementazione esplicita di un membro dell'interfaccia viene scritta usando il nome completo del membro dell'interfaccia. La classe `EditBox` può ad esempio implementare i metodi `IControl.Paint` e `IDataBound.Bind` usando implementazioni esplicite di un membro dell'interfaccia, come indicato di seguito.

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L60-L64)]

È possibile accedere ai membri dell'interfaccia esplicita solo tramite il tipo di interfaccia. Ad esempio, l'implementazione del metodo `IControl.Paint` fornito dalla classe EditBox precedente può essere richiamata solo dopo che è stato convertito il riferimento `EditBox` al tipo di interfaccia `IControl`.

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L71-L74)]

>[!div class="step-by-step"]
[Precedente](arrays.md)
[Successivo](enums.md)

