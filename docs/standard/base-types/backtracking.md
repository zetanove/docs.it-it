---
title: Backtracking nelle espressioni regolari
description: Backtracking nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8a3e6298-26b7-4c99-bd97-c9892f6c9418
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 649dfd6752f0589eb396b00e7d0b5184bb65d488

---

# <a name="backtracking-in-regular-expressions"></a>Backtracking nelle espressioni regolari

Il backtracking si verifica quando un modello di espressione regolare contiene [quantificatori](quantifiers.md) o [costrutti di alternanza](alternation.md) facoltativi e il motore delle espressioni regolari torna a uno stato salvato in precedenza per continuare la ricerca di una corrispondenza. Il backtracking è fondamentale per la potenza delle espressioni regolari. Consente alle espressioni di essere potenti e flessibili e di cercare una corrispondenza di modelli molto complessi. Questa tecnica presenta tuttavia anche alcuni svantaggi. Il backtracking spesso è il fattore più importante che influisce sulle prestazioni del motore delle espressioni regolari. Fortunatamente, lo sviluppatore è in grado di controllare il comportamento del motore delle espressioni regolari e il modo in cui viene utilizzato il backtracking. In questo argomento viene illustrato il funzionamento del backtracking e il modo in cui può essere controllato.

> [!NOTE]
> In generale, un motore NFA (Nondeterministic Finite Automaton) come il motore delle espressioni regolari affida la responsabilità della creazione di espressioni regolari efficienti e veloci allo sviluppatore.
 
Di seguito sono elencate le diverse sezioni di questo argomento:

* [Confronto lineare senza backtracking](#linear-comparison-without-backtracking)

* [Backtracking con quantificatori facoltativi o costrutti di alternanza](#backtracking-with-optional-quantifiers-or-alternation-constructs)

* [Backtracking con quantificatori facoltativi annidati](#backtracking-with-nested-optional-quantifiers)

* [Controllo del backtracking](#controlling-backtracking)

## <a name="linear-comparison-without-backtracking"></a>Confronto lineare senza backtracking

Se un modello di espressione regolare non contiene quantificatori facoltativi o costrutti di alternanza, il motore delle espressioni regolari viene eseguito in un tempo lineare, ovvero dopo che il motore delle espressioni regolari trova una corrispondenza tra il primo elemento del linguaggio del modello e il testo della stringa di input, prova a trovare una corrispondenza tra l'elemento del linguaggio successivo del modello e il carattere o il gruppo di caratteri successivi della stringa di input. Il processo continua finché la ricerca della corrispondenza non avrà esito positivo o negativo. In entrambi i casi, il motore delle espressioni regolari avanza di un carattere alla volta nella stringa di input.

Nell'esempio seguente viene illustrato questo concetto. L'espressione regolare `e{2}\w\b` cerca due occorrenze della lettera "e", seguite da qualsiasi carattere alfanumerico, seguito da un confine di parola.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "needing a reed";
      string pattern = @"e{2}\w\b";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("{0} found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       eed found at position 11
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "needing a reed"
      Dim pattern As String = "e{2}\w\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("{0} found at position {1}", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       eed found at position 11
```

Benché questa espressione regolare includa il quantificatore `{2}`, viene valutata in modo lineare. Il motore delle espressioni regolari non esegue il backtracking perché `{2}` non è un quantificatore facoltativo, ma specifica un numero esatto e non un numero variabile di volte in cui trovare la corrispondenza della sottoespressione precedente. Di conseguenza, il motore delle espressioni regolari tenta di trovare una corrispondenza tra il modello di espressione regolare e la stringa di input come illustrato nella tabella seguente.

Operazione | Posizione nel modello | Posizione nella stringa | Risultato
--------- | ------------------- | ------------------ | ------ 
1 | h | "needing a reed" (indice 0) | Nessuna corrispondenza. 
2 | h | "eeding a reed" (indice 1) | Possibile corrispondenza. 
3 | e{2} | "eding a reed" (indice 2) | Possibile corrispondenza. 
4 | \w | "ding a reed" (indice 3) | Possibile corrispondenza.
5 | \b | "ing a reed" (indice 4) | Possibile corrispondenza non riuscita. 
6 | h | "eding a reed" (indice 2) | Possibile corrispondenza. 
7 | e{2} | "ding a reed" (indice 3) | Possibile corrispondenza non riuscita. 
8 | h | "ding a reed" (indice 3) | La corrispondenza ha esito negativo. 
9 | h | "ing a reed" (indice 4) | Nessuna corrispondenza.
10 | h | "ng a reed" (indice 5) | Nessuna corrispondenza.
11 | h | "g a reed" (indice 6) | Nessuna corrispondenza.
12 | h | " a reed" (indice 7) | Nessuna corrispondenza.
13 | h | "a reed" (indice 8) | Nessuna corrispondenza.
14 | h | "reed" (indice 9) | Nessuna corrispondenza.
15 | h | "reed" (indice 10) | Nessuna corrispondenza.
16 | h | "eed" (indice 11) | Possibile corrispondenza.
17 | e{2} | "ed" (indice 12) | Possibile corrispondenza.
18 | \w | "d" (indice 13) | Possibile corrispondenza.
19 | \b | "" (indice 14) | Corrispondenza.
 

Se un modello di espressione regolare non include quantificatori facoltativi o costrutti di alternanza, il numero massimo di confronti necessari per trovare una corrispondenza tra il modello di espressione regolare e la stringa di input equivale approssimativamente al numero di caratteri della stringa di input. In questo caso, l'espressione regolare utilizza 19 confronti per identificare le possibili corrispondenze nella stringa di 13 caratteri. In altre parole, il motore delle espressioni regolari viene eseguito in un tempo quasi lineare se non contiene quantificatori facoltativi o costrutti di alternanza.

## <a name="backtracking-with-optional-quantifiers-or-alternation-constructs"></a>Backtracking con quantificatori facoltativi o costrutti di alternanza

Quando un'espressione regolare include quantificatori facoltativi o costrutti di alternanza, la valutazione della stringa di input non è più lineare. La corrispondenza dei modelli con un motore NFA è determinata dagli elementi del linguaggio nell'espressione regolare e non dai caratteri con cui trovare una corrispondenza nella stringa di input. Il motore delle espressioni regolari prova pertanto a trovare una piena corrispondenza con le sottoespressioni facoltative o alternative. Quando avanza all'elemento del linguaggio successivo nella sottoespressione e la corrispondenza ha esito negativo, il motore delle espressioni regolari può abbandonare una parte della corrispondenza esatta e tornare a uno stato salvato in precedenza al fine di trovare una corrispondenza tra l'intera espressione regolare e la stringa di input. Questo processo di tornare a uno stato salvato in precedenza per trovare una corrispondenza è noto come backtracking.

Si consideri, ad esempio, il modello di espressione regolare `.*(es)` che cerca una corrispondenza con i caratteri "es" e tutti i caratteri che li precedono. Come illustrato nell'esempio seguente, se la stringa di input è "Essential services are provided by regular expressions.", il modello cerca una corrispondenza con l'intera stringa fino ai caratteri "es" in "expressions" compresi.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "Essential services are provided by regular expressions.";
      string pattern = ".*(es)"; 
      Match m = Regex.Match(input, pattern, RegexOptions.IgnoreCase);
      if (m.Success) {
         Console.WriteLine("'{0}' found at position {1}", 
                           m.Value, m.Index);
         Console.WriteLine("'es' found at position {0}", 
                           m.Groups[1].Index);      
      } 
   }
}
//    'Essential services are provided by regular expres' found at position 0
//    'es' found at position 47
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "Essential services are provided by regular expressions."
      Dim pattern As String = ".*(es)" 
      Dim m As Match = Regex.Match(input, pattern, RegexOptions.IgnoreCase)
      If m.Success Then
         Console.WriteLine("'{0}' found at position {1}", _
                           m.Value, m.Index)
         Console.WriteLine("'es' found at position {0}", _
                           m.Groups(1).Index)                  
      End If     
   End Sub
End Module
'    'Essential services are provided by regular expres' found at position 0
'    'es' found at position 47
```

A tale scopo, il motore delle espressioni regolari utilizza il backtracking come segue:

* Trova la corrispondenza di `.*`, ovvero di zero, uno o più occorrenze di qualsiasi carattere, con l'intera stringa di input.

* Tenta di trovare una corrispondenza di "e" nel modello di espressione regolare. Tuttavia, nella stringa di input non sono presenti altri caratteri di cui cercare una corrispondenza.

* Esegue il backtracking fino all'ultima corrispondenza esatta, "Essential services are provided by regular expressions", e tenta di trovare una corrispondenza di "e" con il punto alla fine della frase. La corrispondenza ha esito negativo.

* Continua a eseguire il backtracking fino a una corrispondenza esatta precedente, un carattere alla volta, finché la sottostringa temporaneamente corrispondente non è "Essential services are provided by regular expr". Confronta quindi la "e" nel modello con la seconda "e" in "expressions" e trova una corrispondenza.

* Confronta la "s" nel modello con la "s" che segue il carattere "e" corrispondente (la prima "s" in "expressions"). La corrispondenza ha esito positivo.

Quando si utilizza il backtracking, la ricerca di una corrispondenza tra il modello di espressione regolare e la stringa di input, con una lunghezza pari a 55 caratteri, richiede 67 operazioni di confronto. È interessante notare che se nel modello di espressione regolare venisse incluso un quantificatore lazy `.*?(es),`, la ricerca di una corrispondenza dell'espressione regolare richiederebbe altri confronti. In questo caso, anziché eseguire il backtracking dalla fine della stringa fino alla "r" in "expressions", il motore delle espressioni regolari dovrà eseguire il backtracking fino all'inizio della stringa per trovare una corrispondenza di "Es" richiedendo 113 confronti. In genere, se un modello di espressione regolare include un singolo costrutto di alternanza o un singolo quantificatore facoltativo, il numero di operazioni di confronto necessarie per trovare una corrispondenza del modello è più del doppio rispetto al numero di caratteri della stringa di input.

## <a name="backtracking-with-nested-optional-quantifiers"></a>Backtracking con quantificatori facoltativi annidati

Il numero di operazioni di confronto necessarie per trovare una corrispondenza di un modello di espressione regolare può aumentare in modo esponenziale se il modello include un numero elevato di costrutti di alternanza, se include costrutti di alternanza annidati o se include sopratutto quantificatori facoltativi annidati. Il modello di espressione regolare `^(a+)+$`, ad esempio, è progettato per cercare una corrispondenza con una stringa completa contenente uno o più caratteri "a". Nell'esempio vengono fornite due stringhe di input di lunghezza identica, ma solo la prima stringa corrisponde al modello. La classe [System.Diagnostics.Stopwatch](xref:System.Diagnostics.Stopwatch) viene usata per determinare il tempo richiesto dall'operazione di corrispondenza. 

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "^(a+)+$";
      string[] inputs = { "aaaaaa", "aaaaa!" };
      Regex rgx = new Regex(pattern);
      Stopwatch sw;

      foreach (string input in inputs) {
         sw = Stopwatch.StartNew();   
         Match match = rgx.Match(input);
         sw.Stop();
         if (match.Success)
            Console.WriteLine("Matched {0} in {1}", match.Value, sw.Elapsed);
         else
            Console.WriteLine("No match found in {0}", sw.Elapsed);
      }
   }
}
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(a+)+$"
      Dim inputs() As String = { "aaaaaa", "aaaaa!" }
      Dim rgx As New Regex(pattern)
      Dim sw As Stopwatch

      For Each input As String In inputs
         sw = Stopwatch.StartNew()   
         Dim match As Match = rgx.Match(input)
         sw.Stop()
         If match.Success Then
            Console.WriteLine("Matched {0} in {1}", match.Value, sw.Elapsed)
         Else
            Console.WriteLine("No match found in {0}", sw.Elapsed)
         End If      
      Next
   End Sub
End Module
```

Come illustrato nell'output dell'esempio, il motore delle espressioni regolari ha impiegato il doppio del tempo per rilevare che una stringa di input non corrisponde al modello rispetto al tempo impiegato per identificare una stringa corrispondente. Ciò è dovuto al fatto che una corrispondenza negativa rappresenta sempre lo scenario peggiore. Il motore delle espressioni regolari deve utilizzare l'espressione regolare per seguire tutti i percorsi possibili nei dati prima di poter concludere che la corrispondenza è negativa e le parentesi annidate creano molti percorsi aggiuntivi nei dati. Il motore delle espressioni regolari conclude che la seconda stringa non corrisponde al modello effettuando le operazioni seguenti:

* Verifica di essere all'inizio della stringa, quindi cerca una corrispondenza tra i primi cinque caratteri della stringa con il modello a+. Determina quindi che non esistono altri gruppi di caratteri "a" nella stringa. Infine, verifica la fine della stringa. Poiché nella stringa rimane un ulteriore carattere, la corrispondenza ha esito negativo. La corrispondenza non riuscita richiede 9 confronti. Il motore delle espressioni regolari salva inoltre le informazioni di stato dalle relative corrispondenze di "a" (che chiameremo corrispondenza 1), "aa" (corrispondenza 2), "aaa" (corrispondenza 3) e "aaaa" (corrispondenza 4).

* Torna alla corrispondenza 4 salvata in precedenza. Determina che esiste un altro carattere "a" da assegnare a un gruppo acquisito aggiuntivo. Infine, verifica la fine della stringa. Poiché nella stringa rimane un ulteriore carattere, la corrispondenza ha esito negativo. La corrispondenza non riuscita richiede 4 confronti. Fino a questo momento sono stati eseguiti complessivamente 13 confronti.

* Torna alla corrispondenza 3 salvata in precedenza. Determina che esistono sono altri due caratteri "a" da assegnare a un gruppo acquisito aggiuntivo. Tuttavia, il test di fine della stringa ha esito negativo. Torna quindi alla corrispondenza 3 e tenta di trovare una corrispondenza degli altri due caratteri "a" nei due gruppi acquisiti aggiuntivi. Il test di fine della stringa ha ancora esito negativo. Le corrispondenza non riuscite richiedono 12 confronti. Fino a questo punto, sono stati eseguiti complessivamente 25 confronti. 

Il confronto della stringa di input con l'espressione regolare continua in questo modo fino a quando il motore delle espressioni regolari non ha tentato tutte le combinazioni di corrispondenze possibili, concludendo infine che non vi è alcuna corrispondenza. A causa dei quantificatori annidati, questo confronto è un'operazione O(2n) o un'operazione esponenziale, dove n è il numero di caratteri all'interno della stringa di input. Ciò significa che nei casi peggiori una stringa di input di 30 caratteri richiede circa 1.073.741.824 confronti e una stringa di input di 40 caratteri richiede circa 1.099.511.627.776 confronti. Se si utilizzano stringhe di queste lunghezze o di lunghezze ancora maggiore, i metodi delle espressioni regolari possono richiedere una quantità di tempo eccessiva per il completamento quando elaborano un input che non corrisponde al modello di espressione regolare.

## <a name="controlling-backtracking"></a>Controllo del backtracking

Il backtracking consente di creare espressioni regolari potenti e flessibili. Tuttavia, come illustrato nella sezione precedente, insieme a questi vantaggi si ottiene una notevole riduzione delle prestazioni. Per evitare un uso eccessivo del backtracking, è consigliabile definire un intervallo di timeout quando si crea un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) o si chiama un metodo di espressione regolare statica corrispondente. Questo è discusso nella sezione seguente. .NET Core supporta anche tre elementi del linguaggio delle espressioni regolari che limitano o evitano del tutto l'uso del backtracking e che supportano espressioni regolari complesse senza o con una minima riduzione delle prestazioni: [sottoespressioni non di backtracking](#nonbacktracking-subexpression), [asserzioni lookbehind](#lookbehind-assertions) e [asserzioni lookahead](#lookahead-assertions). Per altre informazioni su ogni elemento del linguaggio, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

### <a name="defining-a-timeout-interval"></a>Definizione di un intervallo di timeout

È possibile impostare un valore di timeout che rappresenta l'intervallo più lungo entro il quale il motore delle espressioni regolari cercherà una singola corrispondenza prima di rinunciare e generare un'eccezione [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException). Specificare l'intervallo di timeout specificando un valore [TimeSpan](xref:System.TimeSpan) al costruttore `Regex(String, RegexOptions, TimeSpan)` per creare un'istanza di espressioni regolari. Ogni metodo statico di ricerca della corrispondenza ha un overload con un valore [TimeSpan](xref:System.TimeSpan) per il parametro [Regex.Regex(String, RegexOptions, TimeSpan)], che consente di specificare un valore di timeout. Per impostazione predefinita l'intervallo di timeout viene impostato su [Regex.InfiniteMatchTimeout](xref:System.Text.RegularExpressions.Regex.InfiniteMatchTimeout), mentre il motore delle espressioni regolari non ha timeout. 

> [!IMPORTANT]
> È consigliabile impostare sempre un intervallo di timeout se l'espressione regolare si basa sul backtracking.
 
Un'eccezione [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException)n indica che il motore delle espressioni regolari non ha trovato una corrispondenza nell'intervallo di timeout specificato, ma non specifica il motivo per cui l'eccezione è stata generata. Il motivo può essere l'utilizzo eccessivo del backtracking, ma è anche possibile che l'intervallo di timeout sia stato impostato troppo basso dato il carico di sistema al momento in cui l'eccezione è stata generata. Quando si gestisce l'eccezione, è possibile scegliere di ignorare ulteriori corrispondenze con la stringa di input o aumentare l'intervallo di timeout e ritentare l'operazione corrispondente. 

Ad esempio, il codice seguente chiama il costruttore `Regex(String, RegexOptions, TimeSpan)` per creare un'istanza di un oggetto Regex con un valore di timeout di un secondo. Il modello di espressione regolare `(a+)+$`, che corrisponde a uno o più sequenze di uno o più caratteri "a" alla fine di una riga, è soggetto all'utilizzo eccessivo del backtracking. Se viene generata l'eccezione [RegexMatchTimeoutException](xref:System.Text.RegularExpressions.RegexMatchTimeoutException), l'esempio aumenta il valore di timeout fino a un intervallo massimo di tre secondi. Successivamente, ignora il tentativo di corrispondere al modello.

```csharp
using System;
using System.ComponentModel;
using System.Diagnostics;
using System.Security;
using System.Text.RegularExpressions;
using System.Threading; 

public class Example
{
   const int MaxTimeoutInSeconds = 3;

   public static void Main()
   {
      string pattern = @"(a+)+$";    // DO NOT REUSE THIS PATTERN.
      Regex rgx = new Regex(pattern, RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1));       
      Stopwatch sw = null;

      string[] inputs= { "aa", "aaaa>", 
                         "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
                         "aaaaaaaaaaaaaaaaaaaaaa>",
                         "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>" };

      foreach (var inputValue in inputs) {
         Console.WriteLine("Processing {0}", inputValue);
         bool timedOut = false;
         do { 
            try {
               sw = Stopwatch.StartNew();
               // Display the result.
               if (rgx.IsMatch(inputValue)) {
                  sw.Stop();
                  Console.WriteLine(@"Valid: '{0}' ({1:ss\.fffffff} seconds)", 
                                    inputValue, sw.Elapsed); 
               }
               else {
                  sw.Stop();
                  Console.WriteLine(@"'{0}' is not a valid string. ({1:ss\.fffff} seconds)", 
                                    inputValue, sw.Elapsed);
               }
            }
            catch (RegexMatchTimeoutException e) {   
               sw.Stop();
               // Display the elapsed time until the exception.
               Console.WriteLine(@"Timeout with '{0}' after {1:ss\.fffff}", 
                                 inputValue, sw.Elapsed);
               Thread.Sleep(1500);       // Pause for 1.5 seconds.

               // Increase the timeout interval and retry.
               TimeSpan timeout = e.MatchTimeout.Add(TimeSpan.FromSeconds(1));
               if (timeout.TotalSeconds > MaxTimeoutInSeconds) {
                  Console.WriteLine("Maximum timeout interval of {0} seconds exceeded.",
                                    MaxTimeoutInSeconds);
                  timedOut = false;
               }
               else {               
                  Console.WriteLine("Changing the timeout interval to {0}", 
                                    timeout); 
                  rgx = new Regex(pattern, RegexOptions.IgnoreCase, timeout);
                  timedOut = true;
               }
            }
         } while (timedOut);
         Console.WriteLine();
      }   
   }
}
// The example displays output like the following :
//    Processing aa
//    Valid: 'aa' (00.0000779 seconds)
//    
//    Processing aaaa>
//    'aaaa>' is not a valid string. (00.00005 seconds)
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
//    Valid: 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' (00.0000043 seconds)
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaa>
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 01.00469
//    Changing the timeout interval to 00:00:02
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 02.01202
//    Changing the timeout interval to 00:00:03
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 03.01043
//    Maximum timeout interval of 3 seconds exceeded.
//    
//    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>
//    Timeout with 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>' after 03.01018
//    Maximum timeout interval of 3 seconds exceeded.
```

```vb
Imports System.ComponentModel
Imports System.Diagnostics
Imports System.Security
Imports System.Text.RegularExpressions
Imports System.Threading 

Module Example
   Const MaxTimeoutInSeconds As Integer = 3

   Public Sub Main()
      Dim pattern As String = "(a+)+$"    ' DO NOT REUSE THIS PATTERN.
      Dim rgx As New Regex(pattern, RegexOptions.IgnoreCase, TimeSpan.FromSeconds(1))       
      Dim sw As Stopwatch = Nothing

      Dim inputs() As String = { "aa", "aaaa>", 
                                 "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
                                 "aaaaaaaaaaaaaaaaaaaaaa>",
                                 "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>" }

      For Each inputValue In inputs
         Console.WriteLine("Processing {0}", inputValue)
         Dim timedOut As Boolean = False
         Do 
            Try
               sw = Stopwatch.StartNew()
               ' Display the result.
               If rgx.IsMatch(inputValue) Then
                  sw.Stop()
                  Console.WriteLine("Valid: '{0}' ({1:ss\.fffffff} seconds)", 
                                    inputValue, sw.Elapsed) 
               Else
                  sw.Stop()
                  Console.WriteLine("'{0}' is not a valid string. ({1:ss\.fffff} seconds)", 
                                    inputValue, sw.Elapsed)
               End If
            Catch e As RegexMatchTimeoutException   
               sw.Stop()
               ' Display the elapsed time until the exception.
               Console.WriteLine("Timeout with '{0}' after {1:ss\.fffff}", 
                                 inputValue, sw.Elapsed)
               Thread.Sleep(1500)       ' Pause for 1.5 seconds.

               ' Increase the timeout interval and retry.
               Dim timeout As TimeSpan = e.MatchTimeout.Add(TimeSpan.FromSeconds(1))
               If timeout.TotalSeconds > MaxTimeoutInSeconds Then
                  Console.WriteLine("Maximum timeout interval of {0} seconds exceeded.",
                                    MaxTimeoutInSeconds)
                  timedOut = False
               Else                
                  Console.WriteLine("Changing the timeout interval to {0}", 
                                    timeout) 
                  rgx = New Regex(pattern, RegexOptions.IgnoreCase, timeout)
                  timedOut = True
               End If
            End Try
         Loop While timedOut
         Console.WriteLine()
      Next   
   End Sub 
End Module
' The example displays output like the following:
'    Processing aa
'    Valid: 'aa' (00.0000779 seconds)
'    
'    Processing aaaa>
'    'aaaa>' is not a valid string. (00.00005 seconds)
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
'    Valid: 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' (00.0000043 seconds)
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaa>
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 01.00469
'    Changing the timeout interval to 00:00:02
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 02.01202
'    Changing the timeout interval to 00:00:03
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaa>' after 03.01043
'    Maximum timeout interval of 3 seconds exceeded.
'    
'    Processing aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>
'    Timeout with 'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa>' after 03.01018
'    Maximum timeout interval of 3 seconds exceeded.
```

### <a name="nonbacktracking-subexpression"></a>Sottoespressione non di backtracking

L'elemento del linguaggio **(?>** _sottoespressione _**)** evita l'uso del backtracking in una sottoespressione. È utile per non incorrere nei problemi di prestazioni associati alle corrispondenze non riuscite. 

Nell'esempio seguente vengono illustrati i miglioramenti nelle prestazioni con i quantificatori annidati quando non si utilizza il backtracking. Viene calcolato il tempo impiegato dal motore delle espressioni regolari per determinare che una stringa di input non corrisponde a due espressioni regolari. La prima espressione regolare utilizza il backtracking per tentare di trovare una corrispondenza con una stringa contenente una o più occorrenze di una o più cifre esadecimali seguite da due punti, seguiti da una o più cifre esadecimali, seguite da un doppio due punti. La seconda espressione regolare è identica alla prima, con la differenza che il backtracking è disabilitato. Come illustrato nell'output dell'esempio, il miglioramento delle prestazioni derivante dalla disabilitazione del backtracking è significativo.

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "b51:4:1DB:9EE1:5:27d60:f44:D4:cd:E:5:0A5:4a:D24:41Ad:";
      bool matched;
      Stopwatch sw;

      Console.WriteLine("With backtracking:");
      string backPattern = "^(([0-9a-fA-F]{1,4}:)*([0-9a-fA-F]{1,4}))*(::)$";
      sw = Stopwatch.StartNew();
      matched = Regex.IsMatch(input, backPattern);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, backPattern), sw.Elapsed);
      Console.WriteLine();

      Console.WriteLine("Without backtracking:");
      string noBackPattern = "^((?>[0-9a-fA-F]{1,4}:)*(?>[0-9a-fA-F]{1,4}))*(::)$";
      sw = Stopwatch.StartNew();
      matched = Regex.IsMatch(input, noBackPattern);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, noBackPattern), sw.Elapsed);
   }
}
// The example displays output like the following:
//       With backtracking:
//       Match: False in 00:00:27.4282019
//       
//       Without backtracking:
//       Match: False in 00:00:00.0001391
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "b51:4:1DB:9EE1:5:27d60:f44:D4:cd:E:5:0A5:4a:D24:41Ad:"
      Dim matched As Boolean
      Dim sw As Stopwatch

      Console.WriteLine("With backtracking:")
      Dim backPattern As String = "^(([0-9a-fA-F]{1,4}:)*([0-9a-fA-F]{1,4}))*(::)$"
      sw = Stopwatch.StartNew()
      matched = Regex.IsMatch(input, backPattern)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, backPattern), sw.Elapsed)
      Console.WriteLine()

      Console.WriteLine("Without backtracking:")
      Dim noBackPattern As String = "^((?>[0-9a-fA-F]{1,4}:)*(?>[0-9a-fA-F]{1,4}))*(::)$"
      sw = Stopwatch.StartNew()
      matched = Regex.IsMatch(input, noBackPattern)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", Regex.IsMatch(input, noBackPattern), sw.Elapsed)
   End Sub
End Module
' The example displays the following output:
'       With backtracking:
'       Match: False in 00:00:27.4282019
'       
'       Without backtracking:
'       Match: False in 00:00:00.0001391
```

### <a name="lookbehind-assertions"></a>Asserzioni lookbehind

.NET include due elementi del linguaggio, **(?<**=_sottoespressione_**)**e **(?<!**_sottoespressione_**)**, che trovano il carattere o i caratteri precedenti nella stringa di input. Entrambi gli elementi di linguaggio sono asserzioni di larghezza zero, ovvero determinano se il carattere o i caratteri che precedono immediatamente il carattere corrente possono essere trovati da una *sottoespressione*, senza avanzamento o backtracking. 

**(?<**=_sottoespressione_**)** è un'asserzione lookbehind positiva, ovvero il carattere o i caratteri prima della posizione corrente devono corrispondere alla *sottoespressione*. **(?<!**_sottoespressione_**)** è un'asserzione lookbehind negativa, ovvero il carattere o i caratteri prima della posizione corrente non devono corrispondere alla *sottoespressione*. Le asserzioni lookbehind positive e negative sono entrambe particolarmente utili quando la *sottoespressione* è un sottoinsieme della *sottoespressione* precedente. 

Nell'esempio seguente vengono utilizzati due modelli di espressione regolare equivalenti per verificare il nome utente in un indirizzo di posta elettronica. Il primo modello è soggetto a una riduzione delle prestazioni a causa di un utilizzo eccessivo del backtracking. Il secondo modello modifica la prima espressione regolare sostituendo un quantificatore annidato con un'asserzione lookbehind positiva. Nell'output dell'esempio viene visualizzato il tempo di esecuzione del metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)).

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      Stopwatch sw;
      string input = "aaaaaaaaaaaaaaaaaaaa";
      bool result;

      string pattern = @"^[0-9A-Z]([-.\w]*[0-9A-Z])?@";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("Match: {0} in {1}", result, sw.Elapsed);

      string behindPattern = @"^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, behindPattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("Match with Lookbehind: {0} in {1}", result, sw.Elapsed);
   }
}
// The example displays output similar to the following:
//       Match: True in 00:00:00.0017549
//       Match with Lookbehind: True in 00:00:00.0000659
```

```vb
Module Example
   Public Sub Main()
      Dim sw As Stopwatch
      Dim input As String = "aaaaaaaaaaaaaaaaaaaa"
      Dim result As Boolean

      Dim pattern As String = "^[0-9A-Z]([-.\w]*[0-9A-Z])?@"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("Match: {0} in {1}", result, sw.Elapsed)

      Dim behindPattern As String = "^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, behindPattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("Match with Lookbehind: {0} in {1}", result, sw.Elapsed)
   End Sub
End Module
' The example displays output similar to the following:
'       Match: True in 00:00:00.0017549
'       Match with Lookbehind: True in 00:00:00.0000659
```

Il primo modello di espressione regolare, `^[0-9A-Z]([-.\w]*[0-9A-Z])*@, is defined as shown in the following table.`

Criterio | Descrizione
------- | ----------- 
`^` | Inizia la ricerca della corrispondenza all'inizio della stringa.
`[0-9A-Z]` | Trova la corrispondenza di un carattere alfanumerico. Poiché il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase), il confronto non rileva la distinzione tra maiuscole e minuscole.
`[-.\w]*` | Trova la corrispondenza di zero, una o più occorrenze di un trattino, un punto o un carattere alfanumerico. 
`[0-9A-Z]` | Trova la corrispondenza di un carattere alfanumerico. 
`([-.\w]*[0-9A-Z])*` | Trova la corrispondenza di zero o più occorrenze della combinazione di zero o più trattini, punti o caratteri alfanumerici seguiti da un carattere alfanumerico. Equivale al primo gruppo di acquisizione.
`@` | Trova la corrispondenza di una chiocciola ("@").
 
Il secondo criterio di espressione regolare, `^[0-9A-Z][-.\w]*(?<=[0-9A-Z])@`, usa un'asserzione lookbehind positiva e viene definito come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Inizia la ricerca della corrispondenza all'inizio della stringa.
`[0-9A-Z]` | Trova la corrispondenza di un carattere alfanumerico. Poiché il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase), il confronto non rileva la distinzione tra maiuscole e minuscole.
`[-.\w]*` | Trova la corrispondenza di zero o più occorrenze di un trattino, un punto o un carattere alfanumerico.
`(?<=[0-9A-Z])` | Esegue la ricerca dell'ultimo carattere corrispondente e continua la ricerca della corrispondenza se si tratta di un carattere alfanumerico. Si noti che i caratteri alfanumerici sono un subset del set costituito da punti, trattini e tutti i caratteri alfanumerici.
`@` | Trova la corrispondenza di una chiocciola ("@").
 
### <a name="lookahead-assertions"></a>Asserzioni lookahead

.NET include due elementi di linguaggio, **(?**=_sottoespressione_**)** e **(?!**_sottoespressione_**)**, che trovano il carattere o i caratteri successivi nella stringa di input. Entrambi gli elementi di linguaggio sono asserzioni di larghezza zero, ovvero determinano se il carattere o i caratteri che seguono immediatamente il carattere corrente possono essere trovati dalla *sottoespressione*, senza avanzamento o backtracking. 

**(?**=_sottoespressione_**)** è un'asserzione lookahead positiva, ovvero il carattere o i caratteri dopo la posizione corrente devono corrispondere alla *sottoespressione*. **(?!**_sottoespressione_**)** è un'asserzione lookahead negativa, ovvero il carattere o i caratteri dopo la posizione corrente non devono corrispondere alla *sottoespressione*. Le asserzioni lookahead positive e negative sono entrambe particolarmente utili quando la *sottoespressione* è un sottoinsieme della *sottoespressione* successiva. 

Nell'esempio seguente vengono utilizzati due modelli di espressione regolare equivalenti per verificare un nome di tipo completo. Il primo modello è soggetto a una riduzione delle prestazioni a causa di un utilizzo eccessivo del backtracking. Il secondo modello modifica la prima espressione regolare sostituendo un quantificatore annidato con un'asserzione lookahead positiva. Nell'output dell'esempio viene visualizzato il tempo di esecuzione del metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)).

```csharp
using System;
using System.Diagnostics;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aaaaaaaaaaaaaaaaaaaaaa.";
      bool result;
      Stopwatch sw;

      string pattern = @"^(([A-Z]\w*)+\.)*[A-Z]\w*$";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("{0} in {1}", result, sw.Elapsed);

      string aheadPattern = @"^((?=[A-Z])\w+\.)*[A-Z]\w*$";
      sw = Stopwatch.StartNew();
      result = Regex.IsMatch(input, aheadPattern, RegexOptions.IgnoreCase);
      sw.Stop();
      Console.WriteLine("{0} in {1}", result, sw.Elapsed);
   }
}
// The example displays the following output:
//       False in 00:00:03.8003793
//       False in 00:00:00.0000866
```

```vb
Imports System.Diagnostics
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aaaaaaaaaaaaaaaaaaaaaa."
      Dim result As Boolean
      Dim sw As Stopwatch

      Dim pattern As String = "^(([A-Z]\w*)+\.)*[A-Z]\w*$"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("{0} in {1}", result, sw.Elapsed)

      Dim aheadPattern As String = "^((?=[A-Z])\w+\.)*[A-Z]\w*$"
      sw = Stopwatch.StartNew()
      result = Regex.IsMatch(input, aheadPattern, RegexOptions.IgnoreCase)
      sw.Stop()
      Console.WriteLine("{0} in {1}", result, sw.Elapsed)
   End Sub
End Module
' The example displays the following output:
'       False in 00:00:03.8003793
'       False in 00:00:00.0000866
```

Il primo criterio di espressione regolare, `^(([A-Z]\w*)+\.)*[A-Z]\w*$`, è definito nel modo illustrato nella tabella seguente.

Modello | Descrizione
------- | ----------- 
`^` | Inizia la ricerca della corrispondenza all'inizio della stringa.
`([A-Z]\w*)+\.` | Trova la corrispondenza di un carattere alfabetico (A-Z) seguito da zero o più caratteri alfanumerici una o più volte seguiti da un punto. Poiché il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase), il confronto non rileva la distinzione tra maiuscole e minuscole.
`(([A-Z]\w*)+\.)*` | Trova la corrispondenza del modello precedente zero o più volte. 
`[A-Z]\w*` | Trova la corrispondenza di un carattere alfabetico seguito da zero o più caratteri alfanumerici.
`$` | Termina la ricerca della corrispondenza alla fine della stringa di input.
 

Il secondo criterio di espressione regolare, `^((?=[A-Z])\w+\.)*[A-Z]\w*$`, usa un'asserzione lookahead positiva e viene definito come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Inizia la ricerca della corrispondenza all'inizio della stringa.
`(?=[A-Z])` | Esegue la ricerca fino primo carattere e continua la ricerca della corrispondenza se si tratta di un carattere alfabetico (A-Z). Poiché il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase), il confronto non rileva la distinzione tra maiuscole e minuscole.
`\w+\.` | Trova la corrispondenza di uno o più caratteri alfanumerici seguiti da un punto.
`((?=[A-Z])\w+\.)*` | Trova la corrispondenza del modello di uno o più caratteri alfanumerici seguiti da un punto zero o più volte. Il carattere alfanumerico iniziale deve essere alfabetico. 
`[A-Z]\w*` | Trova la corrispondenza di un carattere alfabetico seguito da zero o più caratteri alfanumerici.
`$` | Termina la ricerca della corrispondenza alla fine della stringa di input.
 
## <a name="see-also"></a>Vedere anche

[Espressioni regolari .NET](regular-expressions.md)

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)

[Quantificatori nelle espressioni regolari](quantifiers.md)

[Costrutti di alternanza nelle espressioni regolari](alternation.md)

[Costrutti di raggruppamento nelle espressioni regolari](grouping.md)




<!--HONumber=Nov16_HO3-->


