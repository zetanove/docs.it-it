---
title: Componenti dell&quot;architettura .NET
description: Vengono descritti i componenti dell&quot;architettura .NET, ad esempio la libreria .NET Standard, i runtime .NET e gli strumenti.
keywords: .NET, libreria .NET Standard, .NET Standard, .NET Core, .NET Framework, Xamarin, MSBuild, C#, F#, VB, compilatori
author: cartermp
manager: wpickett
ms.author: cartermp
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2e38e9d9-8284-46ee-a15f-199adc4f26f4
translationtype: Human Translation
ms.sourcegitcommit: 254e89abefd28419bd2f36a047e4df939f7ff8da
ms.openlocfilehash: d0cd8f44876038167db23e7fd1e5a893460f3d73

---

# <a name="net-architectural-components"></a>Componenti dell'architettura .NET

.NET è costituito da diversi componenti principali.  È presente una libreria standard, denominata libreria .NET Standard, costituita da un ampio set di API eseguibili in qualsiasi ambiente.  Questa libreria standard è implementata da tre runtime .NET: .NET Framework, .NET Core e Mono per Xamarin.  Anche i linguaggi .NET possono essere eseguiti in qualsiasi runtime .NET.  Su ciascuna piattaforma sono inoltre disponibili strumenti che consentono di compilare i progetti.  Questi strumenti sono gli stessi, indipendentemente dal runtime scelto.

Di seguito è riportata una rappresentazione grafica di ciascuno dei componenti .NET menzionati in precedenza e della loro collocazione nell'architettura.

![Visualizzazione di insieme di tutti i componenti dell'architettura .NET](media/components.png)

Di seguito è riportata una breve spiegazione di ciascuno dei componenti chiave riportati nella figura precedente.  

## <a name="net-standard-library"></a>Libreria .NET Standard

La libreria .NET Standard è costituita da un set di API implementate da un runtime .NET.

In termini più formali, si tratta di una specifica di API .NET che costituiscono un set di contratti in base a cui viene compilato il codice.  Questi contratti dispongono di implementazioni sottostanti per ogni runtime .NET.  Questo consente la portabilità tra differenti runtime .NET, assicurando la possibilità di eseguire il codice su qualsiasi piattaforma.

La libreria .NET Standard è anche una destinazione di compilazione, dove è nota come .NET Standard.  Attualmente è possibile definire come destinazione .NET Standard 1.0-1.6.  Se il codice ha come destinazione una versione di .NET Standard, può essere eseguito su qualsiasi runtime .NET che implementa tale versione.

Per altre informazioni sulla libreria .NET Standard e su come definire .NET Standard come destinazione, vedere [Libreria .NET Standard](library.md).

## <a name="net-runtimes"></a>Runtime .NET

Microsoft sviluppa e gestisce attivamente tre runtime .NET principali: .NET Core, .NET Framework e Mono per Xamarin.

### <a name="net-core"></a>.NET Core

.NET Core è un runtime multipiattaforma ottimizzato per carichi di lavoro server.  Implementa la libreria .NET Standard, pertanto qualsiasi codice che ha come destinazione .NET Standard può essere eseguito su .NET Core.  Si tratta del runtime usato da ASP.NET Core e dalla piattaforma UWP (Universal Windows Platform).  È moderno, efficiente e progettato per gestire carichi di lavoro server e cloud su larga scala.

Per altre informazioni su .NET Core, vedere [Guida a .NET Core](../core/index.md).

### <a name="net-framework"></a>.NET Framework

.NET Framework è il runtime .NET "storico", esistente dal 2002.  È lo stesso .NET Framework che gli sviluppatori .NET hanno sempre usato.  Questo runtime implementa la libreria .NET Standard, pertanto qualsiasi codice che ha come destinazione .NET Standard può essere eseguito su .NET Framework.  Contiene API aggiuntive specifiche di Windows, ad esempio API per lo sviluppo di applicazioni desktop di Windows con Windows Forms e WPF.  .NET Framework è ottimizzato per la compilazione di applicazioni desktop di Windows.

Per altre informazioni su .NET Framework, vedere [Guida a .NET Framework](../framework/index.md).

### <a name="mono-for-xamarin"></a>Mono per Xamarin

Mono è il runtime usato dalle app Xamarin.  Implementa la libreria .NET Standard, pertanto qualsiasi codice che ha come destinazione .NET Standard può essere eseguito su app Xamarin.  Contiene API aggiuntive per iOS, Android, Xamarin.Forms e Xamarin.Mac.  È ottimizzato per la creazione di applicazioni per dispositivi mobili in iOS e Android.

Per altre informazioni su Mono, vedere la [documentazione Mono](http://www.mono-project.com/docs/).

## <a name="net-tooling-and-common-infrastructure"></a>Strumenti .NET e infrastruttura comune

Gli strumenti per .NET sono comuni in tutte le implementazioni di .NET.  Includono, tra l'altro, quanto riportato di seguito:

* Linguaggi .NET e relativi compilatori
* Componenti del runtime, ad esempio JIT e Garbage Collector
* Sistema di progetto .NET (talvolta noto come "csproj", "vbproj" o "fsproj")
* MSBuild, il motore di compilazione usato per compilare i progetti
* NuGet, il gestore di pacchetti Microsoft per .NET
* L'interfaccia della riga di comando .NET, un'interfaccia della riga di comando multipiattaforma per la compilazione dei progetti .NET
* Strumenti open source di orchestrazione della compilazione, ad esempio CAKE e FAKE

Il vantaggio principale è la disponibilità di una vasta gamma di strumenti e tipologie di infrastruttura comuni per qualsiasi versione di .NET scelta per la compilazione delle app.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere gli argomenti seguenti:

* [Libreria .NET Standard](library.md)
* [Guida a .NET Core](../core/index.md)
* [Guida a .NET Framework](../framework/index.md)
* [Guida a C#](../csharp/index.md)
* [Guida a F#](../csharp/index.md)
* [Guida a VB.NET](../csharp/index.md)


<!--HONumber=Nov16_HO3-->


