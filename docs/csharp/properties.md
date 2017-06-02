---
title: "Proprietà"
description: "Proprietà"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 04/03/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 6950d25a-bba1-4744-b7c7-a3cc90438c55
ms.translationtype: Human Translation
ms.sourcegitcommit: f9eab74a3b259037aff30320753191eee95aa974
ms.openlocfilehash: 763a76a8ea0e48fd6935c951ce584efad50dabb9
ms.contentlocale: it-it
ms.lasthandoff: 04/25/2017

---

# <a name="properties"></a>Proprietà

Le proprietà sono elementi fondamentali in C#. Il linguaggio definisce la sintassi che consente agli sviluppatori di scrivere codice che esprime in modo preciso la finalità della progettazione.

Quando viene eseguito l'accesso, le proprietà si comportano come i campi.
Tuttavia, a differenza dei campi, le proprietà vengono implementate con funzioni di accesso che definiscono le istruzioni eseguite al momento dell'accesso e dell'assegnazione della proprietà.

## <a name="property-syntax"></a>Sintassi delle proprietà

La sintassi delle proprietà è un'estensione naturale dei campi. Un campo definisce una posizione di archiviazione:

```csharp
public class Person
{
    public string FirstName;
    // remaining implementation removed from listing
}
```

La definizione di una proprietà contiene le dichiarazioni di una funzione di accesso `get` e `set` che recupera e assegna il valore della proprietà:

```csharp
public class Person
{
    public string FirstName { get; set; }

    // remaining implementation removed from listing
}
```

La sintassi illustrata sopra è la sintassi della *proprietà automatica*. Il compilatore genera la posizione di archiviazione per il campo che esegue il backup della proprietà. Il compilatore implementa anche il corpo delle funzioni di accesso `get` e `set`.

In alcuni casi è necessario inizializzare una proprietà con un valore diverso da quello predefinito per il suo tipo.  In C# questa operazione è possibile impostando un valore dopo la parentesi graffa chiusa della proprietà. Per la proprietà `FirstName` è preferibile usare come valore iniziale una stringa vuota anziché `null`. Ecco come eseguire questa operazione:

```csharp
public class Person
{
    public string FirstName { get; set; } = string.Empty;

    // remaining implementation removed from listing
}
```

Questo è particolarmente utile per le proprietà di sola lettura, come si vedrà più avanti in questo argomento.

È anche possibile definire l'archiviazione manualmente, come illustrato di seguito:

```csharp
public class Person
{
    public string FirstName
    {
        get { return firstName; }
        set { firstName = value; }
    }
    private string firstName;
    // remaining implementation removed from listing
}
```

Se l'implementazione di una proprietà corrisponde a un'espressione singola, è possibile usare *membri nel corpo dell'espressione* per il getter o il setter:

```csharp
public class Person
{
    public string FirstName
    {
        get => firstName;
        set => firstName = value;
    }
    private string firstName;
    // remaining implementation removed from listing
}
```

Questa sintassi semplificata verrà usata ovunque applicabile in questo argomento.

La definizione della proprietà illustrata sopra è una proprietà di lettura/scrittura. Si noti la parola chiave `value` nella funzione di accesso impostata. La funzione di accesso `set` ha sempre un singolo parametro denominato `value`. La funzione di accesso `get` deve restituire un valore che è convertibile nel tipo della proprietà (in questo esempio `string`).
 
Queste sono le nozioni di basi sulla sintassi. Esistono numerose varianti che supportano un'ampia gamma di termini di progettazione diversi. Di seguito sono descritti i termini e le opzioni di sintassi per ogni termine.

## <a name="scenarios"></a>Scenari

Gli esempi precedenti hanno illustrato uno dei casi più semplici di definizione delle proprietà, ovvero una proprietà di lettura/scrittura senza convalida. Scrivendo il codice desiderato nelle funzioni di accesso `get` e `set` è possibile creare scenari diversi.

### <a name="validation"></a>Convalida

È possibile scrivere codice nella funzione di accesso `set` per assicurarsi che i valori rappresentati da una proprietà siano sempre validi. Ad esempio, si supponga che una regola per la classe `Person` preveda che il nome non può essere vuoto o uno spazio vuoto. Sarà necessario scrivere:

```csharp
public class Person
{
    public string FirstName
    {
        get => firstName;
        set
        {
            if (string.IsNullOrWhiteSpace(value))
                throw new ArgumentException("First name must not be blank");
            firstName = value;
        }
    }
    private string firstName;
    // remaining implementation removed from listing
}
```

L'esempio precedente applica la regola che prevede che il nome non può essere vuoto o uno spazio vuoto. Se lo sviluppatore scrive

```csharp
hero.FirstName = "";
```

L'assegnazione genera `ArgumentException`. Poiché la funzione di accesso di un insieme di proprietà deve avere un tipo restituito void, gli errori vengono segnalati nella funzione di accesso dell'insieme generando un'eccezione.

Questo è un caso semplice di convalida. La stessa sintassi può essere estesa a ogni elemento necessario nello scenario. È possibile controllare le relazioni tra le diverse proprietà o eseguire la convalida in base a qualsiasi condizione esterna. Tutte le istruzioni C# valide sono valide nella funzione di accesso di una proprietà.

### <a name="read-only"></a>Sola lettura

Le definizioni di proprietà descritte fino a questo punto si riferiscono a proprietà di lettura/scrittura con funzioni di accesso pubbliche. Non si tratta tuttavia dell'unica accessibilità valida per le proprietà.
È possibile creare proprietà di sola lettura o assegnare un'accessibilità diversa alle funzioni di accesso set e get. Si supponga che la classe `Person` debba consentire soltanto la modifica del valore della proprietà `FirstName` da altri metodi della classe. È possibile assegnare alla funzione di accesso set l'accessibilità `private` anziché `public`:

```csharp
public class Person
{
    public string FirstName { get; private set; }

    // remaining implementation removed from listing
}
```

L'accesso alla proprietà `FirstName` potrà quindi essere eseguito da qualsiasi codice, ma la proprietà potrà essere assegnata soltanto da altro codice della classe `Person`.

È possibile aggiungere qualsiasi modificatore di accesso restrittivo alle funzioni di accesso set o get. Il modificatore di accesso inserito nella singola funzione di accesso deve essere più restrittivo del modificatore di accesso della definizione della proprietà. Il codice precedente è valido poiché la proprietà `FirstName` è `public` e la funzione di accesso set è `private`. Non è possibile dichiarare una proprietà `private` con una funzione di accesso `public`. Le dichiarazioni di proprietà possono anche essere dichiarate `protected`, `internal`, `protected internal` o `private`.   

È anche consentito inserire il modificatore più restrittivo nella funzione di accesso `get`. Ad esempio, è possibile avere una proprietà `public` e limitare la funzione di accesso `get` a `private`. Questo scenario viene usato raramente.

È anche possibile limitare le modifiche a una proprietà, in modo che possa essere impostata solo in un costruttore o in un inizializzatore di proprietà. È possibile modificare in tal senso la classe `Person` come segue:

```csharp
public class Person
{
    public Person(string firstName)
    {
        this.FirstName = firstName;
    }

    public string FirstName { get; }

    // remaining implementation removed from listing
}
```

Questa funzionalità viene in genere usata per l'inizializzazione delle raccolte esposte come proprietà di sola lettura:

```csharp
public class Measurements
{
    public ICollection<DataPoint> points { get; } = new List<DataPoint>();
}
```

### <a name="computed-properties"></a>Proprietà calcolate

Una proprietà non si limita a restituire il valore di un campo membro. È possibile creare proprietà che restituiscono un valore calcolato. Espandere l'oggetto `Person` per restituire il nome completo, calcolato concatenando il nome e il cognome:

```csharp
public class Person
{
    public string FirstName { get; set; }

    public string LastName { get; set; }

    public string FullName { get { return $"{FirstName} {LastName}"; } }
}
```

L'esempio precedente usa la sintassi di *interpolazione della stringa* per creare la stringa formattata per il nome completo.

È anche possibile usare *membri con corpo di espressione* che consentono di creare la proprietà calcolata `FullName` in modo più conciso:

```csharp
public class Person
{
    public string FirstName { get; set; }

    public string LastName { get; set; }

    public string FullName =>  $"{FirstName} {LastName}";
}
```
 
I *membri con corpo di espressione* usano la sintassi di *espressione lambda* per definire un metodo che contiene una singola espressione. In questo caso, l'espressione restituisce il nome completo per l'oggetto person.

### <a name="lazy-evaluated-properties"></a>Proprietà con valutazione lazy

È possibile unire il concetto di proprietà calcolata al concetto di archiviazione e creare una *proprietà con valutazione lazy*.  Ad esempio, è possibile aggiornare la proprietà `FullName` in modo che venga eseguita soltanto la formattazione della stringa al primo accesso:

```csharp
public class Person
{
    public string FirstName { get; set; }

    public string LastName { get; set; }

    private string fullName;
    public string FullName
    {
        get
        {
            if (fullName == null)
                fullName = $"{FirstName} {LastName}";
            return fullName;
        }
    }
}
```

Il codice riportato sopra tuttavia contiene un bug. Se il codice aggiorna il valore della proprietà `FirstName` o `LastName`, il campo `fullName` valutato in precedenza non è valido. È necessario aggiornare le funzioni di accesso `set` della proprietà `FirstName` e `LastName` in modo che il campo `fullName` venga calcolato nuovamente:

```csharp
public class Person
{
    private string firstName;
    public string FirstName
    {
        get => firstName;
        set
        {
            firstName = value;
            fullName = null;
        }
    }

    private string lastName;
    public string LastName
    {
        get => lastName;
        set
        {
            lastName = value;
            fullName = null;
        }
    }

    private string fullName;
    public string FullName
    {
        get
        {
            if (fullName == null)
                fullName = $"{FirstName} {LastName}";
            return fullName;
        }
    }
}
```

La versione finale valuta la proprietà `FullName` solo quando necessario.
Se è valida, viene usata la versione calcolata in precedenza. Se un'altra modifica dello stato annulla la validità della versione calcolata in precedenza, la versione verrà ricalcolata. Non è necessario che gli sviluppatori che usano questa classe siano a conoscenza dei dettagli dell'implementazione. Nessuna di queste modifiche interne ha effetto sull'uso dell'oggetto Person. Questo è il motivo principale dell'uso delle proprietà per l'esposizione dei membri dati di un oggetto.
 
### <a name="inotifypropertychanged"></a>INotifyPropertyChanged

Uno scenario finale in cui è necessario scrivere codice nella funzione di accesso di una proprietà è quello finalizzato al supporto dell'interfaccia `INotifyPropertyChanged` usata per inviare ai client di data binding la notifica della modifica di un valore. Quando viene modificato il valore di una proprietà, l'oggetto genera l'evento `PropertyChanged` per indicare la modifica. Le librerie di data binding aggiornano a loro volta gli elementi visualizzati in base alla modifica. Il codice seguente illustra come implementare `INotifyPropertyChanged` per la proprietà `FirstName` della classe person.

```csharp
public class Person : INotifyPropertyChanged
{
    public string FirstName
    {
        get => firstName;
        set
        {
            if (string.IsNullOrWhiteSpace(value))
                throw new ArgumentException("First name must not be blank");
            if (value != firstName)
            {
                PropertyChanged?.Invoke(this, 
                    new PropertyChangedEventArgs(nameof(FirstName)));
            }
            firstName = value;
        }
    }
    private string firstName;

    public event PropertyChangedEventHandler PropertyChanged;
    // remaining implementation removed from listing
}
```

L'operatore `?.` è chiamato *operatore condizionale Null*. L'operatore cerca un riferimento Null prima di eseguire la valutazione della parte destra dell'operatore. Se non vengono trovati sottoscrittori dell'evento `PropertyChanged`, il codice che genera l'evento non viene eseguito. In questo caso, verrà generato `NullReferenceException` senza eseguire il controllo. Per altre informazioni, vedere la pagina relativa a [`events`](delegates-events.md). Questo esempio usa anche il nuovo operatore `nameof` per convertire il simbolo del nome della proprietà nella rappresentazione di testo.
L'uso di `nameof` può ridurre gli errori nel caso in cui il nome della proprietà sia stato digitato erroneamente.

Anche questo è un esempio di un caso in cui è possibile scrivere codice nelle funzioni di accesso per supportare gli scenari necessari.

## <a name="summing-up"></a>Conclusioni

Le proprietà sono una forma di campi intelligenti in una classe o un oggetto. All'esterno dell'oggetto, vengono visualizzate come campi dell'oggetto. Tuttavia, le proprietà possono essere implementate usando l'intera gamma di funzionalità di C#.
È possibile specificare la convalida, un'accessibilità diversa, la valutazione lazy o tutti i requisiti necessari negli scenari.

