---
title: Libreria .NET Standard
description: Libreria .NET Standard
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c044882c-af15-45f2-96d1-534557a5ee9b
ms.translationtype: Human Translation
ms.sourcegitcommit: 633dcc6d966125139cb21c4e70dac4d4794ee9a4
ms.openlocfilehash: da326fb823c16c7795a6a05ad302c13918b435aa
ms.contentlocale: it-it
ms.lasthandoff: 03/20/2017

---

# <a name="net-standard-library"></a>Libreria .NET Standard

La libreria .NET Standard è una specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET. La motivazione alla base della libreria Standard è l'esigenza di creare maggiore uniformità nell'ecosistema .NET. Lo standard [ECMA 335](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) continua ad assicurare uniformità riguardo al comportamento del runtime .NET, ma non esiste una specifica simile per le BCL (Base Class Library) .NET per le implementazioni delle librerie .NET. 

La libreria .NET Standard abilita gli scenari chiave seguenti: 

- Definisce un set uniforme di API BCL per tutte le piattaforme .NET da implementare, indipendentemente dal carico di lavoro.
- Consente agli sviluppatori di creare librerie portabili utilizzabili in più runtime .NET usando questo stesso set di API.
- Riduce e (auspicabilmente) elimina la compilazione condizionale del codice sorgente condiviso a causa di API .NET (solo per API del sistema operativo).

I diversi runtime .NET implementano versioni specifiche della libreria .NET Standard. Ciascuna versione del runtime .NET annuncia la versione .NET Standard più recente supportata, implicando che sono supportate anche le versioni precedenti. NET Framework 4.6, ad esempio, implementa la libreria .NET Standard 1.3: questo significa che espone tutte le librerie definite nelle versioni della libreria .NET Standard da 1.0 a 1.3. Analogamente, .NET Framework 4.6.2 implementa la libreria .NET Standard 1.5, mentre .NET Core 1.0 implementa la libreria .NET Standard 1.6.

## <a name="net-platforms-support"></a>Supporto di piattaforme .NET

Di seguito è riportato l'intero set di runtime .NET che supporta la libreria .NET Standard.

| Nome della piattaforma | Alias |  |  |  |  |  | | | |
| :---------- | :--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|.NET Standard | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1,5 | 1.6 | 2.0 |
|.NET Core|netcoreapp|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|1.0|2.0|
|.NET Framework|net|&rarr;|4.5|4.5.1|4.6|4.6.1|4.6.2|vNext|4.6.1|
|Piattaforme Mono/Xamarin||&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|vNext|
|Piattaforma UWP (Universal Windows Platform)|uap|&rarr;|&rarr;|&rarr;|&rarr;|10.0|&rarr;|&rarr;|vNext|
|Windows|win|&rarr;|8.0|8.1||||||
|Windows Phone|wpa|&rarr;|&rarr;|8.1||||||
|Silverlight per Windows Phone|wp|8.0||||||||

## <a name="comparison-to-portable-class-libraries"></a>Confronto con le librerie di classi portabili

È possibile considerare la libreria .NET Standard come la prossima generazione di [libreria di classi portabile](https://msdn.microsoft.com/library/gg597391.aspx). La libreria .NET Standard migliora l'esperienza di creazione delle librerie portabili curando una BCL standard e assicurando di conseguenza una maggiore uniformità tra i runtime .NET. Una libreria che ha come destinazione la libreria .NET Standard è una libreria di classi portabile o una "libreria di classi portabile basata su .NET". Le librerie di classi portabili esistenti sono "librerie di classi portabili basate sul profilo".

La libreria .NET Standard e i profili delle librerie di classi portabili sono stati creati per scopi simili, ma presentano differenze significative.

Analogie:

- Definisce le API che possono essere usate per la condivisione di codice binario.

Differenze:

- La libreria .NET Standard è un set curato di API, mentre i profili delle librerie di classi portabili sono definiti da intersezioni delle piattaforme esistenti.
- La definizione delle versioni della libreria .NET Standard è lineare, mentre quella dei profili delle librerie di classi portabili non lo è.
- I profili delle librerie di classi portabili rappresentano piattaforme Microsoft, mentre la libreria .NET Standard è indipendente dalla piattaforma.

## <a name="specification"></a>Specifica

La specifica della libreria .NET Standard è un set standardizzato di API. La specifica viene gestita dagli implementatori dei runtime .NET, in particolare Microsoft (sono inclusi .NET Framework, .NET Core e Mono) e Unity. Un processo pubblico di commenti e suggerimenti è parte integrante della creazione di nuove versioni della libreria .NET Standard.

### <a name="official-artifacts"></a>Elementi ufficiali

La specifica ufficiale è un insieme di file con estensione cs che definiscono le API che sono parte dello standard. La [directory ref](https://github.com/dotnet/corefx/tree/master/src/System.Runtime/ref) di ciascun [componente](https://github.com/dotnet/corefx/tree/master/src) definisce le API della libreria .NET Standard. Anche se si trovano nel [repository CoreFX](https://github.com/dotnet/corefx), gli elementi di riferimento non sono specifici di .NET Core.

Il metapacchetto [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) ([origine](https://github.com/dotnet/standard/blob/master/netstandard/pkg/NETStandard.Library.dependencies.props)) descrive il set di librerie che definiscono (in parte) una o più versioni della libreria Standard.

Un componente specifico, ad esempio System.Runtime, descrive quanto segue:

- Parte della libreria .NET Standard (solo il relativo ambito).
- Diverse versioni della libreria .NET Standard per tale ambito.

Vengono forniti elementi derivati per facilitare le operazioni di lettura e abilitare alcuni scenari di sviluppo (ad esempio l'uso di un compilatore).

- Elenco di API in markdown (da definire)
- Assembly di riferimento, distribuiti come [pacchetti NuGet](../core/packages.md) e utilizzati come riferimento dal metapacchetto [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/).

### <a name="package-representation"></a>Rappresentazione dei pacchetti

Il principale veicolo di distribuzione degli assembly di riferimento della libreria .NET Standard sono i [pacchetti NuGet](../core/packages.md). Le implementazioni vengono fornite in molti modi diversi, appropriati per ciascun runtime .NET.

I pacchetti NuGet hanno come destinazione uno o più [framework](frameworks.md). I pacchetti della libreria .NET Standard hanno come destinazione il framework ".NET Standard". È possibile definire come destinazione il framework .NET Standard usando il `netstandard` [TFM (Target Framework Moniker) compatto](frameworks.md) (ad esempio `netstandard1.4`). Le librerie che devono essere eseguite in più runtime devono avere come destinazione questo framework. 

Il metapacchetto `NETStandard.Library` fa riferimento al set completo di pacchetti NuGet che definiscono la libreria .NET Standard.  Il modo più comune di definire `netstandard` come destinazione è fare riferimento a questo metapacchetto. Questo metapacchetto descrive e fornisce l'accesso alle circa 40 librerie .NET e alle API associate che definiscono la libreria .NET Standard. Per accedere ad API aggiuntive, è possibile fare riferimento ad altri pacchetti che hanno come destinazione `netstandard`. 

### <a name="versioning"></a>Versionamento

La specifica non è singola, ma costituisce un set di API a crescita incrementale e con definizione lineare delle versioni. La prima versione dello standard definisce un set di dati di riferimento delle API. Le versioni successive aggiungono nuove API ed ereditano quelle definite dalle versioni precedenti. Non esiste alcuna norma stabilita per la rimozione di API dallo standard.

La libreria .NET Standard non è specifica di alcun runtime .NET e non corrisponde allo schema di versionamento di alcuno di questi runtime.

Le API aggiunte a uno dei runtime (ad esempio, .NET Framework, .NET Core e Mono) possono essere prese in considerazione per l'aggiunta alla specifica, in particolare se sono state progettate per essere API fondamentali. Le nuove [versioni della libreria .NET Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md#list-of-net-corefx-apis-and-their-associated-net-platform-standard-version) vengono create sulla base delle versioni dei runtime .NET, consentendo di definire come destinazione nuove API da una libreria di classi portabile .NET Standard. I meccanismi di versionamento sono descritti in modo più dettagliato nell'articolo [.NET Core Versioning](../core/versions/index.md) (Versionamento di .NET Core).

Il versionamento della libreria .NET Standard è importante per l'utilizzo. Data una versione della libreria .NET Standard, è possibile usare librerie che hanno come destinazione la stessa versione o versioni precedenti. L'approccio seguente descrive il flusso di lavoro per l'uso di librerie di classi portabili della libreria .NET Standard, in particolare per la definizione della libreria .NET Standard come destinazione.

- Selezionare una versione della libreria .NET Standard da usare per la libreria di classi portabile.
- Usare librerie che dipendono dalla stessa versione della libreria .NET Standard o da versioni precedenti.
- Se viene individuata una libreria che dipende da una versione successiva della libreria .NET Standard, è necessario adottare la stessa versione oppure decidere di non usare tale libreria.

### <a name="pcl-compatibility"></a>Compatibilità della libreria di classi portabile

La libreria .NET Standard è compatibile con un sottoinsieme di profili delle librerie di classi portabili. Le versioni 1.0, 1.1 e 1.2 della libreria .NET Standard si sovrappongono a un set di profili delle librerie di classi portabili. Questa sovrapposizione è stata creata per due motivi:

- Consentire alle librerie di classi portabili basate su .NET Standard di fare riferimento a librerie di classi portabili basate sul profilo.
- Consentire alle librerie di classi portabili basate sul profilo di essere incluse in un pacchetto come librerie di classi portabili basate su .NET Standard.

La compatibilità delle librerie di classi portabili basate sul profilo è fornita dal pacchetto NuGet [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility). Questa dipendenza è obbligatoria quando si fa riferimento a pacchetti NuGet contenenti librerie di classi portabili basate sul profilo.

Le librerie di classi portabili basate sul profilo inserite in un pacchetto come `netstandard` sono più semplici da usare rispetto alle librerie di classi portabili basate sul profilo in pacchetti generici. `netstandard` è un pacchetto compatibile con gli utenti esistenti.

Di seguito è riportato il set di profili delle librerie di classi portabili compatibili con .NET Standard: 

| Profilo | Versione standard della piattaforma .NET |
| ---------| --------------- |
| Profile7 .NET Portable Subset (.NET Framework 4.5, Windows 8) | 1.1 |
| Profile31 .NET Portable Subset (Windows 8.1, Windows Phone Silverlight 8.1)| 1.0 |
| Profile32 .NET Portable Subset (Windows 8.1, Windows Phone 8.1) | 1.2 |
| Profile44 .NET Portable Subset (.NET Framework 4.5.1, Windows 8.1) | 1.2 |
| Profile49 .NET Portable Subset (.NET Framework 4.5, Windows Phone Silverlight 8) | 1.0 |
| Profile78 .NET Portable Subset (.NET Framework 4.5, Windows 8, Windows Phone Silverlight 8) | 1.0 |
| Profile84 .NET Portable Subset (Windows Phone 8.1, Windows Phone Silverlight 8.1) | 1.0 |
| Profile111 .NET Portable Subset (.NET Framework 4.5, Windows 8, Windows Phone 8.1) | 1.1 |
| Profile151 .NET Portable Subset (.NET Framework 4.5.1, Windows 8.1, Windows Phone 8.1) | 1.2 |
| Profile157 .NET Portable Subset (Windows 8.1, Windows Phone 8.1, Windows Phone Silverlight 8.1) | 1.0 |
| Profile259 .NET Portable Subset (.NET Framework 4.5, Windows 8, Windows Phone 8.1, Windows Phone Silverlight 8) | 1.0 |

## <a name="targeting-net-standard-library"></a>Definizione della libreria .NET Standard come destinazione

È possibile [creare librerie .NET Standard](../core/tutorials/libraries.md) usando una combinazione del framework `netstandard` e del metapacchetto NETStandard.Library. Sono disponibili esempi della [definizione della libreria .NET Standard come destinazione con strumenti .NET Core](../core/packages.md).

