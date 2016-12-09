---
title: Frameworks e destinazioni
description: Illustra i concetti relativi alle destinazioni dei framework durante la scrittura di codice .NET.
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 09/19/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 6ef56a2e-593d-497b-925a-1e25bb6df2e6
translationtype: Human Translation
ms.sourcegitcommit: 38561c2d25c6950d166bf706f4306c867e683b04
ms.openlocfilehash: 82ba6f4abe200dc48158eac1ad3e3609feeda2c9

---

# <a name="frameworks-and-targets"></a>Frameworks e destinazioni

L'ecosistema .NET si basa su un concetto di framework. I framework definiscono l'API che è possibile usare per una particolare piattaforma. .NET Framework 4.6 è una di queste piattaforme. I framework vengono usati in Visual Studio e in altri IDE ed editor per offrire il set corretto di API. Vengono anche usati da NuGet, per la produzione e l'uso dei pacchetti NuGet, per garantire la creazione e l'uso di pacchetti appropriati (e attività incluse) per il framework di destinazione. I framework possono essere considerati come una delle valute principali nell'ecosistema .NET. Il concetto è disponibile per correttezza per evitare a società e clienti di visualizzare @System.MissingMethodException in fase di esecuzione.

## <a name="framework-versions"></a>Versioni di framework

La tabella seguente definisce il set di framework che è possibile usare, come si creano i relativi riferimenti e quale versione della [libreria standard di .NET](library.md) viene implementata.

| Framework | Ultima versione | Moniker della versione di .NET Framework di destinazione (TFM, Target Framework Moniker) | Moniker compatto della versione di .NET Framework di destinazione (TFM, Target Framework Moniker) | Versione standard di .NET | Metapackage |
|:--------: | :--: | :--: | :--: | :--: | :--: | :--: |
| .NET Standard | 1.6 | .NET Standard, versione=1.6 | netstandard1.6 | N/D | [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library)|
| Applicazione .NET Core | 1.0.1 | . NETCoreApp, versione = 1.0 | netcoreapp1.0 | 1.6 | [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App)|
| .NET Framework | 4.6.2 | .NETFramework, versione=4.6.2 | net462 | 1,5 | N/D |

> [!NOTE]
> Queste versioni di framework sono le versioni stabili più recenti. È possibile che siano anche disponibili versioni di prova non descritte in questa tabella.

## <a name="writing-about-frameworks"></a>Riferimento ai framework

Esistono diversi modi per fare riferimento a framework in forma scritta, la maggior parte dei quali è usata in questa documentazione. Vengono descritti di seguito, come legenda per interpretare la documentazione e anche come guida per altri documenti.

Con .NET Framework 4.6.1 come esempio, è possibile usare i seguenti modi:

**Riferimento a un prodotto**

È possibile fare riferimento a una piattaforma .NET o runtime.

- ".NET Framework 4.6.1"

**Riferimento a un framework**

È possibile fare riferimento a un framework o alla destinazione di un framework tramite forme brevi o lunghe del TFM. Entrambi sono ugualmente validi in generale.

- `.NETFramework,Version=4.6.1`
- `net461`

**Riferimento a una famiglia di framework**

È possibile fare riferimento a una famiglia di framework tramite forme brevi o lunghe dell'ID del framework. Entrambi sono ugualmente validi in generale.

- `.NETFramework`
- `net`



<!--HONumber=Nov16_HO3-->


