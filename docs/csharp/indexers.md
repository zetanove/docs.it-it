---
title: Indexers (Indicizzatori)
description: Indexers (Indicizzatori)
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 0e9496da-e766-45a9-b92b-91820d4a350e
ms.translationtype: Human Translation
ms.sourcegitcommit: 890c058bd09893c2adb185e1d8107246eef2e20a
ms.openlocfilehash: a3ee06e9e177fe3c0a41e99361ba9289943c1cf5
ms.contentlocale: it-it
ms.lasthandoff: 04/12/2017

---

# <a name="indexers"></a>Indexers (Indicizzatori)

Gli *indicizzatori* sono simili alle proprietà e per molti aspetti si basano sulle stesse funzionalità del linguaggio delle [proprietà](properties.md). Gli indicizzatori consentono proprietà *indicizzate*, ovvero proprietà a cui si fa riferimento tramite uno o più argomenti, che forniscono un indice per una raccolta di valori.

## <a name="indexer-syntax"></a>Sintassi degli indicizzatori

È possibile accedere a un indicizzatore tramite un nome di variabile e parentesi quadre. Gli argomenti dell'indicizzatore devono trovarsi all'interno delle parentesi:

```csharp
var item = someObject["key"];
someObject["AnotherKey"] = item;
```

Per dichiarare un indicizzatore si usa la parola chiave `this` come nome di proprietà e si racchiudono gli argomenti tra parentesi quadre. Questa dichiarazione corrisponde all'utilizzo illustrato nel paragrafo precedente:

```csharp
public int this[string key]
{
    get { return storage.Find(key); }
    set { storage.SetAt(key, value); }
}
```

Da questo esempio iniziale è possibile rendersi conto della relazione tra la sintassi relativa alle proprietà e a quella relativa agli indicizzatori. Questa analogia si estende alla maggior parte delle regole della sintassi degli indicizzatori. Agli indicizzatori si possono applicare tutti i modificatori di accesso validi (public, protected internal, protected, internal o private). Possono essere sealed, virtual o abstract. Come per le proprietà, in un indicizzatore è possibile specificare modificatori di accesso diversi per le funzioni di accesso get e set.
È anche possibile specificare indicizzatori di sola lettura (omettendo la funzione di accesso set) o indicizzatori di sola scrittura (omettendo la funzione di accesso get).

È possibile applicare agli indicizzatori quasi tutto ciò che si apprende dall'uso delle proprietà. L'unica eccezione a tale regola è costituita dalle *proprietà implementate automaticamente*. Il compilatore non è sempre in grado di generare l'archiviazione corretta per un indicizzatore.

La differenza tra indicizzatori e proprietà è costituita dalla presenza negli indicizzatori di argomenti che consentono di fare riferimento a un elemento all'interno di un set di elementi. È possibile definire più indicizzatori in un tipo, a condizione che gli elenchi di argomenti per ogni indicizzatore siano univoci. Verranno ora esaminati diversi scenari in cui è possibile usare uno o più indicizzatori in una definizione di classe. 

## <a name="scenarios"></a>Scenari

Si definiscono *indicizzatori* in un tipo se l'API corrispondente modella una raccolta per cui si definiscono gli argomenti. Gli indicizzatori possono essere mappati direttamente o meno ai tipi di raccolta che fanno parte di .NET Framework Core. Oltre alla modellazione di una raccolta, il tipo può avere altre responsabilità.
Gli indicizzatori consentono di fornire l'API corrispondente all'astrazione del tipo senza esporre nei minimi dettagli la modalità di archiviazione o di calcolo dei valori per tale astrazione.

Di seguito è riportata la descrizione dettagliata di alcuni scenari comuni per l'uso di *indicizzatori*. È possibile accedere alla [cartella degli esempi per gli indicizzatori](https://github.com/dotnet/docs/tree/master/samples/csharp/indexers). Per istruzioni sul download, vedere [Esempi ed esercitazioni](../samples-and-tutorials/index.md#viewing-and-downloading-samples).

### <a name="arrays-and-vectors"></a>Matrici e vettori

Uno degli scenari più comuni per la creazione di indicizzatori si presenta quando il tipo modella una matrice o un vettore. È possibile creare un indicizzatore per modellare un elenco ordinato di dati. 

Il vantaggio di creare un indicizzatore personalizzato è la possibilità di definire la modalità di archiviazione della raccolta più adatta alle proprie esigenze. Si immagini uno scenario in cui il tipo debba modellare una quantità di dati cronologici troppo grande perché sia possibile caricarla in memoria in una sola volta. È quindi necessario caricare e scaricare sezioni della raccolta in base all'utilizzo. L'esempio seguente riproduce questo comportamento. L'esempio indica il numero di punti dati esistenti, crea pagine in cui inserire sezioni di dati su richiesta e rimuove le pagine dalla memoria per liberare spazio per le pagine relative alle richieste più recenti.

```csharp
public class DataSamples
{
    private class Page
    {
        private readonly List<Measurements> pageData = new List<Measurements>();
        private readonly int startingIndex;
        private readonly int length;
        private bool dirty;
        private DateTime lastAccess;

        public Page(int startingIndex, int length)
        {
            this.startingIndex = startingIndex;
            this.length = length;
            lastAccess = DateTime.Now;

            // This stays as random stuff:
            var generator = new Random();
            for(int i=0; i < length; i++)
            {
                var m = new Measurements
                {
                    HiTemp = generator.Next(50, 95),
                    LoTemp = generator.Next(12, 49),
                    AirPressure = 28.0 + generator.NextDouble() * 4
                };
                pageData.Add(m);
            }
        }
        public bool HasItem(int index) =>
            ((index >= startingIndex) &&
            (index < startingIndex + length));

        public Measurements this[int index]
        {
            get
            {
                lastAccess = DateTime.Now;
                return pageData[index - startingIndex];
            }
            set
            {
                pageData[index - startingIndex] = value;
                dirty = true;
                lastAccess = DateTime.Now;
            }
        }

        public bool Dirty => dirty;
        public DateTime LastAccess => lastAccess;
    }

    private readonly int totalSize;
    private readonly List<Page> pagesInMemory = new List<Page>();

    public DataSamples(int totalSize)
    {
        this.totalSize = totalSize;
    }

    public Measurements this[int index]
    {
        get
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");

            var page = updateCachedPagesForAccess(index);
            return page[index];
        }
        set
        {
            if (index < 0)
                throw new IndexOutOfRangeException("Cannot index less than 0");
            if (index >= totalSize)
                throw new IndexOutOfRangeException("Cannot index past the end of storage");
            var page = updateCachedPagesForAccess(index);

            page[index] = value;
        }
    }

    private Page updateCachedPagesForAccess(int index)
    {
        foreach (var p in pagesInMemory)
        {
            if (p.HasItem(index))
            {
                return p;
            }
        }
        var startingIndex = (index / 1000) * 1000;
        var newPage = new Page(startingIndex, 1000);
        addPageToCache(newPage);
        return newPage;
    }

    private void addPageToCache(Page p)
    {
        if (pagesInMemory.Count > 4)
        {
            // remove oldest non-dirty page:
            var oldest = pagesInMemory
                .Where(page => !page.Dirty)
                .OrderBy(page => page.LastAccess)
                .FirstOrDefault();
            // Note that this may keep more than 5 pages in memory
            // if too much is dirty
            if (oldest != null)
                pagesInMemory.Remove(oldest);
        }
        pagesInMemory.Add(p);
    }
}
```

È possibile seguire questo schema di progettazione per modellare qualsiasi funzione di ordinamento di una raccolta nei casi in cui per validi motivi non è possibile caricare l'intero set di dati in una raccolta in memoria. Si noti che la classe `Page` è una classe annidata private che non fa parte dell'interfaccia public. Questi dettagli sono nascosti agli utenti di questa classe.

### <a name="dictionaries"></a>Dizionari

Un altro scenario comune riguarda la necessità di modellare un dizionario o una mappa e si presenta quando il tipo archivia i valori in base alla chiave, in genere chiavi di testo. Questo esempio crea un dizionario che esegue il mapping di argomenti della riga di comando a [espressioni lambda](delegates-overview.md) che gestiscono tali opzioni. Nell'esempio seguente sono presenti due classi: una classe `ArgsActions` che esegue il mapping di un'opzione della riga di comando a un delegato `Action` e una classe `ArgsProcessor` che usa `ArgsActions` per eseguire ogni `Action` quando incontra tale opzione.

```csharp
public class ArgsProcessor
{
    private readonly ArgsActions actions;

    public ArgsProcessor(ArgsActions actions)
    {
        this.actions = actions;
    }

    public void Process(string[] args)
    {
        foreach(var arg in args)
        {
            actions[arg]?.Invoke();
        }
    }

}
public class ArgsActions
{
    readonly private Dictionary<string, Action> argsActions = new Dictionary<string, Action>();

    public Action this[string s]
    {
        get
        {
            Action action;
            Action defaultAction = () => {} ;
            return argsActions.TryGetValue(s, out action) ? action : defaultAction;
        }
    }

    public void SetOption(string s, Action a)
    {
        argsActions[s] = a;
    }
}
```

In questo esempio la raccolta `ArgsAction` è strettamente mappata alla raccolta sottostante.
La funzione `get` determina se un'opzione specifica è stata configurata. In caso affermativo, viene restituito l'oggetto `Action` associato a tale opzione. In caso contrario, restituisce un oggetto `Action` che non esegue alcuna operazione. La funzione di accesso public non include una funzione di accesso `set`. Per l'impostazione di opzioni la progettazione usa invece un metodo public.

### <a name="multi-dimensional-maps"></a>Mappe multidimensionali

È possibile creare indicizzatori che usano più argomenti, che, in più, non devono necessariamente essere dello stesso tipo. Di seguito sono riportati due esempi.   

Il primo esempio illustra una classe che genera valori per un set di Mandelbrot. Per altre informazioni sulle regole matematiche alla base di questo, leggere [questo articolo](https://en.wikipedia.org/wiki/Mandelbrot_set). L'indicizzatore usa due valori double per definire un punto del piano X, Y.
La funzione di accesso get calcola il numero di iterazioni necessarie a stabilire che un punto non appartiene al set. Se viene raggiunto il numero massimo di iterazioni, il punto si trova nel set e viene restituito il valore maxIterations della classe. Nelle immagini generate tramite computer comunemente note per il set di Mandelbrot sono definiti colori per il numero di iterazioni necessarie a determinare se un punto è esterno al set.

```csharp
public class Mandelbrot
{
    readonly private int maxIterations;

    public Mandelbrot(int maxIterations)
    {
        this.maxIterations = maxIterations;
    }

    public int this [double x, double y]
    {
        get
        {
            var iterations = 0;
            var x0 = x;
            var y0 = y;

            while ((x*x + y * y < 4) &&
                (iterations < maxIterations))
            {
                var newX = x * x - y * y + x0;
                y = 2 * x * y + y0;
                x = newX;
                iterations++;
            }
            return iterations;
        }
    }
}
```

Il set di Mandelbrot definisce valori in corrispondenza di ogni coordinata (x, y) per valori di numeri reali.
Ciò consente di definire un dizionario che può contenere un numero infinito di valori. Pertanto, il set non prevede alcuna archiviazione. Questa classe calcola invece un valore per ogni punto in cui il codice chiama la funzione di accesso `get`. Non viene usata alcuna archiviazione sottostante.

Verrà ora illustrato l'ultimo caso di uso degli indicizzatori, in cui l'indicizzatore riceve più argomenti di tipi diversi. Si consideri un programma per la gestione dei dati cronologici relativi alle temperature. Questo indicizzatore imposta o riceve la temperatura massima e la temperatura minima di una determinata posizione in base alla città corrispondente e alla data:

```csharp
using DateMeasurements = 
    System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements = 
    System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;

public class HistoricalWeatherData
{
    readonly CityDataMeasurements storage = new CityDataMeasurements();

    public Measurements this[string city, DateTime date]
    {
        get
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
                throw new ArgumentOutOfRangeException(nameof(city), "City not found");

            // strip out any time portion:
            var index = date.Date;
            var measure = default(Measurements);
            if (cityData.TryGetValue(index, out measure))
                return measure;
            throw new ArgumentOutOfRangeException(nameof(date), "Date not found");
        }
        set
        {
            var cityData = default(DateMeasurements);

            if (!storage.TryGetValue(city, out cityData))
            {
                cityData = new DateMeasurements();
                storage.Add(city, cityData);
            }

            // Strip out any time portion:
            var index = date.Date;
            cityData[index] = value;
        }
    }
}
```

Questo esempio crea un indicizzatore che esegue il mapping di dati meteo a due diversi argomenti: una città (rappresentata da un valore `string`) e una data (rappresentata da un valore `DateTime`). Per l'archiviazione interna vengono usate due classi `Dictionary` che rappresentano il dizionario bidimensionale. L'API public non rappresenta più l'archiviazione sottostante. Le funzionalità del linguaggio relative agli indicizzatori consentono di creare un'interfaccia public che rappresenta l'astrazione, anche se l'archiviazione sottostante deve usare tipi di raccolta principale diversi.

Due parti del codice potrebbero risultare poco chiare per alcuni sviluppatori. Queste due istruzioni `using`:

```csharp
using DateMeasurements = System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>;
using CityDataMeasurements = System.Collections.Generic.Dictionary<string, System.Collections.Generic.Dictionary<System.DateTime, IndexersSamples.Common.Measurements>>;
```

creano un *alias* per un tipo generico costruito. Queste istruzioni consentono al codice successivo di usare i nomi `DateMeasurements` e `CityDateMeasurements`, più descrittivi, anziché la costruzione generica di `Dictionary<DateTime, Measurements>` e `Dictionary<string, Dictionary<DateTime, Measurements> >`. Questo costrutto richiede però l'uso di nomi completi di tipo sul lato destro del segno `=`.

La seconda tecnica consiste nel rimuovere le parti relative all'ora di qualsiasi oggetto `DateTime` usato per effettuare l'indicizzazione all'interno delle raccolte. .NET framework non prevede un tipo dotato della sola data.
Gli sviluppatori usano il tipo `DateTime`, ma usano la proprietà `Date` per assicurarsi che tutti gli oggetti `DateTime` di quel giorno siano uguali.

## <a name="summing-up"></a>Conclusioni

È necessario creare indicizzatori ogni volta che all'interno di una classe è presente un elemento analogo a una proprietà e tale proprietà rappresenta non un singolo valore, ma una raccolta di valori in cui ogni singolo elemento è identificato da un set di argomenti. Tali argomenti consentono di identificare in modo univoco un elemento della raccolta a cui fare riferimento.
Gli indicizzatori estendono il concetto di [proprietà](properties.md), in cui un membro viene considerato come elemento dati all'esterno della classe, ma come metodo all'interno. Gli indicizzatori consentono agli argomenti di individuare un singolo elemento all'interno di una proprietà che rappresenta un set di elementi.

