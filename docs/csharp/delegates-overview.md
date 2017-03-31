---
title: Introduzione ai delegati
description: Introduzione ai delegati
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 59b61d77-84e5-457b-8da5-fb5f24ca6ed6
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f68742a02ebf12e222b2fa6827352a3684de5648
ms.lasthandoff: 03/13/2017

---

# <a name="introduction-to-delegates"></a>Introduzione ai delegati

[Precedente](delegates-events.md)

I delegati offrono un meccanismo di *associazione tardiva* in .NET. L'associazione tardiva indica la creazione di un algoritmo in cui il chiamante specifica almeno un metodo che implementa parte dell'algoritmo.

Ad esempio, si consideri l'ordinamento di un elenco di stelle in un'applicazione di astronomia.
È possibile scegliere di ordinare le stelle in base alla distanza da terra, alla grandezza o alla luminosità percepita.

In tutti i casi, il metodo Sort() esegue essenzialmente la stessa operazione, ovvero ordina gli elementi nell'elenco in base a un confronto. Il codice che esegue il confronto di due stelle è diverso per ognuno degli ordinamenti.

Questi tipi di soluzioni sono stati usati nel software per mezzo secolo.
Il concetto di delegato del linguaggio C# offre un supporto del linguaggio di prima classe e indipendenza dai tipi.

Come descritto più avanti, il codice C# scritto per questo tipo di algoritmi è indipendente dai tipi e usa il linguaggio e il compilatore per verificare che i tipi corrispondano per gli argomenti e i tipi restituiti.

## <a name="language-design-goals-for-delegates"></a>Obiettivi della progettazione del linguaggio per i delegati

I designer del linguaggio hanno enumerato diversi obiettivi per la funzionalità che in seguito è diventata la funzionalità dei delegati.

Il team voleva un costrutto di linguaggio comune che potesse essere usato per i successivi algoritmi di associazione tardiva. Ciò consente agli sviluppatori di apprendere un solo concetto e di usare lo stesso concetto in diversi problemi software.

Inoltre, il team voleva che fossero supportate le chiamate al metodo singole e multicast. I delegati multicast sono i delegati nei quali sono stati concatenati più metodi. Gli esempi sono descritti [di seguito](delegate-class.md). 

Il team voleva che i delegati supportassero la stessa indipendenza dai tipi stesso che gli sviluppatori si aspettano da tutti i costrutti C#. 

Il team ha infine riconosciuto che un modello di evento è un modello specifico in cui i delegati o gli algoritmi di associazione tardiva successivi sono utili. Il team voleva assicurarsi che il codice per i delegati potesse offrire la base per il modello di evento di .NET.

Il risultato di tutto il lavoro sono stati il delegato e il supporto degli eventi di C# e .NET. Gli articoli rimanenti di questa sezione descrivono le funzionalità del linguaggio, il supporto delle librerie e i termini comuni usati per i delegati.

Verranno fornite informazioni sulla parola chiave `delegate` e sul codice generato dalla parola chiave. Verranno fornite informazioni sulle funzionalità nella classe `System.Delegate` e sul loro utilizzo. Si apprenderà come creare delegati indipendenti dai tipi e come creare metodi che possono essere richiamati tramite i delegati. Si apprenderà anche come usare i delegati e gli eventi tramite le espressioni lambda. Sarà possibile osservare il punto nel quale i delegati diventano uno dei blocchi predefiniti per LINQ. Si apprenderà come delegati costituiscono la base per lo schema di eventi .NET e come sono diversi.

In generale, sarà possibile osservare in che modo i delegati sono parte integrante della programmazione in .NET e dell'uso con le API del framework.

Ma veniamo al dunque.

[Successivo](delegate-class.md)

