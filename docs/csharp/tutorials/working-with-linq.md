---
title: Uso di LINQ
description: "Questa esercitazione illustra come generare sequenze con LINQ, come scrivere i metodi da usare nelle query LINQ e come distinguere le modalità di valutazione eager e lazy."
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 03/28/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.translationtype: Human Translation
ms.sourcegitcommit: be7974018ce3195dc7344192d647fe64fb2ebcc4
ms.openlocfilehash: ec86c558b9aa9c6269fcf9890978f61a934c081f
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

# <a name="working-with-linq"></a>Uso di LINQ

## <a name="introduction"></a>Introduzione

Questa esercitazione illustra alcune funzionalità disponibili in .NET Core e nel linguaggio C#. Verranno affrontati gli argomenti seguenti:

*    Come generare sequenze con LINQ
*   Come scrivere i metodi da usare facilmente nelle query LINQ
*   Come distinguere le modalità di valutazione eager e lazy

Si apprenderanno queste tecniche creando un'applicazione che illustra una delle abilità di base di un prestigiatore: il [miscuglio faro](https://en.wikipedia.org/wiki/Faro_shuffle). In breve, il miscuglio faro è una tecnica che consiste nel tagliare un mazzo di carte esattamente a metà e quindi nel sovrapporre alternativamente le carte delle due metà per ricostruire il mazzo originale.

I prestigiatori adottano questa tecnica perché, dopo ogni miscuglio, ciascuna carta si trova in una posizione nota e le carte vengono ordinate in base a uno schema ripetitivo. 

Ai fini dell'esercitazione, questa tecnica offre un modo scherzoso per illustrare la manipolazione di sequenze di dati. Si creerà un'applicazione che costruisce un mazzo di carte ed esegue una serie di miscugli scrivendo ogni volta la sequenza ottenuta. Si confronterà inoltre l'ordine aggiornato con quello originale.

Questa esercitazione prevede diversi passaggi. Dopo ogni passaggio, è possibile eseguire l'applicazione e verificare lo stato di avanzamento. È anche possibile vedere l'[esempio completo](https://github.com/dotnet/docs/blob/master/samples/csharp/getting-started/console-linq) disponibile nel repository dotnet/docs su GitHub. Per istruzioni sul download, vedere [Esempi ed esercitazioni](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="prerequisites"></a>Prerequisiti

È necessario configurare il computer per l'esecuzione di .NET Core. Le istruzioni di installazione sono disponibili nella pagina [.NET Core](https://www.microsoft.com/net/core). Questa applicazione può essere eseguita in Windows, Ubuntu Linux, OS X o in un contenitore Docker. È necessario installare l'editor di codice preferito. Nelle descrizioni seguenti viene usato [Visual Studio Code](https://code.visualstudio.com/), un editor open source multipiattaforma, ma è possibile usare gli strumenti con cui si ha maggiore familiarità.

## <a name="create-the-application"></a>Creare l'applicazione

Il primo passaggio consiste nel creare una nuova applicazione. Aprire un prompt dei comandi e creare una nuova directory per l'applicazione, impostandola come directory corrente. Digitare il comando `dotnet new console` al prompt dei comandi per creare i file di avvio per un'applicazione "Hello World" di base.

Se non si è mai usato C#, [questa esercitazione](console-teleprompter.md) illustra la struttura di un programma C#. È possibile leggerla e tornare qui per ottenere altre informazioni su LINQ. 

## <a name="creating-the-data-set"></a>Creazione del set di dati

Si creerà innanzitutto un mazzo di carte. Eseguire questa operazione usando una query LINQ con due origini, una per i quattro semi e l'altra per i 13 valori. Le due origini verranno combinate in un mazzo da 52 carte. Un'istruzione `Console.WriteLine` all'interno di un ciclo `foreach` visualizza le carte.

Questa è la query da eseguire:

```csharp
var startingDeck = from s in Suits()
                   from r in Ranks()
                   select new { Suit = s, Rank = r };

foreach (var c in startingDeck)
{
    Console.WriteLine(c);
}
```

Le clausole `from` multiple generano un `SelectMany` che crea una singola sequenza tramite la combinazione di ogni elemento nella prima sequenza con ogni elemento nella seconda. L'ordine è importante ai fini di questa esercitazione. Il primo elemento nella prima sequenza di origine (semi) viene combinato con ogni elemento della seconda sequenza (valori). Si ottengono così le 13 carte appartenenti al primo seme. Il processo viene ripetuto con ogni elemento della prima sequenza, ovvero i semi. Il risultato finale è un mazzo di carte ordinato in base ai semi e quindi in base ai valori.

Dopo questa operazione, è necessario creare i metodi Suits() e Ranks(), rispettivamente per i semi e valori. Si inizierà con un set molto semplice di *metodi iteratore* che generano la sequenza come un oggetto enumerabile di stringhe:

```csharp
static IEnumerable<string> Suits()
{
    yield return "clubs";
    yield return "diamonds";
    yield return "hearts";
    yield return "spades";
}

static IEnumerable<string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
```

Questi due metodi usano entrambi la sintassi `yield return` per generare una sequenza durante l'esecuzione. Il compilatore crea un oggetto che implementa `IEnumerable<T>` e genera la sequenza di stringhe a mano a mano che vengono richieste.

Andare avanti ed eseguire l'esempio che si è creato finora. Verranno visualizzate le 52 carte del mazzo. Può essere molto utile eseguire questo esempio in un debugger per osservare come vengono eseguiti i metodi `Suits()` e `Values()`. È possibile vedere chiaramente che in ogni sequenza ciascuna stringa viene generata solo quando è necessario.

![Finestra della console con l'applicazione che scrive 52 carte](./media/working-with-linq/console.png)

## <a name="manipulating-the-order"></a>Modifica dell'ordine

A questo punto, si creerà un metodo di utilità che può eseguire il miscuglio. Il primo passaggio consiste nel tagliare il mazzo in due. I metodi `Take()` e `Skip()` inclusi nelle API LINQ offrono questa funzionalità:

```csharp
var top = startingDeck.Take(26);
var bottom = startingDeck.Skip(26);
```

Il metodo shuffle, per eseguire il miscuglio, non esiste nella libreria standard ed è pertanto necessario scriverne uno personalizzato. Questo nuovo metodo illustra varie tecniche che è possibile usare con programmi basati su LINQ. Ogni parte del metodo verrà quindi descritta in passaggi distinti.

La firma per il metodo crea un *metodo di estensione*:

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T>
    (this IEnumerable<T> first, IEnumerable<T> second)
```

Un metodo di estensione è un *metodo statico* con finalità specifiche. È possibile notare l'aggiunta del modificatore `this` nel primo argomento del metodo. Ciò significa che il metodo viene chiamato come se fosse un membro del tipo del primo argomento.

I metodi di estensione possono essere dichiarati solo all'interno di classi `static`. Si creerà pertanto una nuova classe statica denominata `extensions` per questa funzionalità. Proseguendo con l'esercitazione si aggiungeranno altri metodi di estensione che verranno inseriti nella stessa classe.

Questa dichiarazione di metodo segue anche un termine standard in cui i tipi di input e output sono `IEnumerable<T>`. Ciò consente la concatenazione dei metodi LINQ per l'esecuzione di query più complesse.

```csharp
using System.Collections.Generic;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>
            (this IEnumerable<T> first, IEnumerable<T> second)
        {
            // implementation coming.
        }
    }
}
```

Si eseguirà contemporaneamente l'enumerazione di entrambe le sequenze, alternando gli elementi e creando un unico oggetto.  Per scrivere un metodo LINQ utilizzabile con le due sequenze è necessario comprendere il funzionamento di `IEnumerable`.

L'interfaccia `IEnumerable` ha un unico metodo: `GetEnumerator()`. L'oggetto restituito da `GetEnumerator()` ha un metodo per passare all'elemento successivo e una proprietà che recupera l'elemento corrente nella sequenza. Si useranno questi due membri per enumerare la raccolta e restituire gli elementi. Questo metodo Interleave sarà un metodo iteratore. Di conseguenza, anziché creare una raccolta e restituirla, si userà la sintassi `yield return` mostrata in precedenza. 

Questa è l'implementazione del metodo:

[!CODE-csharp[InterleaveSequenceWith](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

Dopo avere scritto questo metodo, tornare al metodo `Main` e mischiare una volta il mazzo:

```csharp
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
        
    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
    var shuffle = top.InterleaveSequenceWith(bottom);

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
```

## <a name="comparisons"></a>Confronti

Per vedere quante volte è necessario mischiare il mazzo per ripristinare l'ordine originale è necessario scrivere un metodo che determina se due sequenze sono uguali. Una volta creato tale metodo, sarà necessario inserire in un ciclo il codice per mischiare il mazzo e verificare quando viene ripristinato l'ordine originale.

Scrivere un metodo per determinare se due sequenze sono uguali è un'operazione piuttosto intuitiva. La struttura è simile a quella del metodo usato per mischiare il mazzo. In questo caso, però, anziché restituire ogni elemento, si confronteranno gli elementi corrispondenti di ogni sequenza. Al termine dell'enumerazione dell'intera sequenza, se ogni elemento corrisponde, le sequenze sono identiche:

[!CODE-csharp[SequenceEquals](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

Questo esempio illustra un secondo termine del linguaggio LINQ: i metodi terminali. Questi metodi accettano una sequenza come input (o, in questo caso, due sequenze) e restituiscono un singolo valore scalare. Quando viene usato, questo tipo di metodo è sempre il metodo finale di una query, come indicato dal nome. 

È possibile notare questo comportamento nella pratica quando si usa il metodo per determinare quando viene ripristinato l'ordine originale del mazzo. Inserire in un ciclo il codice per mischiare il mazzo e arrestare l'esecuzione quando viene ripristinato l'ordine originale della sequenza applicando il metodo `SequenceEquals()`. È possibile notare che questo sarebbe sempre il metodo finale in qualsiasi query poiché restituisce un singolo valore anziché una sequenza:

```csharp
var times = 0;
var shuffle = startingDeck;

do
{
    shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    times++;
} while (!startingDeck.SequenceEquals(shuffle));

Console.WriteLine(times);
```

Eseguire l'esempio e vedere come viene riordinato il mazzo a ogni iterazione, finché non viene ripristinata la configurazione originale dopo 8 iterazioni.

## <a name="optimizations"></a>Ottimizzazioni

L'esempio creato finora *mischia solo le carte interne*, lasciando le carte in cima e in fondo al mazzo sempre nella stessa posizione, ma è possibile introdurre una variazione e *mischiare anche le carte esterne*, cambiando la posizione di tutte e 52 le schede. Per mischiare il mazzo in questo modo, si alternano le carte in modo che la prima carta della metà inferiore diventi la prima carta del mazzo. Di conseguenza, l'ultima carta della metà superiore diventerà l'ultima carta del mazzo. Si tratta semplicemente di una modifica di riga. Aggiornare la chiamata al metodo shuffle per modificare l'ordine della metà superiore e di quella inferiore del mazzo:

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

Eseguire nuovamente il programma. Si noterà che il ripristino dell'ordine del mazzo richiede 52 iterazioni. Nel corso dell'esecuzione del programma si inizierà a notare anche un calo significativo delle prestazioni.

Questo problema può essere dovuto a vari motivi. Una delle cause principali consiste nell'uso inefficiente della *valutazione lazy*.

Le query LINQ vengono valutate in modalità lazy. Le sequenze vengono generate solo quando vengono richiesti gli elementi. Questo è in genere uno dei principali vantaggi di LINQ, ma in un programma di questo tipo può tradursi in una crescita esponenziale del tempo di esecuzione.

Il mazzo originale è stato generato tramite una query LINQ e, ogni volta che si mischiano le carte, il mazzo viene generato eseguendo tre query LINQ sul mazzo precedente. Tutte queste operazioni sono eseguite in modalità lazy e quindi vengono ripetute ogni volta che è richiesta la sequenza. Quando si giunge alla cinquantaduesima iterazione, il mazzo originale è stato rigenerato un numero di volte molto elevato. Per comprendere più facilmente questo comportamento è possibile scrivere un log. Si potrà così correggere il problema.

Di seguito è riportato un metodo log che è possibile aggiungere a qualsiasi query per indicare che la query è stata eseguita.

[!CODE-csharp[LogQuery](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

Instrumentare quindi la definizione di ogni query con un messaggio di log:

```csharp
public static void Main(string[] args)
{
    var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                        from r in Ranks().LogQuery("Rank Generation")
                        select new { Suit = s, Rank = r }).LogQuery("Starting Deck");

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
        
    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;

    do
    {
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        shuffle = shuffle.Skip(26)
            .LogQuery("Bottom Half")
            .InterleaveSequenceWith(shuffle.Take(26).LogQuery("Top Half"))
            .LogQuery("Shuffle");

        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }

        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

Si noti che la registrazione non viene eseguita ogni volta che si accede a una query, ma solo quando si crea la query originale. L'esecuzione del programma richiede ancora molto tempo, ma ora si è individuato il motivo del problema. Se il tempo necessario per mischiare anche le carte esterne è eccessivo, limitarsi a mischiare quelle interne. Gli effetti della valutazione lazy saranno ancora visibili. In un'unica esecuzione del programma verranno eseguite 2592 query, inclusa la generazione di tutti i semi e valori.

Esiste un modo semplice per aggiornare il programma ed evitare tutte queste esecuzioni. I metodi LINQ `ToArray()` e `ToList()` consentono di eseguire la query e di memorizzare i risultati rispettivamente in una matrice e in un elenco. Sono quindi utili per memorizzare nella cache i risultati di una query evitando così di ripetere la query di origine.  Aggiungere una chiamata a `ToArray()` alle query che generano i mazzi di carte ed eseguire nuovamente la query:

[!CODE-csharp[Principale](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

In questo modo, il numero di query si ridurrà a 30. Eseguire nuovamente il programma per mischiare anche le carte esterne e si noteranno miglioramenti analoghi. Il totale delle query sarà infatti 162.

Non interpretare erroneamente questo esempio pensando che tutte le query devono essere eseguite in modalità eager. Questo esempio è stato pensato per mettere in evidenza i casi d'uso in cui la valutazione lazy può causare problemi di prestazioni. Questo avviene perché ogni nuova configurazione del mazzo di carte è basata sulla configurazione precedente. Quando si usa la valutazione lazy, ogni nuova configurazione del mazzo è basata sul mazzo originale, anche eseguendo il codice che ha creato `startingDeck`. Questo comportamento determina una grande quantità di operazioni aggiuntive. 

In pratica, per alcuni algoritmi è più efficiente la valutazione eager, mentre per altri è preferibile la valutazione lazy. Quest'ultima rappresenta in genere la scelta migliore quando l'origine dati è costituita da un processo separato, ad esempio un motore di database. In questi casi, la valutazione lazy consente alle query più complesse di eseguire un solo round trip al processo di database. LINQ supporta entrambi i tipi di valutazione. Scegliere l'opzione migliore per il proprio caso.

## <a name="preparing-for-new-features"></a>Preparazione per le nuove funzionalità

Il codice scritto in questa esercitazione offre un esempio di come creare un prototipo semplice per eseguire un'operazione. Questo è un ottimo modo per esaminare un problema e, per molte funzionalità, può rappresentare la migliore soluzione definitiva. Sono stati usati *tipi anonimi* per le carte e ogni carta è rappresentata da stringhe.

I *tipi anonimi* offrono molti vantaggi in termini di produttività. Non è necessario definire una classe per rappresentare l'archiviazione. Il tipo viene generato automaticamente dal compilatore e sfrutta molte delle procedure consigliate per gli oggetti dati semplici. È *non modificabile*, ossia nessuna delle proprietà del tipo può essere modificata dopo che è stata costruita. I tipi anonimi sono interni a un assembly e quindi non sono considerati parte integrante dell'API pubblica per tale assembly. Contengono inoltre un override del metodo `ToString()` che restituisce una stringa formattata con ciascuno dei valori.

I tipi anonimi presentano anche degli svantaggi. Non hanno nomi accessibili e non possono quindi essere usati come argomenti o valori restituiti. Si noterà che i metodi precedenti in cui sono stati usati questi tipi anonimi sono metodi generici. L'override di `ToString()` potrebbe non risultare adeguato a mano a mano che si aggiungono altre funzionalità all'applicazione. 

Nell'esempio vengono inoltre usate stringhe per il seme e il valore di ogni carta. Questa è una soluzione abbastanza aperta. Il sistema dei tipi C# può essere utile per migliorare il codice, sfruttando i tipi `enum` per tali valori.

Iniziando dai semi, l'uso di un tipo `enum` può offrire una soluzione ideale:

[!CODE-csharp[Suit enum](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet2)]

Il metodo `Suits()` cambia anche il tipo e l'implementazione:

[!CODE-csharp[Suit IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet4)]

Eseguire quindi la stessa modifica anche per i valori delle carte:

[!CODE-csharp[Rank enum](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet3)]

E per il metodo da cui sono generati:

[!CODE-csharp[Rank IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet5)]

Come intervento finale, si può decidere di creare un tipo che rappresenta la carta anziché basarsi su un tipo anonimo. I tipi anonimi sono ideali per i tipi semplici e locali, ma in questo esempio la carta da gioco è uno dei concetti principali. Dovrebbe quindi essere un tipo concreto.

[!CODE-csharp[PlayingCard](../../../samples/csharp/getting-started/console-linq/playingcard.cs?name=snippet1)]

Questo tipo usa *proprietà di sola lettura implementate automaticamente* che sono impostate nel costruttore e non sono quindi modificabili. Si avvale inoltre della nuova funzionalità di *interpolazione delle stringhe* che facilita la formattazione dell'output di tipo stringa.

Aggiornare la query che genera il mazzo di carte iniziale in modo da usare il nuovo tipo:

```csharp
var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                    from r in Ranks().LogQuery("Value Generation")
                    select new PlayingCard(s, r))
                    .LogQuery("Starting Deck")
                    .ToArray();
```

Compilare e ripetere l'esecuzione. L'output è un po' più pulito e il codice è leggermente più chiaro e può essere esteso con più facilità.

## <a name="conclusion"></a>Conclusione

Questo esempio ha illustrato alcuni dei metodi usati in LINQ e come creare metodi personalizzati da usare facilmente con il codice abilitato per LINQ. Ha inoltre mostrato le differenze tra le modalità di valutazione lazy e eager e l'effetto che può avere tale decisione sulle prestazioni.

Ha spiegato anche alcuni aspetti di una delle tecniche di cartomagia. I prestigiatori usano il miscuglio faro perché possono controllare lo spostamento di ogni carta nel mazzo. In alcuni trucchi, il prestigiatore chiede a una persona del pubblico di mettere una carta all'inizio del mazzo e mischia il mazzo più volte senza mai perdere di vista la posizione della carta. Per altri trucchi di illusionismo il mazzo di carte deve essere impostato in un certo modo. Il prestigiatore ordina il mazzo prima di eseguire il trucco e quindi mischia cinque volte le carte interne al mazzo. In uno spettacolo, può mostrare un mazzo apparentemente ordinato in maniera casuale, mischiare le carte tre volte e infine ottenere un mazzo con le carte disposte esattamente nel modo desiderato.

