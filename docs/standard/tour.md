---
title: Panoramica di .NET
description: "Panoramica guidata di alcune delle principali funzionalità della piattaforma .NET."
keywords: .NET, .NET Core, panoramica, linguaggi di programmazione, unsafe, gestione della memoria, indipendenza dai tipi, asincrono
author: cartermp
ms.author: wiwagn
ms.date: 02/09/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
ms.translationtype: Machine Translation
ms.sourcegitcommit: d00f2096e0799107a8a2ff1d12274c6026d4c27a
ms.openlocfilehash: 50e5b333f892cf469e9f3fe57a0325ac6d8e641f
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

# <a name="tour-of-net"></a>Panoramica di .NET

.NET è una piattaforma di sviluppo con finalità generali  che offre varie funzionalità chiave, tra cui più linguaggi di programmazione, modelli di programmazione asincroni e simultanei e l'interoperabilità nativa, che consente l'esecuzione di un'ampia gamma di scenari su più piattaforme.

Questo articolo offre una panoramica guidata di alcune delle principali funzionalità della piattaforma .NET.

Per informazioni su tutti i componenti dell'architettura di .NET e sulle relative modalità d'uso, vedere [Componenti dell'architettura .NET](components.md).

## <a name="how-to-run-the-code-samples"></a>Come eseguire i codici di esempio

Per informazioni su come configurare un ambiente di sviluppo all'interno del quale eseguire i codici di esempio, vedere l'articolo [Introduzione](get-started.md).  È possibile copiare i codici di esempio da questa pagina e incollarli nel proprio ambiente per eseguirli. 

> [!NOTE]
In futuro, da questo sito di programmazione sarà possibile eseguire i codici di esempio direttamente nel proprio browser.

## <a name="programming-languages"></a>Linguaggi di programmazione

.NET supporta più linguaggi di programmazione.  I runtime .NET implementano l'[interfaccia della riga di comando](https://www.visualstudio.com/license-terms/ecma-c-common-language-infrastructure-standards/) (CLI, Common Language Infrastructure) che, tra altre cose, specifica un runtime indipendente dal linguaggio e l'interoperabilità di linguaggio.  In questo modo, è possibile scegliere qualsiasi linguaggio .NET per creare applicazioni e servizi in .NET.

Microsoft sviluppa e supporta attivamente tre linguaggi .NET: C#, F# e Visual Basic .NET. 

* C# è un linguaggio semplice, potente, indipendente dai tipi e orientato agli oggetti che mantiene al tempo stesso l'espressività e l'eleganza tipiche dei linguaggi di tipo C. Gli sviluppatori che hanno familiarità con C e linguaggi simili incontreranno pochi problemi ad adattarsi a C#.  Per altre informazioni su C#, vedere [Guida a C#](../csharp/index.md).

* F# è un linguaggio di programmazione multipiattaforma e funzionale che supporta anche la programmazione tradizionale imperativa e orientata agli oggetti.  Per altre informazioni su F#, vedere [Guida a F#](../fsharp/index.md).

* Visual Basic è un linguaggio semplice da apprendere che consente di creare una vasta gamma di applicazioni da eseguire in .NET.

## <a name="automatic-memory-management"></a>Gestione automatica della memoria

.NET usa [Garbage Collector](garbagecollection/index.md) per consentire la gestione automatica della memoria per i programmi.  Il Garbage Collector ha un approccio "lazy" alla gestione della memoria, anteponendo la velocità effettiva dell'applicazione alla raccolta immediata di memoria.  Per altre informazioni sul Garbage Collector di.NET, vedere [Principi fondamentali di Garbage Collection](garbagecollection/fundamentals.md).

Le due righe di codice seguenti allocano entrambe memoria:

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L1-L2)]

Non esiste una parola chiave analoga per deallocare la memoria, in quanto la deallocazione viene eseguita automaticamente quando il Garbage Collector recupera la memoria durante l'esecuzione pianificata.

Garbage Collector è solo uno dei servizi che consentono di garantire la *sicurezza della memoria*.  L'invariante di sicurezza della memoria è molto semplice: un programma garantisce la sicurezza della memoria se accede soltanto alla memoria che è stata allocata (e non liberata).  Ad esempio, il runtime assicura che i programmi non eseguano l'indicizzazione oltre la fine di una matrice o accedano a un campo fantasma oltre la fine di un oggetto.

Nell'esempio seguente il runtime genera un'eccezione `InvalidIndexException` per garantire la sicurezza della memoria.

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L4-L5)]

## <a name="working-with-unmanaged-resources"></a>Utilizzo di risorse non gestite

Alcuni oggetti fanno riferimento a *risorse non gestite*. Le risorse non gestite sono risorse che non vengono gestite automaticamente dal runtime di .NET.  Ad esempio, un handle di file è una risorsa non gestita.  Un oggetto @System.IO.FileStream è un oggetto gestito, ma fa riferimento a un handle di file, che non è gestito.  Dopo aver usato FileStream, è necessario rilasciare l'handle di file.

In .NET gli oggetti che fanno riferimento a risorse non gestite implementano l'interfaccia @System.IDisposable.  Dopo aver usato l'oggetto, è possibile chiamare il metodo @System.IDisposable.Dispose dell'oggetto, che è responsabile del rilascio delle risorse non gestite.  I linguaggi .NET specificano una comoda sintassi `using` per tali oggetti, come nell'esempio seguente:

[!code-csharp[UnmanagedResources](../../samples/csharp/snippets/tour/UnmanagedResources.csx#L1-L6)]

Una volta che il blocco `using` è stato completato, il runtime di .NET chiama automaticamente il metodo @System.IDisposable.Dispose dell'oggetto `stream`, che rilascia l'handle di file.  Il runtime esegue questa operazione anche se un'eccezione fa sì che il controllo lasci il blocco.

Per altre informazioni, vedere le pagine seguenti:

* Per C#, [using Statement](../csharp/language-reference/keywords/using-statement.md) (Istruzione using)
* Per F#, [Resource Management: The `use` Keyword](../fsharp/language-reference/resource-management-the-use-keyword.md) (Gestione risorse: la parola chiave `use`)
* Per Visual Basic, [Using Statement](../visual-basic/language-reference/statements/using-statement.md) (Istruzione Using (Visual Basic))

## <a name="type-safety"></a>Indipendenza dai tipi

Gli oggetti vengono allocati in termini di tipi. Le uniche operazioni consentite per un determinato oggetto e per la memoria che utilizza sono quelle del relativo tipo. Un oggetto `Dog` può avere i metodi `Jump` e `WagTail`, ma è improbabile che abbia un metodo `SumTotal`. Un programma può chiamare soltanto i metodi dichiarati di un determinato tipo. Tutte le altre chiamate genereranno un errore in fase di compilazione o un'eccezione di runtime (se si usano funzionalità dinamiche o `object`).

I linguaggi .NET sono orientati agli oggetti, con gerarchie di classi di base e derivate. Il runtime .NET consentirà solo cast degli oggetti e chiamate allineate alla gerarchia di oggetti. Si tenga presente che ogni tipo definito in un qualsiasi linguaggio .NET deriva dal tipo di base `object`.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L18-L23)]

L'indipendenza dai tipi viene inoltre usata per forzare l'incapsulamento garantendo la fedeltà delle parole chiave di accesso. Le parole chiave di accesso sono elementi che controllano l'accesso ai membri di un determinato tipo da parte di altro codice. Vengono in genere usate per diversi dati presenti all'interno di un tipo e per gestire il comportamento del tipo stesso.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L3-L3)]

C#, Visual Basic e F# supportano l'**inferenza del tipo** locale. Con l'inferenza del tipo, il compilatore dedurrà il tipo dell'espressione sul lato sinistro dall'espressione sul lato destro. Questo non significa che l'indipendenza dai tipi è interrotta o evitata. Il tipo risultante **ha** un tipo sicuro, con tutto quello che implica tale caratteristica. Di seguito vengono riscritte le prime due righe dell'esempio precedente per introdurre l'inferenza del tipo. Il resto dell'esempio non viene modificato.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L28-L34)]

Oltre all'inferenza del tipo locale del metodo disponibile in C# e Visual Basic, F# offre anche altre funzionalità di inferenza del tipo.  Per altre informazioni, vedere [Inferenza del tipo](../fsharp/language-reference/type-inference.md).

## <a name="delegates-and-lambdas"></a>Delegati e lambda

I delegati sono simili ai puntatori alle funzioni del linguaggio C++, ma con l'importante differenza che sono indipendenti dai tipi. Sono un tipo di metodo disconnesso all'interno del sistema di tipo CLR. I metodi regolari sono collegati a una classe e possono essere chiamati direttamente solo tramite convenzioni di chiamata statiche o di istanza.

Nel mondo .NET i delegati vengono usati in diverse API e ubicazioni, in particolare nelle espressioni lambda, che costituiscono uno dei fondamenti di LINQ.

Per altre informazioni, vedere il documento [Delegates and lambdas](delegates-lambdas.md) (Delegati e lambda).

## <a name="generics"></a>Generics

I generics sono una funzionalità aggiunta a .NET Framework 2.0. In breve, i generics consentono al programmatore di introdurre un "parametro di tipo" durante la definizione delle classi, operazione che consente al codice client (gli utenti del tipo) di specificare il tipo esatto da usare al posto del parametro di tipo.

I generics sono stati aggiunti per consentire ai programmatori di implementare strutture dati generiche. Prima della loro introduzione, per rendere un tipo `List` generico sarebbe stato necessario usare elementi di tipo `object`. Questa soluzione poteva determinare diversi problemi sia a livello semantico che delle prestazioni, per non parlare dei possibili subdoli errori di runtime. Il più noto di questi ultimi è la situazione in cui una struttura di dati contiene, ad esempio, sia numeri interi che stringhe. Quando si usano i membri dell'elenco, viene generata un'eccezione di tipo `InvalidCastException`.

L'esempio seguente illustra un programma di base in esecuzione mediante un'istanza dei tipi @System.Collections.Generic.List%601.

[!code-csharp[GenericsShort](../../samples/csharp/snippets/tour/GenericsShort.csx)]

Per altre informazioni, vedere l'articolo [Generic types (Generics) overview](generics.md) (Panoramica sui tipi generici (Generics)).

## <a name="async-programming"></a>Programmazione asincrona

La programmazione asincrona è uno dei concetti fondamentali di .NET, poiché offre supporto asincrono nel runtime, nelle librerie del framework e nei costrutti dei linguaggi .NET. A livello interno, questi elementi sono basati su oggetti, ad esempio `Task`, e sfruttano i vantaggi offerti dal sistema operativo per eseguire i processi di I/O nel modo più efficiente possibile.

Per altre informazioni sulla programmazione asincrona in .NET, iniziare con la lettura dell'articolo [Async overview](async.md) (Panoramica sulla programmazione asincrona).

## <a name="language-integrated-query-linq"></a>LINQ (Language-Integrated Query)

LINQ è un potente set di funzionalità per C# e Visual Basic che consente di scrivere codice semplice e dichiarativo per operare sui dati. I dati possono avere diverse forme, ad esempio oggetti in memoria, dati in un database SQL o un documento XML, ma il codice LINQ è in genere uguale per le diverse origini dati.

Per altre informazioni e alcuni esempi, vedere [LINQ (Language-Integrated Query)](using-linq.md).

## <a name="native-interoperability"></a>Interoperabilità nativa

Ogni sistema operativo in uso offre un notevole supporto alla piattaforma per diverse attività di programmazione. .NET consente di accedere a tali API in diversi modi. Nel suo insieme, questo supporto è denominato "interoperabilità nativa". Questa sezione spiega come accedere ad API native da codice .NET gestito.

Il metodo principale per ottenere l'interoperabilità nativa è usare "platform invoke", abbreviato in P/Invoke. In .NET Core questo supporto è disponibile nelle piattaforme Linux e Windows. Un altro metodo, valido solo per Windows, per ottenere l'interoperabilità nativa è noto come "interoperabilità COM" ed è usato per operare con [componenti COM](https://msdn.microsoft.com/library/bwa2bx93.aspx) nel codice gestito. Tale metodo è basato sull'infrastruttura P/Invoke, ma funziona in modo leggermente diverso.

La maggior parte del supporto per l'interoperabilità di Mono (e di Xamarin) per Java e Objective-C è realizzato in modo simile, nel senso che vengono usati gli stessi principi.

Per altre informazioni, vedere il documento [Native interoperability](native-interop.md) (Interoperabilità nativa).

## <a name="unsafe-code"></a>Codice di tipo unsafe

CLR consente di accedere alla memoria nativa e di eseguire operazioni di aritmetica dei puntatori tramite codice `unsafe`. Queste operazioni sono necessarie per determinati algoritmi e per l'interoperabilità dei sistemi. Anche se il codice di tipo unsafe è uno strumento potente, non è consigliabile usarlo a meno che non sia necessario per l'interoperabilità con API di sistema o per implementare l'algoritmo più efficiente. Il codice di tipo unsafe non può essere eseguito nello stesso modo in ambienti diversi e inoltre non sfrutta i vantaggi offerti da un Garbage Collector e dall'indipendenza dai tipi. È consigliabile limitare e centralizzare il codice di tipo unsafe nella misura massima possibile. È inoltre necessario testare tale codice in modo accurato.

L'esempio seguente è una versione modificata del metodo `ToString()` della classe `StringBuilder`  e illustra come l'uso di codice `unsafe` possa implementare in modo efficiente un algoritmo spostando direttamente blocchi di memoria:

[!code-csharp[Unsafe](../../samples/csharp/snippets/tour/Unsafe.csx)]

## <a name="next-steps"></a>Passaggi successivi

Per una panoramica delle funzionalità di C#, vedere [Tour of C#](../csharp/tour-of-csharp/index.md) (Panoramica di C#).

Per una panoramica delle funzionalità di F#, vedere l'articolo [Tour of F#](../fsharp/tour.md) (Panoramica di F#).

Per un'introduzione alla scrittura di codice personalizzato, vedere [Introduzione](get-started.md).

Per informazioni sui componenti principali di .NET, vedere [Componenti dell'architettura .NET](components.md).

