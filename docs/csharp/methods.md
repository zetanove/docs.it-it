---
title: Metodi | Guida a C#
description: Panoramica dei metodi e dei parametri e dei valori restituiti dei metodi
keywords: .NET, .NET Core, C#
author: rpetrusha
ms.author: ronpet
ms.date: 10/26/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 577a8527-1081-4b36-9b9e-0685b6553c6e
ms.translationtype: Human Translation
ms.sourcegitcommit: 81f31f1abc9db14b6b899564d67ca6e90d269ad7
ms.openlocfilehash: 42ded63bacfb6ff2ceadde6fa37c7bddb413a933
ms.contentlocale: it-it
ms.lasthandoff: 04/11/2017

---
# <a name="methods"></a>Metodi #

Un metodo è un blocco di codice che contiene una serie di istruzioni. Un programma fa in modo che le istruzioni vengano eseguite chiamando il metodo e specificando gli argomenti del metodo obbligatori. In C#, ogni istruzione eseguita viene attuata nel contesto di un metodo. Il metodo `Main` è il punto di ingresso per ogni applicazione C# e viene chiamato da Common Language Runtime (CLR) quando viene avviato il programma.

> [!NOTE]
> In questo argomento vengono descritti i metodi denominati. Per informazioni sulle funzioni anonime, vedere [Funzioni anonime](https://msdn.microsoft.com/library/bb882516.aspx).

Di seguito sono elencate le diverse sezioni di questo argomento:

- [Firme del metodo](#signatures)
- [Chiamata del metodo](#invocation)
- [Metodi ereditati e sottoposti a override](#inherited)
- [Passaggio di parametri](#passing)
  - [Passaggio di parametri per valore](#byval)
  - [Passaggio di parametri per riferimento](#byref)
  - [Matrici di parametri](#paramarray)
- [Parametri e argomenti facoltativi](#optional)
- [Valori restituiti](#return)
- [Metodi di estensione](#extension)
- [Metodi asincroni](#async)
- [Membri con corpo di espressione](#expr)
- [Iteratori](#iterators)

<a name="signatures"></a>
## <a name="method-signatures"></a>Firme del metodo ##

I metodi vengono dichiarati in `class` o `struct` specificando:

- Un livello di accesso facoltativo, ad esempio `public` o `private`. Il valore predefinito è `private`.
- Modificatori facoltativi, ad esempio `abstract` o `sealed`.
- Il valore restituito o `void` se il metodo non ha alcun valore.
- Nome del metodo.
- Tutti i parametri del metodo. I parametri del metodo vengono racchiusi tra parentesi e separati da virgole. Le parentesi vuote indicano che il metodo non richiede parametri.

Queste parti costituiscono la firma del metodo.

> [!NOTE]
> Un tipo restituito di un metodo non fa parte della firma del metodo in caso di overload dei metodi. Fa tuttavia parte della firma del metodo quando si determina la compatibilità tra un delegato e il metodo a cui fa riferimento.

L'esempio seguente definisce una classe denominata `Motorcycle` che contiene cinque metodi:

[!code-csharp[csSnippets.Methods#40](../../samples/snippets/csharp/concepts/methods/methods40.cs#40)]

Si noti che la classe `Motorcycle` include un metodo sottoposto a overload, ovvero `Drive`. Due metodi hanno lo stesso nome, ma devono essere differenziati in base ai relativi tipi di parametri.

<a name="invocation"></a>
## <a name="method-invocation"></a>Chiamata del metodo ##

I metodi possono essere di *istanza* o *statici*. Per chiamare un metodo di istanza è necessario creare un'istanza di un oggetto e chiamare il metodo nell'oggetto; un metodo di istanza agisce sull'istanza e i relativi dati. La chiamata a un metodo statico viene eseguita facendo riferimento al nome del tipo a cui appartiene il metodo; i metodi statici non agiscono sui dati dell'istanza. Se si tenta di chiamare un metodo statico attraverso un'istanza di un oggetto viene generato un errore del compilatore.

La chiamata a un metodo è un'operazione analoga all'accesso a un campo. Dopo il nome dell'oggetto (in una chiamata a un metodo di istanza) o il nome del tipo (in una chiamata a un metodo `static`), aggiungere un punto, il nome del metodo e le parentesi. Gli argomenti vengono elencati tra parentesi e separati da virgole.

La definizione del metodo specifica i nomi e i tipi di tutti i parametri obbligatori. Quando il chiamante chiama il metodo, specifica valori concreti, chiamati argomenti, per ogni parametro. Gli argomenti devono essere compatibili con il tipo di parametro, ma il nome dell'argomento, se usato nel codice chiamante, non deve essere lo stesso del parametro denominato definito nel metodo. Nell'esempio seguente il metodo `Square` include un singolo parametro di tipo `int` denominato *i*. La prima chiamata al metodo passa al metodo `Square` una variabile di tipo `int` denominata *num*, la seconda passa una costante numerica e la terza passa un'espressione.

[!code-csharp[csSnippets.Methods#74](../../samples/snippets/csharp/concepts/methods/params74.cs#74)]

La forma più comune di chiamata al metodo usa argomenti posizionali; specifica gli argomenti nello stesso ordine dei parametri del metodo. Per questa ragione, i metodi della classe `Motorcycle` possono essere chiamati come nell'esempio seguente. La chiamata al metodo `Drive`, ad esempio, include due argomenti che corrispondono ai due parametri nella sintassi del metodo. Il primo diventa il valore del parametro `miles`, il secondo il valore del parametro `speed`.

[!code-csharp[csSnippets.Methods#41](../../samples/snippets/csharp/concepts/methods/methods40.cs#41)]

Quando si esegue una chiamata a un metodo è anche possibile usare *argomenti denominati* anziché argomenti posizionali. Quando si usano gli argomenti denominati, si specifica il nome del parametro seguito da due punti (":") e l'argomento. Gli argomenti del metodo possono essere in qualsiasi ordine, a condizione che siano presenti tutti gli argomenti necessari. L'esempio seguente usa gli argomenti denominati per richiamare il metodo `TestMotorcycle.Drive`. In questo esempio gli argomenti denominati vengono passati nell'ordine inverso dall'elenco di parametri del metodo.

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/named1.cs#45)]

È possibile richiamare un metodo usando argomenti posizionali e denominati. Un argomento posizionale non può, tuttavia, seguire un argomento denominato. L'esempio seguente richiama il metodo `TestMotorcycle.Drive` dall'esempio precedente usando un argomento posizionale e un argomento denominato.

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/named2.cs#46)]

 <a name="inherited"></a>
 ##<a name="inherited-and-overridden-methods"></a>Metodi ereditati e sottoposti a override ##

Oltre ai membri definiti in modo esplicito in un tipo, un tipo eredita i membri definiti nelle relative classi base. Poiché tutti i tipi del sistema di tipi gestiti ereditano direttamente o indirettamente dalla classe @System.Object, tutti i tipi di ereditano i relativi membri, ad esempio @System.Object.Equals(System.Object), @System.Object.GetType e @System.Object.ToString. L'esempio seguente definisce una classe `Person`, crea l'istanza di due oggetti `Person` e chiama il metodo `Person.Equals` per determinare se i due oggetti sono uguali. Il metodo `Equals`, tuttavia, non è definito nella classe `Person`; viene ereditato da @System.Object.

[!code-csharp[csSnippets.Methods#104](../../samples/snippets/csharp/concepts/methods/inherited1.cs#104)]

I tipi possono eseguire l'override dei membri ereditati usando la parola chiave `override` e specificando un'implementazione per il metodo sottoposto a override. La firma del metodo deve essere la stessa del metodo sottoposto a override. L'esempio seguente è simile a quello precedente, ad eccezione del fatto che viene eseguito l'override del metodo @Object.Equals(System.Object). Viene anche eseguito l'override del metodo @Object.GetHashCode poiché i due metodi devono fornire risultati coerenti.

[!code-csharp[csSnippets.Methods#105](../../samples/snippets/csharp/concepts/methods/overridden1.cs#105)]

<a name="passing"></a>
## <a name="passing-parameters"></a>Passaggio di parametri ##

I tipi in C# sono *tipi di valore* o *tipi di riferimento*. Per un elenco dei tipi di valore predefiniti, vedere [Tipi e variabili](./tour-of-csharp/types-and-variables.md). Per impostazione predefinita, i tipi di valore e i tipi di riferimento vengono passati a un metodo per valore.

<a name="byval"></a>
### <a name="passing-parameters-by-value"></a>Passaggio di parametri per valore ###

Quando un tipo valore viene passato a un metodo per valore, viene passata al metodo una copia dell'oggetto anziché l'oggetto stesso. Di conseguenza, le modifiche all'oggetto nel metodo chiamato non hanno effetto sull'oggetto originale quando il controllo torna al chiamante.

L'esempio seguente passa un tipo di valore a un metodo per valore e il metodo chiamato tenta di modificare il valore del tipo di valore. Definisce una variabile di tipo `int`, che è un tipo di valore, ne inizializza il valore a 20 e la passa a un metodo denominato `ModifyValue` che modifica il valore della variabile in 30. Quando il metodo viene restituito, tuttavia, il valore della variabile rimane invariato.

[!code-csharp[csSnippets.Methods#10](../../samples/snippets/csharp/concepts/methods/byvalue10.cs#10)]

Quando viene passato un oggetto di tipo riferimento a un metodo per valore, viene passato un riferimento all'oggetto per valore, ovvero il metodo riceve un argomento che indica la posizione dell'oggetto, ma non l'oggetto stesso. Se si modifica un membro dell'oggetto usando questo riferimento, la modifica si riflette nell'oggetto quando il controllo torna al metodo chiamante. Tuttavia, la sostituzione dell'oggetto passato al metodo non ha effetto sull'oggetto originale quando il controllo torna al chiamante.

L'esempio seguente definisce una classe (che è un tipo riferimento) denominata `SampleRefType`. Crea un'istanza di un oggetto `SampleRefType`, assegna 44 al campo `value` e passa l'oggetto al metodo `ModifyObject`. L'esempio è sostanzialmente uguale al precedente in quanto passa un argomento per valore a un metodo ma, essendo usato un tipo riferimento, il risultato è diverso. La modifica eseguita in `ModifyObject` al campo `obj.value` cambia anche il campo `value` dell'argomento `rt` nel metodo `Main` in 33, come mostra l'output dell'esempio.

[!code-csharp[csSnippets.Methods#42](../../samples/snippets/csharp/concepts/methods/byvalue42.cs#42)]

<a name="byref"></a>
### <a name="passing-parameters-by-reference"></a>Passaggio di parametri per riferimento ###

Si passa un parametro per riferimento quando si vuole modificare il valore di un argomento in un metodo e si vuole riflettere tale modifica quando il controllo torna al metodo chiamante. Per passare un parametro per riferimento, usare la parola chiave `ref` o `out`.

L'esempio seguente è identico a quello precedente, ad eccezione del fatto che il valore viene passato per riferimento al metodo `ModifyValue`. Quando il valore del parametro è modificato nel metodo `ModifyValue`, la modifica del valore si riflette quando il controllo torna al chiamante.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/byref106.cs#106)]

Un modello comune che usa parametri di riferimento implica lo scambio dei valori delle variabili. Si passano due variabili a un metodo per riferimento e il metodo scambia il loro contenuto. L'esempio seguente scambia i valori integer.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/swap107.cs#107)]

Il passaggio di un parametro di tipo riferimento consente di modificare il valore del riferimento stesso anziché il valore dei singoli elementi o campi.

<a name="paramarray"></a>
### <a name="parameter-arrays"></a>Matrici di parametri ###

In alcuni casi, il requisito che richiede di specificare il numero esatto di argomenti per il metodo è limitativo. Usando la parola chiave `params` per indicare che un parametro è una matrice di parametri, si consente la chiamata al metodo con un numero variabile di argomenti. Il parametro contrassegnato con la parola chiave `params` deve essere di tipo matrice e deve essere l'ultimo parametro dell'elenco di parametri del metodo.

Un chiamante potrà quindi richiamare il metodo in uno dei tre modi seguenti:

- Passando una matrice del tipo appropriato che contiene il numero desiderato di elementi.
- Passando un elenco delimitato da virgole di singoli argomenti del tipo appropriato al metodo.
- Non specificando un argomento nella matrice di parametri.

L'esempio seguente definisce un metodo denominato `DoStringOperation` che esegue l'operazione di stringa specificata dal primo parametro, un membro di enumerazione `StringOperation`. Le stringhe in cui deve essere eseguita l'operazione sono definite da una matrice di parametri. Il metodo `Main` illustra tutti e tre i metodi di chiamata al metodo. Si noti che il metodo contrassegnato con la parola chiave `params` deve essere preparato a gestire il caso in cui non viene specificato alcun argomento per la matrice di parametri, in modo che il relativo valore sia `null`.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/byref108.cs#108)]

<a name="optional"></a>
## <a name="optional-parameters-and-arguments"></a>Parametri e argomenti facoltativi ##

La definizione di un metodo può specificare che i parametri sono obbligatori o facoltativi. I parametri sono obbligatori per impostazione predefinita. I parametri facoltativi vengono specificati includendo il valore predefinito del parametro nella definizione del metodo. Quando il metodo viene chiamato, se non sono specificati argomenti per un parametro facoltativo, viene usato il valore predefinito.

Il valore predefinito del parametro deve essere assegnato da uno dei tipi di espressioni seguenti:

- Una costante, ad esempio una stringa letterale o un numero.
- Un'espressione del form `new ValType`, dove `ValType` è un tipo di valore. Si noti che viene richiamato il costruttore predefinito implicito del tipo di valore, che non è un membro effettivo del tipo.
- Un'espressione del form `default(ValType)`, dove `ValType` è un tipo di valore.

Se un metodo include parametri obbligatori e facoltativi, i parametri facoltativi sono definiti alla fine dell'elenco di parametri, dopo tutti i parametri obbligatori.

L'esempio seguente definisce un metodo, `ExampleMethod`, con un parametro obbligatorio e due facoltativi.

[!code-csharp[csSnippets.Methods#21](../../samples/snippets/csharp/concepts/methods/optional1.cs#21)]

Se viene richiamato un metodo con più argomenti facoltativi usando argomenti posizionali, il chiamante deve specificare un argomento per tutti i parametri facoltativi, dal primo all'ultimo parametro per il quale è specificato un argomento. Nel caso del metodo `ExampleMethod`, ad esempio, se il chiamante specifica un argomento per il parametro `description`, deve specificarne uno anche per il parametro `optionalInt`. `opt.ExampleMethod(2, 2, "Addition of 2 and 2");` è una chiamata a un metodo valido; `opt.ExampleMethod(2, , "Addition of 2 and 0);` genera un errore di compilazione "Argomento mancante".

Se un metodo viene chiamato usando argomenti denominati o una combinazione di argomenti posizionali e denominati, il chiamante può omettere tutti gli argomenti successivi all'ultimo argomento posizionale nella chiamata al metodo.

L'esempio seguente esegue una chiamata al metodo `ExampleMethod` tre volte.  Le prime due chiamate al metodo usano argomenti posizionali. La prima omette entrambi gli argomenti facoltativi, mentre la seconda omette l'ultimo argomento. La terza chiamata al metodo specifica un argomento posizionale per il parametro obbligatorio, ma usa un argomento denominato per specificare un valore per il parametro `description` omettendo l'argomento `optionalInt`.

[!code-csharp[csSnippets.Methods#22](../../samples/snippets/csharp/concepts/methods/optional1.cs#22)]

L'uso di parametri facoltativi ha effetto sulla *risoluzione dell'overload* o sulla modalità con la quale il compilatore C# determina l'overload specifico da richiamare tramite una chiamata al metodo come descritto di seguito:

- Un metodo, un indicizzatore o un costruttore è un candidato per l'esecuzione se ogni parametro è facoltativo o corrisponde, per nome o per posizione, a un solo argomento nell'istruzione chiamante e tale argomento può essere convertito nel tipo del parametro.
- Se è disponibile più di un candidato, agli argomenti specificati in modo esplicito vengono applicate le regole di risoluzione dell'overload per le conversioni preferite. Gli argomenti omessi per i parametri facoltativi vengono ignorati.
- Se due candidati sono giudicati ugualmente validi, la preferenza va a un candidato che non ha parametri facoltativi per i quali sono stati omessi gli argomenti nella chiamata. Si tratta di una conseguenza di una preferenza generale nella risoluzione dell'overload per i candidati che hanno un numero di parametri inferiore.

 <a name="return"></a>
 ## <a name="return-values"></a>Valori restituiti ##

I metodi possono restituire un valore al chiamante. Se il tipo restituito, ovvero il tipo elencato prima del nome del metodo, non è `void`, il metodo può restituire il valore usando la parola chiave `return`. Un'istruzione con la parola chiave `return` seguita da una variabile, una costante o un'espressione corrispondente al tipo restituito restituirà tale valore al chiamante del metodo. Per usare la parola chiave `return` per restituire un valore, sono obbligatori metodi con un tipo restituito non void. La parola chiave `return` interrompe anche l'esecuzione del metodo.

Se il tipo restituito è `void`, un'istruzione `return` senza un valore è tuttavia utile per interrompere l'esecuzione del metodo. Senza la parola chiave `return` , l'esecuzione del metodo verrà interrotta quando verrà raggiunta la fine del blocco di codice.

Ad esempio, questi due metodi usano la parola chiave `return` per restituire numeri interi:

[!code-csharp[csSnippets.Methods#44](../../samples/snippets/csharp/concepts/methods/return44.cs#44)]

Per usare un valore restituito da un metodo, il metodo chiamante può usare la chiamata al metodo stessa ovunque è sufficiente un valore dello stesso tipo. È inoltre possibile assegnare il valore restituito a una variabile. I due esempi seguenti di codice ottengono lo stesso risultato:

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/return44.cs#45)]

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/return44.cs#46)]

L'uso di una variabile locale, in questo caso `result`, per archiviare un valore è facoltativo. Potrebbe migliorare la leggibilità del codice o potrebbe essere necessario se si desidera archiviare il valore originale dell'argomento per l'intero ambito del metodo.

In alcuni casi, si vuole che il metodo restituisca più di un singolo valore. A questo scopo, a partire da C# 7.0 è possibile usare *tipi di tupla* e *letterali di tupla*. Il tipo di tupla definisce i tipi di dati degli elementi della tupla. I letterali di tupla specificano i valori effettivi della tupla restituita. Nell'esempio seguente `(string, string, string, int)` definisce il tipo di tupla restituito dal metodo `GetPersonalInfo`. L'espressione `(per.FirstName, per.MiddleName, per.LastName, per.Age)` è il letterale della tupla; il metodo restituisce il nome iniziale, centrale e finale e la durata di un oggetto `PersonInfo`.

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    if (per != null)
       return (per.FirstName, per.MiddleName, per.LastName, per.Age);
    else
       return null;
}
```

Il chiamante può quindi usare la tupla restituita con codice simile al seguente:

```csharp
var person = GetPersonalInfo("111111111")
if (person != null)
   Console.WriteLine("{person.Item1} {person.Item3}: age = {person.Item4}");
```

È anche possibile assegnare i nomi agli elementi della tupla nella definizione del tipo della tupla. L'esempio seguente mostra una versione alternativa del metodo `GetPersonalInfo` che usa elementi denominati:

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    if (per != null)
       return (per.FirstName, per.MiddleName, per.LastName, per.Age);
    else
       return null;
}
```

La chiamata precedente al metodo `GetPersonInfo` può quindi essere modificata come segue:

```csharp
var person = GetPersonalInfo("111111111");
if (person != null)
   Console.WriteLine("{person.FName} {person.LName}: age = {person.Age}");
```

Se a un metodo viene passata una matrice come argomento e il metodo modifica il valore dei singoli elementi, non è necessario che il metodo restituisca la matrice, anche se è possibile scegliere di effettuare questa operazione per ragioni di stile o per il flusso funzionale di valori.  L'operazione non è necessaria perché C# passa tutti i tipi riferimento per valore e il valore di un riferimento a una matrice è il puntatore alla matrice. Nell'esempio seguente le modifiche al contenuto della matrice `values` eseguite nel metodo `DoubleValues` sono rilevabili da qualsiasi codice che include un riferimento alla matrice.

[!code-csharp[csSnippets.Methods#101](../../samples/snippets/csharp/concepts/methods/returnarray1.cs#101)]

 <a name="exten"></a>
 ## <a name="extension-methods"></a>Metodi di estensione ##

In genere, è possibile aggiungere un metodo a un tipo esistente in due modi:

- Modificare il codice sorgente per il tipo. Questa operazione non è possibile se non si è proprietari del codice sorgente del tipo. Questa operazione diventa una modifica importante se si aggiungono anche tutti i campi dati privati per supportare il metodo.
- Definire il nuovo metodo in una classe derivata. Non è possibile aggiungere un metodo in questo modo usando l'ereditarietà per gli altri tipi, ad esempio strutture ed enumerazioni. Questo modo non può essere usato neanche per "aggiungere" un metodo a una classe sealed.

I metodi di estensione consentono di "aggiungere" un metodo a un tipo esistente senza modificare il tipo o implementare il nuovo metodo in un tipo ereditato. È necessario anche che il metodo di estensione non si trovi nello stesso assembly del tipo che estende. Un metodo di estensione viene chiamato come se fosse un membro definito di un tipo.

Per altre informazioni, vedere [Metodi di estensione](https://msdn.microsoft.com/library/bb383977.aspx).

<a name="async"></a>
## <a name="async-methods"></a>Metodi asincroni ##

Tramite la funzionalità async, è possibile richiamare i metodi asincroni senza usare callback espliciti o suddividere manualmente il codice in più metodi o espressioni lambda.

Se si contrassegna un metodo con il modificatore [async](https://msdn.microsoft.com/library/hh156513.aspx), è possibile usare l'operatore [await](https://msdn.microsoft.com/library/hh156528.aspx) nel metodo. Quando il controllo raggiunge un'espressione `await` nel metodo asincrono, il controllo torna al chiamante se l'attività attesa non è stata completata e l'avanzamento nel metodo con la parola chiave `await` viene sospeso fino al completamento dell'attività attesa. Una volta completata l'attività, l'esecuzione del metodo può riprendere.

> [!NOTE]
> Un metodo async viene restituito al chiamante quando rileva il primo oggetto atteso che non è ancora completo o raggiunge la fine del metodo async, qualunque si verifichi prima.

Un metodo asincrono può avere un tipo restituito @System.Threading.Tasks.Task<TResult>, @System.Threading.Tasks.Task o `void`. Il tipo restituito `void` viene usato principalmente per definire i gestori eventi in cui è necessario un tipo restituito `void`. Un metodo asincrono che restituisce `void` non può essere atteso e il chiamante di un metodo che restituisce void non può intercettare le eccezioni generate dal metodo. Questa limitazione verrà risolta al rilascio di C# 7 per consentire a un metodo asincrono di [restituire qualsiasi tipo attività](https://github.com/ljw1004/roslyn/blob/features/async-return/docs/specs/feature%20-%20arbitrary%20async%20returns.md).

Nell'esempio seguente `DelayAsync` è un metodo asincrono con un'istruzione return che restituisce un valore Integer. Poiché si tratta di un metodo asincrono, la dichiarazione del metodo deve avere un tipo restituito di `Task<int>`. Poiché il tipo restituito è `Task<int>`, la valutazione dell'espressione `await` in `DoSomethingAsync` genera un numero intero come dimostra l'istruzione `int result = await delayTask` seguente.

[!code-csharp[csSnippets.Methods#102](../../samples/snippets/csharp/concepts/methods/async1.cs#102)]

Un metodo asincrono non può dichiarare parametri [ref](https://msdn.microsoft.com/library/14akc2c7.aspx) o [out](https://msdn.microsoft.com/library/t3c3bfhx.aspx) , ma può chiamare metodi che hanno tali parametri.

 Per altre informazioni sui metodi asincroni, vedere [Programmazione asincrona con Async e Await](https://msdn.microsoft.com/library/mt674882.aspx), [Flusso di controllo in programmi asincroni](https://msdn.microsoft.com/library/mt674892.aspx) e [Tipi restituiti asincroni](https://msdn.microsoft.com/library/mt674893.aspx).

<a name="expr"></a>
## <a name="expression-bodied-members"></a>Membri con corpo di espressione ##

È comune disporre di definizioni di metodo che semplicemente restituiscono subito il risultato di un'espressione o che includono una singola istruzione come corpo del metodo.  Esiste una sintassi breve per definire tali metodi usando `=>`:

```csharp

public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);

```

Se il metodo restituisce `void` o è un metodo asincrono, il corpo del metodo deve essere un'espressione di istruzione (come per le espressioni lambda).  Le proprietà e gli indicizzatori devono essere di sola lettura e non è necessario usare la parola chiave della funzione di accesso `get` .

<a name="iterators"></a>
## <a name="iterators"></a>Iteratori ##

Un iteratore esegue un'iterazione personalizzata su una raccolta, ad esempio un elenco o una matrice. Un iteratore usa l'istruzione [yield return](https://msdn.microsoft.com/library/9k7k7cf0.aspx) per restituire un elemento alla volta. Quando viene raggiunta un'istruzione `yield return`, viene memorizzata la posizione corrente in modo che il chiamante possa richiedere l'elemento successivo della sequenza.

Il tipo restituito di un iteratore può essere @System.Collections.IEnumerable, @System.Collections.Generic.IEnumerable%601, @System.Collections.IEnumerator o @System.Collections.Generic.IEnumerator%601.

Per altre informazioni, vedere [Iteratori](https://msdn.microsoft.com/library/mt639331.aspx).

## <a name="see-also"></a>Vedere anche ##

[Modificatori di accesso](https://msdn.microsoft.com/library/wxh6fsc7.aspx)
[Classi statiche e membri di classi statiche ](https://msdn.microsoft.com/library/79b3xss3.aspx)
[Ereditarietà](https://msdn.microsoft.com/library/ms173149.aspx)
[Classi e membri delle classi astratte e sealed](https://msdn.microsoft.com/library/ms173150.aspx)
[params](https://msdn.microsoft.com/library/w5zay9db.aspx)
[out](https://msdn.microsoft.com/library/t3c3bfhx.aspx)
[ref](https://msdn.microsoft.com/library/14akc2c7.aspx)
[Passaggio di parametri](https://msdn.microsoft.com/library/0f66670z.aspx)

