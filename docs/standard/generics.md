---
title: Panoramica di tipi generici (generics)
description: Panoramica di tipi generici (generics)
keywords: .NET, .NET Core
author: kuhlenh
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: a315b111-8e48-446c-ab19-acb6405894a7
translationtype: Human Translation
ms.sourcegitcommit: 5b1a76c011b95db3ff5c4b4e01556f79c45fb369
ms.openlocfilehash: 5dcb9d10aeded8c5e8956c4b99ba9675311a787a

---

# <a name="generic-types-generics-overview"></a>Panoramica di tipi generici (generics)

I generics vengono usati sempre in C#, implicitamente o esplicitamente. Durante l'uso di LINQ in C#, si è mai notato che si stava usando IEnumerable<T>? Oppure, visualizzando un esempio online di un "repository generico" che comunica con database tramite Entity Framework, si è notato che la maggior parte dei metodi restituiscono IQueryable<T>? Molti utenti e sviluppatori si chiedono che cosa rappresenta la **T** in questi esempi e perché è presente?

Introdotto per la prima volta in .NET Framework 2.0, i generics comportavano modifiche al linguaggio C# e a Common Language Runtime (CLR). I **generics** sono essenzialmente un "modello di codice" che consente agli sviluppatori di definire strutture di dati [indipendenti dai tipi](https://msdn.microsoft.com/library/hbzz1a9a.aspx) senza il commit di un tipo di dati effettivo. Ad esempio, `List<T>` è una [raccolta generica](https://msdn.microsoft.com/library/System.Collections.Generic.aspx) che può essere dichiarata e usata con qualsiasi tipo: `List<int>`, `List<string>`, `List<Person>`, e così via.

Quindi? Perché i generics sono utili? Per capire meglio questo meccanismo, è necessario esaminare una classe specifica prima e dopo l'aggiunta dei generics. Viene esaminata la classe `ArrayList`. In C# 1.0, gli elementi `ArrayList` erano di tipo `object`. Ciò vuol dire che qualsiasi elemento aggiunto veniva convertito automaticamente nel tipo `object`; la stessa cosa accade durante la lettura degli elementi dall'elenco (questo processo è noto come [conversione boxing](https://msdn.microsoft.com/library/yz2be5wk.aspx) e unboxing rispettivamente). Le conversioni boxing e unboxing influiscono sulle prestazioni. Non è possibile tuttavia individuare in fase di compilazione il tipo effettivo dei dati nell'elenco. E ciò crea un codice fragile. I generics risolvono il problema, offrendo informazioni aggiuntive sul tipo di dati contenuti in ogni istanza dell'elenco. In parole semplici, è possibile aggiungere solo numeri interi al tipo `List<int>` e persone al tipo `List<Person>`, e così via.

I generics sono anche disponibili in fase di esecuzione o **reified**. Ciò significa che il runtime sa quale tipo di struttura dei dati si sta usando e può eseguire un'archiviazione in memoria in modo più efficiente.

Questo è un breve programma che illustra l'efficienza di conoscere il tipo di struttura dei dati in fase di esecuzione:

```cs
  using System;
  using System.Collections;
  using System.Collections.Generic;
  using System.Diagnostics;

  namespace GenericsExample {
    class Program {
      static void Main(string[] args) {
        //generic list
        List<int> ListGeneric = new List<int> { 5, 9, 1, 4 };
        //non-generic list
        ArrayList ListNonGeneric = new ArrayList { 5, 9, 1, 4 };
        // timer for generic list sort
        Stopwatch s = Stopwatch.StartNew();
        ListGeneric.Sort();
        s.Stop();
        Console.WriteLine($"Generic Sort: {ListGeneric}  \n Time taken: {s.Elapsed.TotalMilliseconds}ms");

        //timer for non-generic list sort
        Stopwatch s2 = Stopwatch.StartNew();
        ListNonGeneric.Sort();
        s2.Stop();
        Console.WriteLine($"Non-Generic Sort: {ListNonGeneric}  \n Time taken: {s2.Elapsed.TotalMilliseconds}ms");
        Console.ReadLine();
      }
    }
  }

```

Il programma produce l'output seguente:

```console
Generic Sort: System.Collections.Generic.List\`1[System.Int32] Time taken: 0.0789ms
Non-Generic Sort: System.Collections.ArrayList Time taken: 2.4324ms

```

La prima cosa che si può notare è che l'ordinamento dell'elenco generico è notevolmente più veloce dell'elenco non generico. È anche possibile notare che il tipo per un elenco generico è specifico ([System. Int32]), mentre il tipo per un elenco non generico è generalizzato. Poiché il runtime riconosce che il tipo generico `List<int>` è di tipo int, può archiviare gli elementi dell'elenco in una matrice sottostante di integer in memoria, mentre il tipo `ArrayList` non generico deve eseguire il cast di ogni elemento dell'elenco come oggetto archiviato in una matrice di oggetti in memoria. Come illustrato in questo esempio, i cast aggiuntivi richiedono tempo e rallentano l'ordinamento dell'elenco.

Se il runtime riconosce il tipo generico, offre una migliore esperienza di debug. Quando si esegue il debug di un tipo generico in C#, si può sapere di quale tipo è ogni elemento nella struttura dei dati. Senza i generics, questo non sarebbe possibile.

## <a name="further-reading-and-resources"></a>Altre informazioni e risorse

*   [Introduzione ai generics per C#](https://msdn.microsoft.com/library/ms379564.aspx)
*   [Generics (Guida per programmatori C#)](https://msdn.microsoft.com/library/512aeb7t.aspx)



<!--HONumber=Nov16_HO1-->


