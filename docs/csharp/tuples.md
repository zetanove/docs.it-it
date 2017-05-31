---
title: Tuple | Guida per C#
description: Informazioni sui tipi di tupla denominati e non denominati in C#
keywords: .NET, .NET Core, C#
author: BillWagner
ms-author: wiwagn
ms.date: 11/23/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: ee8bf7c3-aa3e-4c9e-a5c6-e05cc6138baa
ms.translationtype: Human Translation
ms.sourcegitcommit: 6b30f41e3fb07a962542a09a41c698efee7ebb5a
ms.openlocfilehash: 0ea7299d87dc69784e3bed93e48d83e4a0076a20
ms.contentlocale: it-it
ms.lasthandoff: 04/26/2017

---

# <a name="c-tuple-types"></a>Tipi di tupla di C# #

Le tuple in C# sono tipi definiti tramite una sintassi leggera. I vantaggi includono una sintassi più semplice, regole per le conversioni basate su numero (detto "grado") e tipi di campi, nonché regole coerenti per le copie e le assegnazioni. Come un compromesso, le tuple non supportano gli idiomi orientati agli oggetti associati all'ereditarietà. È possibile ottenere una panoramica della sezione nell'argomento [Tuples in the What's new in C# 7](whats-new/csharp-7.md#tuples) (Tuple in Novità di C# 7).

Questo argomento descrive le regole del linguaggio che controllano le tuple in C# 7, le diverse modalità di uso delle stesse e una guida iniziale per l'uso delle tuple.

> [!NOTE]
> Le nuove funzionalità delle tuple richiedono il tipo `System.ValueTuple`. Per Visual Studio 2017, è necessario aggiungere il pacchetto NuGet [System.ValueTuple](https://www.nuget.org/packages/System.ValueTuple/), disponibile nella Raccolta NuGet.
> Senza questo pacchetto potrebbe essere riscontrato un errore di compilazione simile a `error CS8179: Predefined type 'System.ValueTuple``2' is not defined or imported` o `error CS8137: Cannot define a class or member that utilizes tuples because the compiler required type 'System.Runtime.CompilerServices.TupleElementNamesAttribute' cannot be found.`

Iniziamo dai motivi dell'aggiunta del nuovo supporto per le tuple. I metodi restituiscono un oggetto singolo. Le tuple consentono di creare più facilmente pacchetti di valori multipli in questo oggetto singolo. 

.NET Framework dispone già di classi `Tuple` generiche. Queste classi, tuttavia, presentano due limitazioni principali. Da un lato, le classi `Tuple` hanno denominato i campi `Item1`, `Item2` e così via. Questi nomi non includono informazioni semantiche. L'uso di questi tipi `Tuple` non consente di comunicare il significato di ciascun campo. Un altro problema è costituito dal fatto che le classi `Tuple` sono tipi di riferimento. L'uso di uno dei tipi `Tuple` si traduce nell'allocazione di oggetti. Nei percorsi critici, ciò può avere un impatto notevole sulle prestazioni dell'applicazione.

Per evitare tali problematiche, è possibile creare un `class` o `struct` per supportare più campi. Sfortunatamente, ciò comporta più lavoro per l'utente e rende poco chiare le finalità. Compilare uno `struct` o una `class` implica la definizione di un tipo con dati e comportamento. In molti casi, si desidera semplicemente archiviare più valori in un singolo oggetto.

Le nuove funzionalità del linguaggio per le tuple, combinate con un nuovo set di classi nel framework, risolvono queste problematiche. Queste nuove tuple usano i nuovi struct generici `ValueTuple`. Come suggerisce il nome, questo tipo è uno `struct` invece di una `class`. Sono disponibili versioni diverse di questo struct per supportare le tuple con diversi numeri di campi. Il supporto del nuovo linguaggio fornisce nomi semantici per i campi del tipo di tupla, oltre alle funzionalità per agevolare la costruzione o l'accesso ai campi della tupla.

Le funzionalità del linguaggio e gli struct `ValueTuple` generici applicano la regola che impedisce all'utente di aggiungere comportamenti (metodi) a questi tipi di tupla.
Tutti i tipi `ValueTuple` sono *struct modificabili*. Ogni campo del membro è un campo pubblico. Questo rende i campi molto leggeri. Tuttavia, ciò implica che le tuple non devono essere usate nei contesti in cui l'immutabilità è un fattore importante.

Le tuple sono contenitori di dati più semplici e flessibili rispetto ai tipi `class` e `struct`. Esaminiamo queste differenze.

## <a name="named-and-unnamed-tuples"></a>Tuple con e senza nome

Lo struct `ValueTuple` include campi denominati `Item1`, `Item2`, `Item3` e così via, più simili alle proprietà definite nei tipi `Tuple` esistenti.
Questi nomi sono gli unici nomi che è possibile usare per le *tuple senza nome*. Quando non si forniscono alla tupla nomi alternativi per i campi, viene creata una tupla senza nome:

[!code-csharp[Tupla senza nome](../../samples/snippets/csharp/tuples/tuples/program.cs#01_UnNamedTuple "Tupla senza nome")]

Tuttavia, quando si inizializza una tupla, è possibile usare nuove funzionalità del linguaggio che assegnano a ciascun campo un nome più semplice. In questo modo viene creata una *tupla con nome*.
Le tuple con nome dispongono ancora di campi denominati `Item1`, `Item2`, `Item3` e così via.
Ma dispongono anche di sinonimi per i campi a cui l'utente ha assegnato un nome.
Creare una tupla con nome specificando i nomi per ogni campo. Un modo consiste nello specificare i nomi come parte dell'inizializzazione della tupla:

[!code-csharp[Tupla con nome](../../samples/snippets/csharp/tuples/tuples/program.cs#02_NamedTuple "Tupla con nome")]

I sinonimi vengono gestiti dal compilatore e dal linguaggio in modo che sia possibile usare efficacemente le tuple con nome. Gli editor e gli IDE possono leggere questi nomi semantici tramite le API di Roslyn. In questo modo è possibile fare riferimento ai campi di una tupla con nome tramite questi nomi semantici in qualsiasi punto dello stesso assembly. Il compilatore sostituisce i nomi definiti con equivalenti `Item*` durante la generazione dell'output compilato. Il Microsoft Intermediate Language (MSIL) compilato non include i nomi assegnati ai campi. 

Il compilatore deve comunicare tali nomi creati per le tuple, restituiti dalle proprietà o dai metodi pubblici. In questi casi, il compilatore aggiunge un attributo `TupleElementNames` al metodo. Questo attributo contiene una proprietà dell'elenco `TransformNames` che presenta i nomi assegnati a ognuno dei campi nella tupla. 

> [!NOTE]
> Anche gli strumenti di sviluppo come Visual Studio consentono di leggere i metadati e di fornirli a IntelliSense e ad altre funzionalità tramite i nomi dei campi dei metadati.

È importante comprendere questi principi fondamentali delle nuove tuple e del tipo `ValueTuple` per comprendere le regole per la mutua assegnazione delle tuple con nome.

## <a name="assignment-and-tuples"></a>Assegnazione e tuple

Il linguaggio supporta l'assegnazione tra tipi di tupla che hanno lo stesso numero di campi e conversioni implicite dei tipi per ognuno di tali campi. Non sono considerate altre conversioni per le assegnazioni. Esaminiamo i tipi di assegnazioni consentiti tra i tipi di tupla.

Considerare le variabili usate negli esempi seguenti:

[!code-csharp[Creazione variabili](../../samples/snippets/csharp/tuples/tuples/program.cs#03_VariableCreation "Creazione variabili")]

Le prime due variabili, `unnamed` e `anonymous` non hanno nomi semantici forniti per i campi. I nomi dei campi sono `Item1` e `Item2`.
Le ultime due variabili, `named` e `differentName` hanno nomi semantici attribuiti ai campi. Si noti che queste due tuple presentano nomi diversi per i campi.

Tutte e quattro le tuple hanno lo stesso numero di campi (detto "grado") e i tipi di tali campi sono identici. Pertanto, tutte queste assegnazioni funzionano:

[!code-csharp[Assegnazione variabili](../../samples/snippets/csharp/tuples/tuples/program.cs#04_VariableAssignment "Assegnazione variabili")]

Si noti che non sono assegnati i nomi delle tuple. I valori dei campi vengono assegnati seguendo l'ordine dei campi nella tupla.

Le tuple di tipo diverso o con numero di campi diverso non possono essere assegnate:

```csharp
// Does not compile.
// CS0029: Cannot assign Tuple(int,int,int) to Tuple(int, string)
var differentShape = (1, 2, 3);
named = differentShape;
```

## <a name="tuples-as-method-return-values"></a>Tuple come valori restituiti dal metodo

Uno degli usi più comuni per le tuple è come valore restituito dal metodo. Di seguito viene illustrato un esempio. Si consideri il metodo che calcola la deviazione standard per una sequenza di numeri:

[!code-csharp[Deviazione standard](../../samples/snippets/csharp/tuples/tuples/statistics.cs#05_StandardDeviation "Deviazione standard")]

> [!NOTE]
> Questi esempi calcolano la deviazione standard non corretta di esempio.
> La formula di deviazione standard non corretta di esempio consiste nel dividere la somma dei quadrati delle differenze rispetto al valore medio per (N-1) invece di N, come fa il metodo di estensione `Average`. Per altre informazioni sulle differenze tra queste formule di deviazione standard, consultare un testo di statistica.

Segue la formula per la deviazione standard tratta dal libro di testo. Genera la risposta corretta, ma si tratta di un'implementazione molto inefficiente. Questo metodo enumera la sequenza due volte: una volta per produrre la media e una volta per produrre la media del quadrato della differenza della media.
Si noti che le query LINQ vengono valutate in modo differito, quindi il calcolo delle differenze rispetto al valore medio e la media tra tali differenze genera un'unica enumerazione.

Esiste una formula alternativa che calcola la deviazione standard usando solo un'enumerazione della sequenza.  Questo calcolo produce due valori durante l'enumerazione della sequenza: la somma di tutti gli elementi nella sequenza e la somma di ogni valore quadrato:

[!code-csharp[Formula della somma dei quadrati](../../samples/snippets/csharp/tuples/tuples/statistics.cs#06_SumOfSquaresFormula "Calcolare la deviazione standard tramite la somma dei quadrati")]

Questa versione enumera la sequenza esattamente una volta. Tuttavia, non si tratta di codice particolarmente riutilizzabile. Continuando a lavorare, si scoprirà che numerosi calcoli statistici usano il numero di elementi nella sequenza, la somma della sequenza e la somma dei quadrati della sequenza. Eseguiamo il refactoring di questo metodo e scriviamo un metodo di utilità che produce tutti e tre questi valori.

A questo punto le tuple diventano molto utili. 

Aggiorniamo questo metodo in modo tale che i tre valori calcolati durante l'enumerazione vengano archiviati in una tupla. Questa operazione consente di creare questa versione:

[!code-csharp[Versione della tupla](../../samples/snippets/csharp/tuples/tuples/statistics.cs#07_TupleVersion "Eseguire il refactoring per usare le tuple")]

Il supporto del refactoring di Visual Studio semplifica l'estrazione delle funzionalità per le statistiche principali in un metodo privato. Ciò offre un metodo `private static` che restituisce il tipo di tupla con tre valori di `Sum`, `SumOfSquares`, e `Count`:

[!code-csharp[Versione del metodo della tupla](../../samples/snippets/csharp/tuples/tuples/statistics.cs#08_TupleMethodVersion "Dopo l'estrazione del metodo di utilità")]
 
Il linguaggio fornisce due opzioni aggiuntive che è possibile usare se si desidera apportare manualmente rapide modifiche. In primo luogo, è possibile usare la dichiarazione `var` per inizializzare il risultato della tupla dalla chiamata al metodo `ComputeSumAndSumOfSquares`. È anche possibile creare tre variabili discrete all'interno del metodo `ComputeSumAndSumOfSquares`. Di seguito è riportata la versione finale:

[!code-csharp[Versione pulita della tupla](../../samples/snippets/csharp/tuples/tuples/statistics.cs#09_CleanedTupleVersion "Dopo la pulizia finale")]

Questa versione finale può essere usata per qualsiasi metodo che necessiti di questi tre valori o di sottoinsiemi di essi.

Il linguaggio supporta altre opzioni per la gestione dei nomi dei campi in questi metodi che restituiscono tuple.

È possibile rimuovere i nomi dei campi dalla dichiarazione di valore restituito e restituire una tupla senza nome:

```csharp
private static (double, double, int) ComputeSumAndSumOfSquares(IEnumerable<double> sequence)
{
    double sum = 0;
    double sumOfSquares = 0;
    int count = 0;

    foreach (var item in sequence)
    {
        count++;
        sum += item;
        sumOfSquares += item * item;
    }

    return (sum, sumOfSquares, count);
}
```

È necessario risolvere i campi di questa tupla come `Item1`, `Item2`, e `Item3`.
Si consiglia di fornire nomi semantici per i campi delle tuple restituite dai metodi.

Un altro ambito in cui le tuple possono rivelarsi molto utili è la creazione di query LINQ in cui il risultato finale è una proiezione che contiene alcune, ma non tutte, le proprietà degli oggetti selezionati.

In genere, i risultati della query vengono proiettati in una sequenza di oggetti del tipo anonimo. Ciò presenta numerose limitazioni, principalmente perché i tipi anonimi non possono essere facilmente denominati nel tipo restituito per un metodo. In alternativa, usare `object` o `dynamic` come tipo del risultato offre costi significativi in termini di prestazioni.

La restituzione di una sequenza di un tipo di tupla è semplice e i nomi e i tipi dei campi sono disponibili in fase di compilazione e tramite gli strumenti IDE.
Si consideri, ad esempio, un'applicazione ToDo. È possibile definire una classe simile alla seguente per rappresentare una singola voce nell'elenco ToDo:

[!code-csharp[Voce ToDo](../../samples/snippets/csharp/tuples/tuples/projectionsample.cs#14_ToDoItem "Voce ToDo")]

Le applicazioni per dispositivi mobili possono supportare un modulo compresso delle voci ToDo correnti che visualizza solo il titolo. Questa query LINQ genera una proiezione che include solo l'ID e il titolo. Un metodo che restituisce una sequenza di tuple esprime in maniera accurata questa struttura:

[!code-csharp[Query che restituisce una tupla](../../samples/snippets/csharp/tuples/tuples/projectionsample.cs#15_QueryReturningTuple "Query che restituisce una tupla")]

La tupla con nome può essere parte della firma. Consente al compilatore e agli strumenti IDE di garantire in modo statico che si sta usando correttamente il risultato. La tupla con nome contiene anche le informazioni sul tipo statico in modo da eliminare la necessità di usare le costose funzionalità di runtime quali la reflection o l'associazione dinamica al fine di lavorare con i risultati.

## <a name="deconstruction"></a>Decostruzione

È possibile decomprimere tutte le voci in una tupla *decostruendo* la tupla restituita da un metodo. Per la decostruzione delle tuple esistono due diversi approcci.  Il primo consente di dichiarare in modo esplicito il tipo di ogni campo all'interno di parentesi per creare variabili discrete per ognuno dei campi nella tupla:

[!code-csharp[Decostruzione](../../samples/snippets/csharp/tuples/tuples/statistics.cs#10_Deconstruct "Decostruzione")]

È anche possibile dichiarare variabili tipizzate in modo implicito per ogni campo in una tupla usando la parola chiave `var` all'esterno delle parentesi:

[!code-csharp[Decostruzione con Var](../../samples/snippets/csharp/tuples/tuples/statistics.cs#11_DeconstructToVar "Decostruzione con Var")]

In aggiunta, è possibile usare la parola chiave `var` con una o tutte le dichiarazioni di variabili all'interno delle parentesi. 

```csharp
(double sum, var sumOfSquares, var count) = ComputeSumAndSumOfSquares(sequence);
```
Si noti che non è possibile usare un tipo specifico all'esterno delle parentesi, anche se ogni campo nella tupla presenta lo stesso tipo.

### <a name="deconstructing-user-defined-types"></a>Decostruzione dei tipi definiti dall'utente

Qualsiasi tipo di tupla può essere decostruito come illustrato in precedenza. È semplice anche abilitare la decostruzione sui tipi definiti dall'utente (classi, struct o perfino interfacce).

L'autore del tipo può definire uno o più metodi `Deconstruct` che assegnano valori a qualsiasi numero di variabili `out` che rappresentano gli elementi di dati di cui il tipo è composto. Ad esempio, il tipo `Person` seguente definisce un metodo `Deconstruct` che decostruisce un oggetto person in campi che rappresentano il nome e il cognome:

[!code-csharp[Tipo con metodo di decostruzione](../../samples/snippets/csharp/tuples/tuples/person.cs#12_TypeWithDeconstructMethod "Tipo con metodo di decostruzione")]

Il metodo di decostruzione consente l'assegnazione da un `Person` a due stringhe, che rappresentano le proprietà `FirstName` e `LastName`:

[!code-csharp[Tipo di decostruzione](../../samples/snippets/csharp/tuples/tuples/program.cs#12A_DeconstructType "Decostruire un tipo classe")]

È possibile abilitare la decostruzione anche per i tipi non creati dall'utente.
Il metodo `Deconstruct` può essere un metodo di estensione che decomprime i membri di dati accessibili di un oggetto. Nell'esempio seguente viene illustrato un tipo `Student`, derivato dal tipo `Person` e un metodo di estensione che decostruisce un `Student` in tre variabili, che rappresentano `FirstName`, `LastName` e `GPA`:

[!code-csharp[Tipo con metodo di estensione deconstruct](../../samples/snippets/csharp/tuples/tuples/person.cs#13_ExtensionDeconstructMethod "Tipo con metodo di estensione deconstruct")]

Un oggetto `Student` dispone ora di due metodi `Deconstruct` di accesso: il metodo di estensione dichiarato per i tipi `Student` e i membri del tipo `Person`. Entrambi appartengono all'ambito, consentendo la decostruzione di un `Student` in due o tre variabili.
Se si assegna uno studente a tre variabili, vengono restituiti nome, cognome e GPA. Se si assegna uno studente a due variabili, vengono restituiti solo nome e cognome.

[!code-csharp[Decostruire con il metodo di estensione](../../samples/snippets/csharp/tuples/tuples/program.cs#13A_DeconstructExtension "Decostruire un tipo classe tramite un metodo di estensione")]

È necessario prestare particolare attenzione alla definizione di più metodi `Deconstruct` in una classe o in una gerarchia di classi. Più metodi `Deconstruct` che presentano lo stesso numero di parametri `out` possono rapidamente causare ambiguità. I chiamanti potrebbero non essere in grado di eseguire facilmente chiamate al metodo `Deconstruct` desiderato.

In questo esempio, vi è una minima possibilità di chiamata ambigua perché il metodo `Deconstruct` per `Person` ha due parametri di output e il metodo `Deconstruct` per `Student` ne ha tre.

## <a name="conclusion"></a>Conclusione 

Il nuovo supporto per linguaggio e libreria per le tuple con nome rende più semplice lavorare con schemi che usano strutture di dati che archiviano più campi, ma non definiscono il comportamento, come le classi e gli struct. Usare le tuple per questi tipi è semplice e veloce. Si ottengono tutti i vantaggi del controllo del tipo statico, senza la necessità di creare tipi tramite la sintassi più dettagliata `class` o `struct`. Anche in questo caso, risultano particolarmente utili per i metodi di utilità `private` o `internal`. Creare tipi definiti dall'utente, tipi `class` o `struct` quando i metodi pubblici restituiscono un valore che contiene più campi.

