---
title: Panoramica della programmazione asincrona
description: Panoramica della programmazione asincrona
keywords: .NET, .NET Core
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: fb9940e56b5d0e8f4474584102f2e6167a79f291
ms.lasthandoff: 03/02/2017

---

# <a name="async-overview"></a>Panoramica della programmazione asincrona

Fino a non molto tempo fa, per avere app più veloci bastava acquistare un nuovo PC o server. Ad un certo punto, però, questa tendenza si è fermata. Anzi, si è invertita. Sono comparsi telefoni cellulari con chip ARM a core singolo da 1ghz e i carichi di lavoro dei server si sono spostati sulle macchine virtuali. Gli utenti vogliono interfacce a velocità di risposta elevata e i titolari di business vogliono server scalabili in base alle loro attività aziendali. Il passaggio ai dispositivi mobili e cloud e una popolazione connessa a Internet che ormai supera i&3; miliardi di utenti, hanno avuto come risultato lo sviluppo di nuovi modelli di software. 

* Ci si aspetta che le applicazioni client siano sempre attive, sempre connesse e costantemente reattive all'interazione dell'utente, ad esempio al tocco, con valutazioni dell'archivio applicazioni sempre ottime.
* Ci si attende dai servizi che sappiano gestire i picchi di traffico scalando verticalmente e orizzontalmente senza intoppi. 

La programmazione asincrona è una tecnica fondamentale che semplifica la gestione di pesanti operazioni I/O simultanee su diversi core. .NET offre ad app e servizi la capacità di garantire velocità di risposta ed elasticità grazie a modelli di programmazione asincrona a livello di linguaggio facili da usare in C#, VB e F#.

## <a name="why-write-async-code"></a>Perché scrivere codice asincrono?

Le app moderne fanno un uso intensivo di I/O file e rete. Le API I/O solitamente si bloccano per impostazione predefinita, con conseguenti esperienze utente e uso dell'hardware poco soddisfacenti, a meno che non si voglia imparare a usare modelli complessi. Le API asincrone e il modello di programmazione asincrona a livello di linguaggio invertono questa tendenza, rendendo l'esecuzione asincrona predefinita, con pochi concetti nuovi da apprendere.

Il codice asincrono ha le caratteristiche seguenti:

* Gestisce più richieste server cedendo i thread per gestire più richieste durante l'attesa del ritorno delle richieste I/O.
* Consente alle interfacce utente di essere più reattive, cedendo thread all'interazione dell'interfaccia utente durante l'attesa delle richieste I/O e spostando le attività con esecuzione prolungata ad altri core della CPU.
* Molte delle API di .NET più recenti sono asincrone.
* Scrivere codice asincrono in .NET è estremamente facile.

## <a name="whats-next"></a>Passaggi successivi

Per un approfondimento dei concetti della programmazione asincrona, vedere [La programmazione asincrona in dettaglio](async-in-depth.md).


