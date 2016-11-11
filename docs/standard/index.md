---
title: Nozioni di base su .NET
description: Nozioni di base su .NET
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 10/05/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
translationtype: Human Translation
ms.sourcegitcommit: be774ae1291def36baafffbf2f717cf98565cd60
ms.openlocfilehash: fba870a93784b579da1065a07d82974951ac7e28

---

# <a name="net-primer"></a>Nozioni di base su .NET

> Per imparare a creare una semplice applicazione .NET Core, consultare le [esercitazioni introduttive di .NET Core](../core/getting-started.md). Sono necessari pochi minuti per realizzare ed eseguire la prima app.

.NET è una piattaforma di sviluppo con finalità generali che può essere usata per qualsiasi tipo di app o carico di lavoro compatibile con questo genere di soluzioni. Integra diverse funzionalità chiave interessanti per molti sviluppatori, come la gestione automatica della memoria e il supporto per moderni linguaggi di programmazione, che permettono di creare in modo efficiente applicazioni di alta qualità. .NET realizza un ambiente di programmazione di alto livello con diverse funzionalità pratiche, consentendo al tempo stesso l'accesso a basso livello alla memoria e alle API native.

Sono disponibili diverse implementazioni di .NET basate su [standard .NET](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) aperti che specificano i concetti chiave della piattaforma. Questi standard sono ottimizzati in modo separato per i diversi tipi di applicazione (desktop, dispositivi mobili, giochi, cloud) e supportano numerosi chip, ad esempio x86/x64 e ARM, e sistemi operativi, ad esempio Windows, Linux, iOS, Android e macOS. Anche i componenti open source costituiscono una parte importante dell'ecosistema .NET: diverse implementazioni e librerie .NET, infatti, sono disponibili con licenze approvate da OSI (Open Source Initiative).

Per informazioni su tutte le differenti edizioni di .NET disponibili, sia Microsoft che di altre società, vedere il documento [Overview of .NET implementations](../about/products.md) (Panoramica delle implementazioni .NET).

Le nozioni di base fornite in questo articolo consentiranno di comprendere alcuni dei concetti chiave della piattaforma .NET. Per ogni argomento verranno inoltre forniti collegamenti ad altre risorse. Al termine, l'utente disporrà di informazioni sufficienti per riconoscere le caratteristiche e i concetti più significativi della piattaforma .NET e saprà come estendere le proprie conoscenze su tali aspetti chiave. 

## <a name="a-stroll-through-net"></a>Panoramica di .NET

Come qualsiasi framework di sviluppo di applicazioni avanzato e collaudato, .NET include diverse funzionalità potenti che facilitano il lavoro degli sviluppatori e rendono la scrittura del codice un'attività più efficace ed espressiva. Questa sezione descrive i concetti base delle funzionalità più importanti e, quando necessario, fornisce puntatori a informazioni più dettagliate. Una volta conclusa questa panoramica, l'utente avrà a disposizione informazioni sufficienti per leggere sia gli esempi disponibili nel repository GitHub sia altro codice comprendendone le finalità.

*   [Linguaggi di programmazione](#programming-languages)
*   [Automatic Memory Management](#automatic-memory-management)
*   [Indipendenza dai tipi](#type-safety)
*   [Delegati e lambda](#delegates-and-lambdas)
*   [Tipi generici (Generics)](#generic-types-generics)
*   [LINQ (Language-Integrated Query)](#language-integrated-query-linq)
*   [Programmazione asincrona](#async-programming)
*   [Interoperabilità nativa](#native-interoperability)
*   [Codice di tipo unsafe](#unsafe-code)

### <a name="programming-languages"></a>Linguaggi di programmazione

Per creare la propria applicazione, uno sviluppatore può scegliere qualsiasi linguaggio di programmazione che supporta .NET. Poiché .NET offre interoperabilità e indipendenza dal linguaggio, è possibile interagire con altre applicazioni e componenti .NET indipendentemente dal linguaggio in cui sono stati sviluppati.

I linguaggi che consentono di sviluppare applicazioni per la piattaforma .NET sono conformi alla [specifica CLI (Common Language Infrastructure)](https://www.visualstudio.com/en-us/mt639507).

I linguaggi Microsoft supportati da .NET includono C#, F# e Visual Basic. 

* C# è un linguaggio semplice, potente, indipendente dai tipi e orientato agli oggetti che mantiene al tempo stesso l'espressività e l'eleganza tipiche dei linguaggi di tipo C. Gli sviluppatori che hanno familiarità con C e linguaggi simili incontreranno pochi problemi ad adattarsi a C#.

* F# è un linguaggio di programmazione multipiattaforma e funzionale che supporta anche la programmazione tradizionale imperativa e orientata agli oggetti.

* Visual Basic è un linguaggio semplice da apprendere che consente di creare una vasta gamma di applicazioni da eseguire in .NET.

> [!NOTE]
> Nella versione corrente di .NET Core solo C# è pienamente supportato per tutti gli strumenti Microsoft.  F# è supportato in .NET Core SDK, ma non dispone ancora degli strumenti di Visual Studio.  Il supporto di Visual Basic per l'SDK e gli strumenti Visual Studio sarà disponibile a breve.

### <a name="automatic-memory-management"></a>Gestione automatica della memoria

Garbage Collection è la più nota funzionalità di .NET. Gli sviluppatori non devono gestire attivamente la memoria, anche se sono presenti meccanismi per fornire ulteriori informazioni al Garbage Collector. C# include la parola chiave `new` per allocare la memoria in termini di un particolare tipo e la parola chiave `using` per fornire l'ambito relativo all'utilizzo dell'oggetto. Il Garbage Collector ha un approccio "lazy" alla gestione della memoria, anteponendo la velocità effettiva dell'applicazione alla raccolta immediata di memoria.

Le due righe di codice seguenti allocano entrambe memoria:

```cs
var title = ".NET Primer";
var list = new List<string>;

```

Non esiste una parola chiave analoga per deallocare la memoria, in quanto la deallocazione viene eseguita automaticamente quando il Garbage Collector recupera la memoria durante l'esecuzione pianificata.

Le variabili di metodo in genere escono dall'ambito dopo il completamento del metodo e a quel punto possono essere raccolte. È tuttavia possibile indicare al Garbage Collector che un particolare oggetto è fuori ambito prima del completamento del metodo usando l'istruzione `using`.

```cs
using(FileStream stream = GetFileStream(context))
{
    //operations on the stream
}

```

Dopo il completamento del blocco `using`, il Garbage Collector saprà che l'oggetto `stream` dell'esempio precedente può essere raccolto e che la relativa memoria può essere recuperata.

Una delle funzionalità meno ovvie, ma più potenti di Garbage Collector è la sicurezza della memoria. L'invariante di sicurezza della memoria è molto semplice: un programma garantisce la sicurezza della memoria se accede soltanto alla memoria che è stata allocata (e non liberata). I puntatori tralasciati rappresentano sempre un errore e tenerne traccia è spesso piuttosto difficile.

Per garantire la sicurezza della memoria, il runtime .NET offre servizi aggiuntivi che non sono normalmente forniti da un Garbage Collector. Assicura infatti che i programmi non eseguano l'indicizzazione oltre la fine di un array o accedano a un campo fantasma oltre la fine di un oggetto.

L'esempio seguente genera un'eccezione come risultato della sicurezza della memoria.

```cs
int[] numbers = new int[42];
int number = numbers[42]; // will throw (indexes are 0-based)

```

### <a name="type-safety"></a>Indipendenza dai tipi

Gli oggetti vengono allocati in termini di tipi. Le uniche operazioni consentite per un determinato oggetto e per la memoria che utilizza sono quelle del relativo tipo. Un oggetto `Dog` può avere i metodi `Jump` e `WagTail`, ma è improbabile che abbia un metodo `SumTotal`. Un programma può chiamare soltanto i metodi dichiarati di un determinato tipo. Tutte le altre chiamate genereranno un errore in fase di compilazione o un'eccezione di runtime (se si usano funzionalità dinamiche o `object`).

I linguaggi .NET sono orientati agli oggetti, con gerarchie di classi di base e derivate. Il runtime .NET consentirà solo cast degli oggetti e chiamate allineate alla gerarchia di oggetti. Si tenga presente che ogni tipo definito in un qualsiasi linguaggio .NET deriva dal tipo di base `object`.

```cs
Dog dog = Dog.AdoptDog(); // Returns a Dog type
Pet pet = (Pet)dog; // Dog derives from Pet
pet.ActCute();
Car car = (Car)dog; // will throw - no relationship between Car and Dog
object temp = (object)dog; // legal - a Dog is an object
car = (Car)temp; // will throw - the runtime isn't fooled
car.Accelerate() // the dog won't like this, nor will the program get this far

```

L'indipendenza dai tipi viene inoltre usata per forzare l'incapsulamento garantendo la fedeltà delle parole chiave di accesso. Le parole chiave di accesso sono elementi che controllano l'accesso ai membri di un determinato tipo da parte di altro codice. Vengono in genere usate per diversi dati presenti all'interno di un tipo e per gestire il comportamento del tipo stesso.

```cs
Dog dog = Dog._nextDogToBeAdopted; // will throw - this is a private field

```

Alcuni linguaggi .NET supportano l'**inferenza del tipo**. Con l'inferenza del tipo, il compilatore dedurrà il tipo dell'espressione sul lato sinistro dall'espressione sul lato destro. Questo non significa che l'indipendenza dai tipi è interrotta o evitata. Il tipo risultante **ha** un tipo sicuro, con tutto quello che implica tale caratteristica. Di seguito vengono riscritte le prime due righe dell'esempio precedente per introdurre l'inferenza del tipo. Si noti che il resto dell'esempio non viene modificato.

```cs
  var dog = Dog.AdoptDog();
  var pet = (Pet)dog;
  pet.ActCute();
  Car car = (Car)dog; // will throw - no relationship between Car and Dog
  object temp = (object)dog; // legal - a Dog is an object
  car = (Car)temp; // will throw - the runtime isn't fooled
  car.Accelerate() // the dog won't like this, nor will the program get this far

```

### <a name="delegates-and-lambdas"></a>Delegati e lambda

I delegati sono simili ai puntatori alle funzioni del linguaggio C++, ma con l'importante differenza che sono indipendenti dai tipi. Sono un tipo di metodo disconnesso all'interno del sistema di tipo CLR. I metodi regolari sono collegati a una classe e possono essere chiamati direttamente solo tramite convenzioni di chiamata statiche o di istanza.

Nel mondo .NET i delegati vengono usati in diverse API e ubicazioni, in particolare nelle espressioni lambda, che costituiscono uno dei fondamenti di LINQ.

Per altre informazioni, vedere il documento [Delegates and lambdas](delegates-lambdas.md) (Delegati e lambda).

### <a name="generic-types-generics"></a>Tipi generici (Generics)

I tipi generici, detti anche "generics", sono una funzionalità aggiunta a .NET Framework 2.0. In breve, i generics consentono al programmatore di introdurre un "parametro di tipo" durante la definizione delle classi, operazione che consente al codice client (gli utenti del tipo) di specificare il tipo esatto da usare al posto del parametro di tipo.

I generics sono stati aggiunti per consentire ai programmatori di implementare strutture dati generiche. Prima della loro introduzione, per rendere un tipo _List_ generico sarebbe stato necessario utilizzare elementi di tipo _object_. Questa soluzione poteva determinare diversi problemi sia a livello semantico che delle prestazioni, per non parlare dei possibili subdoli errori di runtime. Il più noto di questi ultimi è la situazione in cui una struttura di dati contiene, ad esempio, sia numeri interi che stringhe. Quando si utilizzano i membri dell'elenco, viene generata un'eccezione di tipo _InvalidCastException_.

L'esempio seguente mostra un programma di base in esecuzione mediante un'istanza dei tipi @System.Collections.Generic.List%601.

```cs
using System;
using System.Collections.Generic;

namespace GenericsSampleShort {
    public static void Main(string[] args){
        // List<string> is the client way of specifying the actual type for the type parameter T
        List<string> listOfStrings = new List<string> { "First", "Second", "Third" };

        // listOfStrings can accept only strings, both on read and write.
        listOfStrings.Add("Fourth");

        // Below will throw a compile-time error, since the type parameter
        // specifies this list as containing only strings.
        listOfStrings.Add(1);

    }
}

```

Per altre informazioni, vedere l'articolo [Generic types (Generics) overview](generics.md) (Panoramica sui tipi generici (Generics)).

### <a name="async-programming"></a>Programmazione asincrona

La programmazione asincrona è uno dei concetti fondamentali di .NET, poiché offre supporto asincrono nel runtime, nelle librerie del framework e nei costrutti dei linguaggi .NET. A livello interno, questi elementi sono basati su oggetti, ad esempio `Task`, e sfruttano i vantaggi offerti dal sistema operativo per eseguire i processi di I/O nel modo più efficiente possibile.

Per altre informazioni sulla programmazione asincrona in .NET, iniziare con la lettura dell'articolo [Async overview](async.md) (Panoramica sulla programmazione asincrona).

### <a name="language-integrated-query-linq"></a>LINQ (Language-Integrated Query)

LINQ è un potente set di funzionalità per C# e Visual Basic che consente di scrivere codice semplice e dichiarativo per operare sui dati. I dati possono avere diverse forme, ad esempio oggetti in memoria, dati in un database SQL o un documento XML, ma il codice LINQ è in genere uguale per le diverse origini dati.

Per altre informazioni e alcuni esempi, vedere [LINQ (Language-Integrated Query)](using-linq.md).

### <a name="native-interoperability"></a>Interoperabilità nativa

Ogni sistema operativo in uso offre un notevole supporto alla piattaforma per diverse attività di programmazione. .NET consente di accedere a tali API in diversi modi. Nel suo insieme, questo supporto è denominato "interoperabilità nativa". Questa sezione spiega come accedere ad API native da codice .NET gestito.

Il metodo principale per ottenere l'interoperabilità nativa è usare "platform invoke", abbreviato in P/Invoke. In .NET Core questo supporto è disponibile nelle piattaforme Linux e Windows. Un altro metodo, valido solo per Windows, per ottenere l'interoperabilità nativa è noto come "interoperabilità COM" ed è usato per operare con [componenti COM](https://msdn.microsoft.com/library/bwa2bx93.aspx) nel codice gestito. Tale metodo è basato sull'infrastruttura P/Invoke, ma funziona in modo leggermente diverso.

La maggior parte del supporto per l'interoperabilità di Mono (e di Xamarin) per Java e Objective-C è realizzato in modo simile, nel senso che vengono usati gli stessi principi.

Per altre informazioni, vedere il documento [Native interoperability](native-interop.md) (Interoperabilità nativa).

### <a name="unsafe-code"></a>Codice di tipo unsafe

CLR consente di accedere alla memoria nativa e di eseguire operazioni di aritmetica dei puntatori tramite codice `unsafe`. Queste operazioni sono necessarie per determinati algoritmi e per l'interoperabilità dei sistemi. Anche se il codice di tipo unsafe è uno strumento potente, non è consigliabile usarlo a meno che non sia necessario per l'interoperabilità con API di sistema o per implementare l'algoritmo più efficiente. Il codice di tipo unsafe non può essere eseguito nello stesso modo in ambienti diversi e inoltre non sfrutta i vantaggi offerti da un Garbage Collector e dall'indipendenza dai tipi. È consigliabile limitare e centralizzare il codice di tipo unsafe nella misura massima possibile. È inoltre necessario testare tale codice in modo accurato.

Il metodo `ToString()` della [classe StringBuilder](https://github.com/dotnet/coreclr/blob/master/src/mscorlib/src/System/Text/StringBuilder.cs#L327) mostra come l'uso di codice `unsafe` può implementare in modo efficiente un algoritmo spostando direttamente blocchi di memoria:

```cs
public override String ToString() {
          Contract.Ensures(Contract.Result<String>() != null);

          VerifyClassInvariant();

          if (Length == 0)
              return String.Empty;

          string ret = string.FastAllocateString(Length);
          StringBuilder chunk = this;
          unsafe {
              fixed (char* destinationPtr = ret)
              {
                  do
                  {
                      if (chunk.m_ChunkLength > 0)
                      {
                          // Copy these into local variables so that they are stable even in the presence of ----s (hackers might do this)
                          char[] sourceArray = chunk.m_ChunkChars;
                          int chunkOffset = chunk.m_ChunkOffset;
                          int chunkLength = chunk.m_ChunkLength;

                          // Check that we will not overrun our boundaries.
                          if ((uint)(chunkLength + chunkOffset) <= ret.Length && (uint)chunkLength <= (uint)sourceArray.Length)
                          {
                              fixed (char* sourcePtr = sourceArray)
                                  string.wstrcpy(destinationPtr + chunkOffset, sourcePtr, chunkLength);
                          }
                          else
                          {
                              throw new ArgumentOutOfRangeException("chunkLength", Environment.GetResourceString("ArgumentOutOfRange_Index"));
                          }
                      }
                      chunk = chunk.m_ChunkPrevious;
                  } while (chunk != null);
              }
          }
          return ret;
      }

```

## <a name="notes"></a>Note

Il termine "runtime .NET" viene usato in tutto il documento per indicare le diverse implementazioni di .NET, ad esempio CLR, Mono, IL2CPP e altre. I nomi più specifici vengono usati solo se necessario.

Questo documento non intende ripercorrere la storia di .NET, ma si limita a descrivere la piattaforma .NET allo stato attuale. Non è importante se una funzionalità di .NET è sempre stata disponibile o se è stata introdotta solo di recente: vengono riportati soli gli aspetti che è importante evidenziare e discutere.



<!--HONumber=Nov16_HO1-->


