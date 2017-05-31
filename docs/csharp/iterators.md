---
title: Iteratori
description: Iteratori
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 5cf36f45-f91a-4fca-a0b7-87f233e108e9
ms.translationtype: Human Translation
ms.sourcegitcommit: 890c058bd09893c2adb185e1d8107246eef2e20a
ms.openlocfilehash: 7fea22be3b98c3218d173e5d80f1f22ef7ecf7e2
ms.contentlocale: it-it
ms.lasthandoff: 04/12/2017

---

# <a name="iterators"></a>Iteratori

Quasi tutti i programmi che vengono scritti avranno la necessità di eseguire un'iterazione in una raccolta. Si scriverà il codice che esamina ogni elemento in una raccolta. 

Si creeranno anche metodi iteratori, cioè metodi che producono un iteratore per gli elementi di quella classe. Essi possono essere usati per le azioni seguenti:

+ Esecuzione di un'azione su ogni elemento in una raccolta.
+ Enumerazione di una raccolta personalizzata.
+ Estensione in [LINQ](linq/index.md) o in altre librerie.
+ Creazione di una pipeline di dati dove i dati fluiscono in modo efficace tramite i metodi iteratori.

Il linguaggio C# offre funzionalità per entrambi gli scenari. In questo articolo viene offerta una panoramica di tali funzionalità.

Questa esercitazione prevede diversi passaggi. Dopo ogni passaggio, è possibile eseguire l'applicazione e verificare lo stato di avanzamento. È anche possibile [visualizzare o scaricare l'esempio completato](https://github.com/dotnet/docs/blob/master/samples/csharp/iterators) per questo argomento. Per istruzioni sul download, vedere [Esempi ed esercitazioni](../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="iterating-with-foreach"></a>Iterazione con foreach

L'enumerazione di una raccolta è semplice: la parola chiave `foreach` enumera una raccolta eseguendo l'istruzione incorporata una volta per ogni elemento nella raccolta:
 
```csharp
foreach (var item in collection)
{
   Console.WriteLine(item.ToString());
}
```

Questo è tutto. Per eseguire l'iterazione in tutto il contenuto di una raccolta, è sufficiente l'istruzione `foreach`. L'istruzione `foreach` non è tuttavia magica. Si basa su due interfacce generiche definite nella libreria di base di .NET per generare il codice necessario per eseguire l'iterazione di una raccolta: `IEnumerable<T>` e `IEnumerator<T>`. Questo meccanismo è illustrato più dettagliatamente nel seguito di questo articolo.

Queste due interfacce dispongono anche di controparti non generiche: `IEnumerable` e `IEnumerator`. Le versioni [generic](programming-guide/generics/index.md) sono preferite per il codice moderno.

## <a name="enumeration-sources-with-iterator-methods"></a>Origini di enumerazione con metodi iteratori

Un'altra eccezionale funzionalità del linguaggio C# consente di creare metodi che creano un'origine per un'enumerazione. Essi sono denominati *metodi iteratori*. Un metodo iteratore definisce come generare gli oggetti in una sequenza quando richiesto. Usare le parole chiave contestuali `yield return` per definire un metodo iteratore. 

È possibile scrivere questo metodo per produrre la sequenza di numeri interi da 0 a 9:

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    yield return 0;
    yield return 1;
    yield return 2;
    yield return 3;
    yield return 4;
    yield return 5;
    yield return 6;
    yield return 7;
    yield return 8;
    yield return 9;
}
```

Il codice sopra riportato indica istruzioni `yield return` distinte per evidenziare che è possibile usare più istruzioni `yield return` discrete in un metodo iteratore.
È possibile (come capita spesso) usare altri costrutti di linguaggio per semplificare il codice di un metodo iteratore. La definizione di metodo seguente produce la stessa identica sequenza di numeri:

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;
}
```

Non è necessario scegliere l'uno o l'altro. È possibile specificare qualsiasi numero di istruzioni `yield return` necessarie per soddisfare le esigenze del metodo:

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;
        
    yield return 50;
    
    index = 100;
    while (index++ < 110)
        yield return index;
}
```

Questa è la sintassi di base. Si consideri un esempio reale in cui si vuole scrivere un metodo iteratore. Si supponga di lavorare su un progetto IoT e che i sensori dispositivo generino un flusso di dati molto grande. Per ottenere un'idea dei dati, è possibile scrivere un metodo che campioni ogni elemento dati n. Questo piccolo metodo iteratore serve allo scopo:

```csharp
public static IEnumerable<T> Sample(this IEnumerable<T> sourceSequence, int interval)
{
    int index = 0;
    foreach (T item in sourceSequence)
    {
        if (index++ % interval == 0)
            yield return item;
    }
}
```

I metodi iteratori presentano un'importante restrizione: non è possibile avere sia un'istruzione `return` che un'istruzione `yield return` nello stesso metodo. Il codice seguente non verrà compilato:

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;
        
    yield return 50;
   
    // generates a compile time error: 
    var items = new int[] {100, 101, 102, 103, 104, 105, 106, 107, 108, 109 };
    return items;  
}
```

Questa restrizione non costituisce in genere un problema. È possibile scegliere di usare `yield return` in tutto il metodo o di separare il metodo originale in più metodi, alcuni con l'uso di `return` e altri con l'uso di `yield return`.

È possibile modificare leggermente l'ultimo metodo in modo da usare `yield return` ovunque:

```csharp
public IEnumerable<int> GetSingleDigitNumbers()
{
    int index = 0;
    while (index++ < 10)
        yield return index;
        
    yield return 50;
   
    var items = new int[] {100, 101, 102, 103, 104, 105, 106, 107, 108, 109 };
    foreach (var item in items)
        yield return item;
}
```
 
In alcuni casi, la risposta giusta è la suddivisione di un metodo iteratore in due metodi diversi: uno che usa `return` e un altro che usa `yield return`. Si consideri una situazione in cui si vuole restituire una raccolta vuota o i primi 5 numeri dispari, in base a un argomento booleano. Ciò può essere scritto con i due metodi seguenti:

```csharp
public IEnumerable<int> GetSingleDigitOddNumbers(bool getCollection)
{
    if (getCollection == false)
        return new int[0];
    else
        return IteratorMethod();
}

private IEnumerable<int> IteratorMethod()
{
    int index = 0;
    while (index++ < 10)
        if (index % 2 == 1)
            yield return index;
}
```
 
Esaminare i metodi descritti precedentemente. Il primo usa l'istruzione `return` standard per restituire una raccolta vuota o l'iteratore creato dal secondo metodo. Il secondo metodo usa l'istruzione `yield return` per creare la sequenza richiesta.

## <a name="deeper-dive-into-foreach"></a>Approfondimento di `foreach`

L'istruzione `foreach` si espande in un termine standard che usa le interfacce `IEnumable<T>` e `IEnumerator<T>` per eseguire l'iterazione tra tutti gli elementi di una raccolta. Riduce al minimo gli errori commessi dagli sviluppatori a causa di una gestione non corretta delle risorse. 

Il compilatore traduce il ciclo `foreach` illustrato nel primo esempio in un risultato simile a questo costrutto:

```csharp
IEnumerator<int> enumerator = collection.GetEnumerator();
while (enumerator.MoveNext())
{
    var item = enumerator.Current;
    Console.WriteLine(item.ToString());
}
```

Il costrutto sopra rappresenta il codice generato dal compilatore C# a partire dalla versione 5 e successive. Prima della versione 5, la variabile `item` aveva un ambito diverso:

```csharp
// C# versions 1 through 4:
IEnumerator<int> enumerator = collection.GetEnumerator();
int item = default(int);
while (enumerator.MoveNext())
{
    item = enumerator.Current;
    Console.WriteLine(item.ToString());
}
```

La modifica è stata apportata perché il comportamento precedente avrebbe potuto causare bug gravi e difficili da diagnosticare relativi alle espressioni lambda. Per altre informazioni, vedere la sezione relativa alle [espressioni lambda](lambda-expressions.md). 

Il codice esatto generato dal compilatore è leggermente più complesso e gestisce situazioni in cui l'oggetto restituito da `GetEnumerator()` implementa l'interfaccia `IDisposable`. L'espansione completa genera codice più simile al seguente:

```csharp
{
    var enumerator = collection.GetEnumerator();
    try 
    {
        while (enumerator.MoveNext())
        {
            var item = enumerator.Current;
            Console.WriteLine(item.ToString());
        }
    } finally 
    {
        // dispose of enumerator.
    }
}
```

Il modo in cui l'enumeratore viene eliminato dipende dalle caratteristiche del tipo di `enumerator`. Nel caso generale, la clausola `finally` si espande a:

```csharp
finally 
{
   (enumerator as IDisposable)?.Dispose();
} 
```

Tuttavia, se il tipo di `enumerator` è un tipo sealed e non esiste alcuna conversione implicita dal tipo di `enumerator` a `IDisposable`, la clausola `finally` si espande in un blocco vuoto:
```csharp
finally 
{
} 
```

Se esiste una conversione implicita dal tipo di `enumerator` a `IDisposable` e `enumerator` è un tipo di valore non nullable, la `finally` si clausola espande a:

```csharp
finally 
{
   ((IDisposable)enumerator).Dispose();
} 
```

Fortunatamente, non è necessario ricordare tutti questi dettagli. L'istruzione `foreach` gestisce tutte queste sfumature. Il compilatore genererà il codice corretto per tutti questi costrutti. 



