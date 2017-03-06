---
title: Supporto di .NET Core | Microsoft Docs
description: Informazioni sui diversi rami di rilascio (LTS e Current) per il supporto di .NET Core
keywords: .NET, .NET Core, lts, current, fts, supporto, rami di rilascio, percorsi di rilascio, ciclo di vita, rami di versioni
author: kendrahavens
ms.author: mairaw
ms.date: 01/30/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: fedc7025-f320-4cba-957b-ef74885f66de
translationtype: Human Translation
ms.sourcegitcommit: 1ef17b16b85c81a0b96bb1712db3734dc67d801d
ms.openlocfilehash: 582a521e6a30b740465890b6cb8c773061a98ea6

---

# <a name="net-core-support"></a>Supporto di .NET Core

Questa è una descrizione generale del supporto di .NET Core.

## <a name="lts-and-current-release-trains"></a>Rami di rilascio LTS e Current

La disponibilità di due rami di rilascio per il supporto è un concetto comune ampiamente usato nel mondo del software, in particolare per progetti open source come .NET Core. .NET Core offre i rami di rilascio per il supporto seguenti: [LTS (Long Term Support)](https://en.wikipedia.org/wiki/Long-term_support) e Current. Le versioni LTS vengono mantenute aggiornate per la stabilità per l'intero ciclo di vita e ricevono correzioni di problemi importanti e correzioni per la sicurezza. L'aggiunta di nuove funzionalità e altre correzioni di bug vengono effettuate nelle versioni Current. Dal punto di vista del supporto, questi rami di rilascio hanno gli attributi seguenti in relazione al ciclo di vita del supporto.

Le versioni LTS sono
* Supportate per tre anni dopo la data di disponibilità generale di una versione LTS
* Oppure supportate per un anno dopo la data di disponibilità generale di una versione LTS successiva

Le versioni Current sono
* Supportate all'interno della stessa finestra di tre anni della versione LTS padre
* Supportate per tre mesi dopo la data di disponibilità generale di una versione Current successiva
* E supportate per un anno dopo la data di disponibilità generale di una versione LTS successiva

## <a name="versioning"></a>Versionamento
Le nuove versioni LTS sono contrassegnate tramite un incremento del numero di versione principale. Le versioni Current hanno lo stesso numero di versione principale del ramo LTS corrispondente e sono contrassegnate tramite un incremento del numero di versione secondario. Ad esempio, il numero di versione 1.0.3 per il ramo LTS e il numero 1.1.0 per Current. Gli aggiornamenti per correzioni di bug per entrambi i rami incrementano la versione di patch. Per altre informazioni sullo schema di controllo delle versioni, vedere [Versionamento di .NET Core](index.md).

## <a name="what-causes-updates-in-lts-and-current-trains"></a>Quali modifiche comportano aggiornamenti dei rami LTS e Current?
Per comprendere le modifiche specifiche, ad esempio correzioni di bug o l'aggiunta di API, che causano aggiornamenti dei numeri di versione, vedere la sezione Albero delle decisioni nella [documentazione sul controllo delle versioni](index.md). Non esiste un set di regole fisso per determinare le modifiche che vengono integrate nel ramo LTS dal ramo Current. In genere, gli aggiornamenti della sicurezza e le patch necessari per ottenere il comportamento previsto sono motivi validi per aggiornare il ramo LTS. È anche intenzione di Microsoft supportare i sistemi operativi desktop recenti per gli sviluppatori nel ramo LTS, anche se ciò potrebbe non essere sempre possibile. Un buon modo per scoprire quali API, correzioni e sistemi operativi sono supportati in una determinata versione consiste nel consultare le [note sulla versione](https://github.com/dotnet/core/tree/master/release-notes) corrispondenti su GitHub.

### <a name="further-reading"></a>Ulteriori informazioni
* [.NET Core Support Lifecycle Fact Sheet (Scheda informativa sul ciclo di supporto per .NET Core)](https://www.microsoft.com/net/core/support)
* [Sistemi operativi e versioni attualmente supportati](https://github.com/dotnet/core/blob/master/roadmap.md)


<!--HONumber=Feb17_HO1-->


