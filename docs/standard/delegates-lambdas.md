---
title: Delegati e lambda
description: Delegati e lambda
keywords: .NET, .NET Core
author: richlander
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: fe2e4b4c-6483-4106-a4b4-a33e2e306591
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 1dbe9c72999c14e45910310eb0bbc91ebe9f1e4a
ms.lasthandoff: 03/02/2017

---

# <a name="delegates-and-lambdas"></a>Delegati e lambda

I delegati definiscono un tipo che specifica una firma di metodo specifica. Un metodo (statico o istanza) che soddisfa questa firma può essere assegnato a una variabile del tipo, quindi chiamato direttamente (con gli argomenti appropriati) o passato come argomento a un altro metodo e quindi chiamato. L'esempio seguente mostra l'uso dei delegati.

```cs
public class Program
{

  public delegate string Reverse(string s);

  static string ReverseString(string s)
  {
      return new string(s.Reverse().ToArray());
  }

  static void Main(string[] args)
  {
      Reverse rev = ReverseString;

      Console.WriteLine(rev("a string"));
  }
}

```

*   Nella riga 4 viene creato un tipo delegato di una determinata firma, in questo caso un metodo che accetta un parametro di stringa e quindi restituisce un parametro di stringa.
*   Nella riga 6 viene definita l'implementazione del delegato specificando un metodo con la stessa firma.
*   Nella riga 13 il metodo viene assegnato a un tipo conforme al delegato `Reverse`.
*   Infine, nella riga 15 viene chiamato il delegato passando una stringa da invertire.

Per semplificare il processo di sviluppo, .NET include un set di tipi di delegato che i programmatori possono riutilizzare senza dover creare nuovi tipi. I tipi sono `Func<>`, `Action<>` e `Predicate<>` e possono essere usati in posizioni diverse all'interno delle API .NET senza dover definire nuovi tipi di delegato. Le differenze tra i tre tipi sono evidenti nelle firme e riguardano principalmente la modalità di utilizzo prevista:

*   `Action<>` viene usato quando è necessario eseguire un'azione usando gli argomenti del delegato.
*   `Func<>` viene in genere usato in presenza di una trasformazione, ovvero quando è necessario trasformare gli argomenti del delegato in un risultato diverso. Le proiezioni sono un esempio tipico.
*   `Predicate<>` viene usato quando è necessario determinare se l'argomento soddisfa la condizione del delegato. Può essere scritto anche come `Func<T, bool>`.

L'esempio precedente può essere ora riscritto usando il delegato `Func<>` anziché un tipo personalizzato. Il programma continuerà a essere eseguito nello stesso modo.

```cs
public class Program
{

  static string ReverseString(string s)
  {
      return new string(s.Reverse().ToArray());
  }

  static void Main(string[] args)
  {
      Func<string, string> rev = ReverseString;

      Console.WriteLine(rev("a string"));
  }
}

```

In questo esempio semplice, la presenza di un metodo definito all'esterno del metodo Main() non è necessaria. Per questa ragione è stato introdotto in .NET Framework 2.0 il concetto di **delegati anonimi**. I delegati anonimi consentono di creare delegati "incorporati" senza dover specificare tipi o metodi aggiuntivi. Sarà sufficiente incorporare la definizione del delegato dove necessario.

In questo esempio il delegato anonimo viene configurato e usato per visualizzare un elenco dei soli numeri pari che vengono quindi stampati nella console.

```cs
public class Program
{

  public static void Main(string[] args)
  {
    List<int> list = new List<int>();

    for (int i = 1; i <= 100; i++)
    {
        list.Add(i);
    }

    List<int> result = list.FindAll(
      delegate(int no)
      {
          return (no%2 == 0);
      }
    );

    foreach (var item in result)
    {
        Console.WriteLine(item);
    }
  }
}

```

Si notino le righe evidenziate. È possibile osservare che il corpo del delegato è costituito da un set di espressioni, come qualsiasi altro delegato. Ma anziché essere una definizione separata, il delegato è stato inserito _appositamente_ nella chiamata al metodo `FindAll()` del tipo `List<T>`.

Anche con questo approccio, tuttavia, rimane una parte considerevole di codice che è possibile eliminare. A tale scopo, vengono usate le **espressioni lambda**.

Le espressioni lambda, chiamate anche "lambda", sono state usate per la prima volta in C# 3.0 come uno dei componenti fondamentali di Language Integrated Query (LINQ). Si tratta semplicemente una sintassi più pratica per l'uso dei delegati. Dichiarano una firma e il corpo di un metodo senza avere una propria identità formale, a meno che non vengano assegnate a un delegato. A differenza dei delegati, possono essere assegnate direttamente come parte sinistra della registrazione eventi o in diverse clausole e metodi Linq.

Poiché un'espressione lambda è soltanto un modo diverso di specificare un delegato, è possibile riscrivere l'esempio precedente per usare un'espressione lambda anziché un delegato anonimo.

```cs
public class Program
{

  public static void Main(string[] args)
  {
    List<int> list = new List<int>();

    for (int i = 1; i <= 100; i++)
    {
        list.Add(i);
    }

    List<int> result = list.FindAll(i => i % 2 == 0);

    foreach (var item in result)
    {
        Console.WriteLine(item);
    }
  }
}

```

Nelle righe evidenziate è possibile osservare l'aspetto di un'espressione lambda. Anche in questo caso, si tratta soltanto di una sintassi **molto** pratica per l'uso di delegati con un funzionamento simile a quello del delegato anonimo.

Le lambda sono semplicemente delegati, ovvero possono essere usate come gestori di eventi come mostra il frammento di codice seguente.

```cs
public MainWindow()
{
    InitializeComponent();

    Loaded += (o, e) =>
    {
        this.Title = "Loaded";
    };
}

```

## <a name="further-reading-and-resources"></a>Altre informazioni e risorse

*   [Delegati](https://msdn.microsoft.com/library/ms173171.aspx)
*   [Funzioni anonime](https://msdn.microsoft.com/library/bb882516.aspx)
*   [Espressioni lambda](https://msdn.microsoft.com/library/bb397687.aspx)

