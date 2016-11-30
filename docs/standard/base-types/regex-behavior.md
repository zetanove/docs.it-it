---
title: Dettagli sul comportamento delle espressioni regolari
description: Dettagli sul comportamento delle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 6f11047f-45a4-4caf-a259-18abe08cc0d2
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: fa0513a5b450742995bd86fca495ba9904e7361b

---

# <a name="details-of-regular-expression-behavior"></a>Dettagli sul comportamento delle espressioni regolari


Il motore delle espressioni regolari di .NET è un selettore di espressioni regolari di backtracking che incorpora un motore NFA (Nondeterministic Finite Automaton) tradizionale come quello usato da Perl, Python, Emacs e Tcl. Ciò lo distingue dai motori delle espressioni regolari puri DFA (Deterministic Finite Automaton), più veloci ma più limitati, come quelli usati in awk, egrep o lex. Lo distingue anche dai motori NFA POSIX, standardizzati ma più lenti. Nella sezione seguente vengono descritti i tre tipi di motori delle espressioni regolari e viene spiegato perché le espressioni regolari in .NET vengono implementate usando un motore NFA tradizionale.

## <a name="benefits-of-the-nfa-engine"></a>Vantaggi del motore NFA

Quando i motori DFA eseguono criteri di ricerca, l'ordine di elaborazione è basato sulla stringa di input. Il motore inizia all'inizio della stringa di input e procede in sequenza per determinare se il carattere successivo corrisponde al criterio di espressione regolare. È in grado di garantire la corrispondenza con la stringa più lunga possibile. Poiché non testano mai due volte lo stesso carattere, i motori DFA non supportano il backtracking. Tuttavia, poiché un motore DFA contiene solo stati finiti, non è in grado di trovare corrispondenze con i backreference e dato che non crea un'espansione esplicita, non è in grado di acquisire sottoespressioni.

A differenza dei motori DFA, quando i motori NFA tradizionali eseguono criteri di ricerca, l'ordine di elaborazione dipende dal criterio di espressione regolare. Durante l'elaborazione di un elemento di linguaggio specifico, il motore usa la corrispondenza greedy, ossia trova la corrispondenza con la maggior parte possibile della stringa di input. Ma salva anche il proprio stato dopo aver trovato la corrispondenza con una sottoespressione. Se la ricerca di una corrispondenza ha esito negativo, il motore torna allo stato salvato in modo da tentare altre corrispondenze. Questo processo di abbandono una corrispondenza riuscita con una sottoespressione in modo da consentire la corrispondenza di altri elementi di linguaggio nell'espressione regolare è noto come backtracking. I motori NFA usano il backtracking per testare tutte le possibili espansioni di un'espressione regolare in un ordine specifico e accettano la prima corrispondenza. Poiché un motore NFA tradizionale crea un'espansione specifica dell'espressione regolare per trovare una corrispondenza, è in grado di acquisire corrispondenze di sottoespressioni e backreference corrispondenti. Tuttavia, dato che un motore NFA tradizionale usa il backtracking, è possibile che visiti lo stesso stato più volte se arriva allo stato attraverso percorsi diversi. Di conseguenza, può diventare estremamente lento nel peggiore dei casi. Un motore NFA tradizionale accetta la prima corrispondenza trovata, quindi tralascia altre corrispondenze che potrebbero essere più lunghe.

I motori NFA POSIX sono come i motori NFA tradizionali, ad eccezione del fatto che continuano a eseguire il backtracking fino a quando possono di aver trovato la corrispondenza più lunga possibile. Di conseguenza, un motore NFA POSIX è più lento rispetto a un motore NFA tradizionale e quando si usa un motore NFA POSIX, non è possibile preferire una corrispondenza più breve rispetto a una più lunga modificando l'ordine di ricerca di backtracking. 

I motori NFA tradizionali sono i preferiti dei programmatori perché offrono un maggiore controllo sulla corrispondenza delle stringhe rispetto ai motori DFA o NFA POSIX. Benché nel peggiore dei casi possano essere lenti, è possibile impostarli in modo che trovino le corrispondenze in tempo lineare o polinomiale usando criteri che riducono le ambiguità e limitano il backtracking. In altre parole, anche se la potenza e la flessibilità dei motori NFA possono influire negativamente sulle prestazioni, nella maggior parte dei casi questi motori offrono prestazioni da buone ad accettabili se un'espressione regolare è ben scritta e si evitano situazioni in cui il backtracking peggiora notevolmente le prestazioni.

> [!NOTE]
> Per informazioni sui problemi di prestazioni causati dall'uso eccessivo del backtracking e su come elaborare un'espressione regolare in modo da risolverli, vedere [Backtracking nelle espressioni regolari](backtracking.md).
 
## <a name="net-framework-engine-capabilities"></a>Funzionalità del motore di .NET Framework

Per usufruire dei vantaggi offerti da un motore NFA tradizionale, il motore delle espressioni regolari di .NET include un set completo di costrutti per consentire ai programmatori di controllare il motore di backtracking. Tali costrutti possono essere usati per trovare più rapidamente le corrispondenze o per favorire espansioni specifiche rispetto ad altre.

Altre funzionalità del motore delle espressioni regolari di .NET sono: 

### <a name="lazy-quantifiers"></a>Quantificatori lazy

Quantificatori lazy: **??**, __*?__, **+?**, **{**_n_**,**_m_**}?**. Questi costrutti indicano al motore di backtracking di cercare prima il numero minimo di ripetizioni. Al contrario, i normali quantificatori greedy tentano di trovare prima il numero massimo di ripetizioni. L'esempio che segue illustrata la differenza tra i due tipi. Un'espressione regolare trova la corrispondenza con una frase che termina con un numero e un gruppo di acquisizione deve estrarre tale numero. L'espressione regolare `.+(\d+)\.` include il quantificatore greedy `.+`, che fa in modo che il motore delle espressioni regolari acquisisca solo l'ultima cifra del numero. Al contrario, l'espressione regolare `.+?(\d+)\.` include il quantificatore lazy `.+?`, che fa in modo che il motore delle espressioni regolari acquisisca l'intero numero.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string greedyPattern = @".+(\d+)\.";
      string lazyPattern = @".+?(\d+)\.";
      string input = "This sentence ends with the number 107325.";
      Match match;

      // Match using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (greedy): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);
       // Match using lazy quantifier .+?.
      match = Regex.Match(input, lazyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (lazy): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", lazyPattern);
   }
}
// The example displays the following output:
//       Number at end of sentence (greedy): 5
//       Number at end of sentence (lazy): 107325
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim greedyPattern As String = ".+(\d+)\."
      Dim lazyPattern As String = ".+?(\d+)\."
      Dim input As String = "This sentence ends with the number 107325."
      Dim match As Match

      ' Match using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (greedy): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If

      ' Match using lazy quantifier .+?.
      match = Regex.Match(input, lazyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (lazy): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", lazyPattern)
      End If
   End Sub
End Module
' The example displays the following output:
'       Number at end of sentence (greedy): 5
'       Number at end of sentence (lazy): 107325
```

Le versioni greedy e lazy di questa espressione regolare vengono definite come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`.+` (quantificatore greedy) | Trova almeno un'occorrenza di qualsiasi carattere. In questo modo il motore delle espressioni regolari considera soddisfatta la corrispondenza con l'intera stringa ed esegue il backtracking, necessario per verificare le corrispondenze con il resto del criterio.
`.+?` (quantificatore lazy) | Trova almeno un'occorrenza di qualsiasi carattere, ma accetta la corrispondenza con il minor numero possibile di caratteri.
`(\d+)` | Trova la corrispondenza con almeno un carattere alfanumerico e la assegna al primo gruppo di acquisizione.
`\.` | Trova la corrispondenza con un punto.
 
Per altre informazioni sui quantificatori lazy, vedere [Quantificatori nelle espressioni regolari](quantifiers.md).

### <a name="positive-lookahead"></a>Lookahead positivo

Lookahead positivo: **(?**=_subexpression_**)**. Questa funzionalità consente al motore di backtracking tornare alla stessa posizione nel testo dopo aver trovato la corrispondenza con una sottoespressione. È utile per eseguire una ricerca in tutto il testo verificando più criteri a partire dalla stessa posizione. Ciò consente anche al motore di verificare che una sottostringa esista alla fine della corrispondenza senza includere la sottostringa nel testo di cui è stata trovata la corrispondenza. Nell'esempio seguente il lookahead positivo viene usato per estrarre le parole di una frase che non sono seguite da simboli di punteggiatura.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b[A-Z]+\b(?=\P{P})";
      string input = "If so, what comes next?";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       If
//       what
//       comes
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b[A-Z]+\b(?=\P{P})"
      Dim input As String = "If so, what comes next?"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       If
'       what
'       comes
```

L'espressione regolare `\b[A-Z]+\b(?=\P{P})` viene definita come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`[A-Z]+` | Trova la corrispondenza con qualsiasi carattere alfabetico una o più volte. Poiché il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) viene chiamato con l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase), il confronto non rileva la distinzione tra maiuscole e minuscole. 
`\b` | Termina la corrispondenza sul confine di parola.
`(?=\P{P})` | Esegue il lookahead per determinare se il carattere successivo è un simbolo di punteggiatura. In caso contrario, la corrispondenza ha esito positivo.

Per altre informazioni sulle asserzioni per il lookahead positivo, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

### <a name="negative-lookahead"></a>Lookahead negativo

Lookahead negativo: **(?!**_subexpression_**)**. Questa funzionalità aggiunge la capacità di considerare soddisfatta la corrispondenza con un'espressione solo se non trova la corrispondenza con una sottoespressione. Ciò risulta particolarmente utile per abbreviare una ricerca, poiché spesso è più semplice formulare un'espressione per un caso da eliminare che un'espressione che individua i casi da includere. Ad esempio, è difficile scrivere un'espressione per le parole che non iniziano con "non". Nell'esempio seguente viene usato il lookahead negativo per escluderle.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?!non)\w+\b";
      string input = "Nonsense is not always non-functional.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       is
//       not
//       always
//       functional
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?!non)\w+\b"
      Dim input As String = "Nonsense is not always non-functional."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       is
'       not
'       always
'       functional
```

Il criterio di ricerca di espressioni regolari `\b(?!non)\w+\b` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(?!non)` | Esegue il lookahead per verificare che la stringa corrente non inizi con "non". In caso contrario, la corrispondenza ha esito negativo.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`\b` | Termina la corrispondenza sul confine di parola.
 
Per altre informazioni sulle asserzioni per il lookahead negativo, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

### <a name="conditional-evaluation"></a>Valutazione condizionale

Valutazione condizionale: **(?(**_expression_**)**_yes_&#124;_no_**)** e **(?(**_name_**)**_yes_&#124;_no_**)**, dove *expression* è una sottoespressione di cui trovare la corrispondenza, *name* è il nome di un gruppo di acquisizione, *yes* è la stringa di cui trovare la corrispondenza se viene soddisfatta la corrispondenza con *expression* o *name* è un gruppo valido, non vuoto e acquisito e *no* è la sottoespressione di cui trovare la corrispondenza se la corrispondenza con *expression* non è soddisfatta o *name* non è un gruppo valido, non vuoto e acquisito. Questa funzionalità consente al motore di eseguire la ricerca usando più di un criterio alternativo, in base al risultato della corrispondenza di una sottoespressione precedente o al risultato di un'asserzione di larghezza zero. Ciò offre una forma più efficace di backreference che consente, ad esempio, di trovare la corrispondenza con una sottoespressione in base al fatto che sia stata trovata o meno la corrispondenza con una sottoespressione precedente. L'espressione regolare nell'esempio seguente trova la corrispondenza con paragrafi destinati all'uso sia pubblico che interno. I paragrafi destinati solo all'uso interno iniziano con un tag `<PRIVATE>`. Il criterio di espressione regolare `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$` usa la valutazione condizionale per assegnare il contenuto dei paragrafi destinati all'uso pubblico e all'uso interno a gruppi di acquisizione separati. I paragrafi possono quindi essere gestiti in modo diverso.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "<PRIVATE> This is not for public consumption." + Environment.NewLine + 
                     "But this is for public consumption." + Environment.NewLine + 
                     "<PRIVATE> Again, this is confidential.\n";  
      string pattern = @"^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$";
      string publicDocument = null, privateDocument = null;

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
      {
         if (match.Groups[1].Success) {
            privateDocument += match.Groups[1].Value + "\n";
         }
         else {
            publicDocument += match.Groups[3].Value + "\n";   
            privateDocument += match.Groups[3].Value + "\n";
         }  
      }

      Console.WriteLine("Private Document:");
      Console.WriteLine(privateDocument);
      Console.WriteLine("Public Document:");
      Console.WriteLine(publicDocument);
   }
}
// The example displays the following output:
//    Private Document:
//    This is not for public consumption.
//    But this is for public consumption.
//    Again, this is confidential.
//    
//    Public Document:
//    But this is for public consumption.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "<PRIVATE> This is not for public consumption." + vbCrLf + _
                            "But this is for public consumption." + vbCrLf + _
                            "<PRIVATE> Again, this is confidential." + vbCrLf
      Dim pattern As String = "^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$"
      Dim publicDocument As String = Nothing
      Dim privateDocument As String = Nothing

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         If match.Groups(1).Success Then
            privateDocument += match.Groups(1).Value + vbCrLf
         Else
            publicDocument += match.Groups(3).Value + vbCrLf   
            privateDocument += match.Groups(3).Value + vbCrLf
         End If  
      Next

      Console.WriteLine("Private Document:")
      Console.WriteLine(privateDocument)
      Console.WriteLine("Public Document:")
      Console.WriteLine(publicDocument)
   End Sub
End Module
' The example displays the following output:
'    Private Document:
'    This is not for public consumption.
'    But this is for public consumption.
'    Again, this is confidential.
'    
'    Public Document:
'    But this is for public consumption.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`^` | Inizia la corrispondenza all'inizio di una riga.
`(?<Pvt>\<PRIVATE\>\s)?` | Trova la corrispondenza con zero o un'occorrenza della stringa `<PRIVATE>` seguita da un carattere di spazio vuoto. Assegna la corrispondenza a un gruppo di acquisizione denominato Pvt.
`(?(Pvt)((\w+\p{P}?\s)+)` | Se il gruppo di acquisizione `Pvt` esiste, trova una o più occorrenze di uno o più caratteri alfanumerici seguiti da zero o un separatore di punteggiatura seguito da un carattere di spazio vuoto. Assegna la sottostringa al primo gruppo di acquisizione.
`&#124;((\w+\p{P}?\s)+))` | Se il gruppo di acquisizione `Pvt` non esiste, trova una o più occorrenze di uno o più caratteri alfanumerici seguiti da zero o un separatore di punteggiatura seguito da un carattere di spazio vuoto. Assegna la sottostringa al terzo gruppo di acquisizione.
`\r?$` | Trova la corrispondenza alla fine di una riga o alla fine della stringa.
 
Per altre informazioni sulla valutazione condizionale, vedere [Costrutti di alternanza nelle espressioni regolari](alternation.md).

### <a name="balancing-group-definitions"></a>Definizioni di gruppo di bilanciamento

Definizioni di gruppo di bilanciamento: **(?<**_nome1-nome2_**>** _subexpression_**)**. Questa funzionalità consente al motore delle espressioni regolari di tenere traccia dei costrutti annidati, ad esempio parentesi o parentesi quadre di apertura e chiusura. Per un esempio, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

### <a name="nonbacktracking-subexpressions"></a>Sottoespressioni di non backtracking

Sottoespressioni non di backtracking (note anche come sottoespressioni greedy): **(?>**_subexpression_**)**. Questa funzionalità consente al motore di backtracking di garantire che una sottoespressione corrisponda solo alla prima corrispondenza trovata per tale sottoespressione, come se l'espressione venisse eseguita indipendentemente dall'espressione che la contiene. Se non si usa questo costrutto, il backtracking dall'espressione più ampia può modificare il comportamento di una sottoespressione. Ad esempio, l'espressione regolare `(a+)\w` trova la corrispondenza con uno o più caratteri "a", insieme a un carattere alfanumerico che segue la sequenza di caratteri "a", e assegna la sequenza di caratteri "a" al primo gruppo di acquisizione. Se però anche l'ultimo carattere della stringa di input è "a", l'elemento di linguaggio `\w` ne determina la corrispondenza e il carattere non viene incluso nel gruppo acquisito.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "aaaaa", "aaaaab" };
      string backtrackingPattern = @"(a+)\w";
      Match match;

      foreach (string input in inputs) {
         Console.WriteLine("Input: {0}", input);
         match = Regex.Match(input, backtrackingPattern);
         Console.WriteLine("   Pattern: {0}", backtrackingPattern);
         if (match.Success) { 
            Console.WriteLine("      Match: {0}", match.Value);
            Console.WriteLine("      Group 1: {0}", match.Groups[1].Value);
         }
         else {
            Console.WriteLine("      Match failed.");
         }   
      }
      Console.WriteLine();            
   }
}
// The example displays the following output:
//       Input: aaaaa
//          Pattern: (a+)\w
//             Match: aaaaa
//             Group 1: aaaa
//       Input: aaaaab
//          Pattern: (a+)\w
//             Match: aaaaab
//             Group 1: aaaaa
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "aaaaa", "aaaaab" }
      Dim backtrackingPattern As String = "(a+)\w"
      Dim match As Match

      For Each input As String In inputs
         Console.WriteLine("Input: {0}", input)
         match = Regex.Match(input, backtrackingPattern)
         Console.WriteLine("   Pattern: {0}", backtrackingPattern)
         If match.Success Then 
            Console.WriteLine("      Match: {0}", match.Value)
            Console.WriteLine("      Group 1: {0}", match.Groups(1).Value)
         Else 
            Console.WriteLine("      Match failed.")
         End If   
      Next
      Console.WriteLine()            
   End Sub
End Module
' The example displays the following output:
'       Input: aaaaa
'          Pattern: (a+)\w
'             Match: aaaaa
'             Group 1: aaaa
'       Input: aaaaab
'          Pattern: (a+)\w
'             Match: aaaaab
'             Group 1: aaaaa
```

L'espressione regolare `((?>a+))\w` evita questo comportamento. Poiché la corrispondenza di tutti i caratteri "a" consecutivi viene determinata senza backtracking, il primo gruppo di acquisizione include tutti i caratteri "a" consecutivi. Se i caratteri "a" non sono seguiti da almeno un carattere diverso da "a", la corrispondenza ha esito negativo.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "aaaaa", "aaaaab" };
      string nonbacktrackingPattern = @"((?>a+))\w";
      Match match;

      foreach (string input in inputs) {
         Console.WriteLine("Input: {0}", input);
         match = Regex.Match(input, nonbacktrackingPattern);
         Console.WriteLine("   Pattern: {0}", nonbacktrackingPattern);
         if (match.Success) { 
            Console.WriteLine("      Match: {0}", match.Value);
            Console.WriteLine("      Group 1: {0}", match.Groups[1].Value);
         }
         else {
            Console.WriteLine("      Match failed.");
         }   
      }
      Console.WriteLine();            
   }
}
// The example displays the following output:
//       Input: aaaaa
//          Pattern: ((?>a+))\w
//             Match failed.
//       Input: aaaaab
//          Pattern: ((?>a+))\w
//             Match: aaaaab
//             Group 1: aaaaa
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "aaaaa", "aaaaab" }
      Dim nonbacktrackingPattern As String = "((?>a+))\w"
      Dim match As Match

      For Each input As String In inputs
         Console.WriteLine("Input: {0}", input)
         match = Regex.Match(input, nonbacktrackingPattern)
         Console.WriteLine("   Pattern: {0}", nonbacktrackingPattern)
         If match.Success Then 
            Console.WriteLine("      Match: {0}", match.Value)
            Console.WriteLine("      Group 1: {0}", match.Groups(1).Value)
         Else 
            Console.WriteLine("      Match failed.")
         End If   
      Next
      Console.WriteLine()            
   End Sub
End Module
' The example displays the following output:
'       Input: aaaaa
'          Pattern: ((?>a+))\w
'             Match failed.
'       Input: aaaaab
'          Pattern: ((?>a+))\w
'             Match: aaaaab
'             Group 1: aaaaa
```

Per altre informazioni sulle sottoespressioni non di backtracking, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

### <a name="right-to-left-matching"></a>Corrispondenza da destra a sinistra

Corrispondenza da destra a sinistra specificata passando l'opzione [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) a un costruttore della classe [Regex](xref:System.Text.RegularExpressions.Regex) o al metodo corrispondente dell'istanza statica. Questa funzionalità è utile durante la ricerca da destra verso sinistra anziché da sinistra verso destra oppure nei casi in cui risulta più efficace iniziare una corrispondenza nella parte destra del criterio anziché in quella sinistra. Come illustrato nell'esempio seguente, l'uso della corrispondenza da destra a sinistra può modificare il comportamento dei quantificatori greedy. Nell'esempio vengono condotte due ricerche di una frase che termina con un numero. La ricerca da sinistra a destra che usa il quantificatore greedy `+` trova la corrispondenza con una delle sei cifre nella frase, mentre la ricerca da destra a sinistra trova la corrispondenza con tutte le sei cifre. Per una descrizione del criterio di espressione regolare, vedere l'esempio che illustra i quantificatori lazy in precedenza in questa sezione.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string greedyPattern = @".+(\d+)\.";
      string input = "This sentence ends with the number 107325.";
      Match match;

      // Match from left-to-right using lazy quantifier .+?.
      match = Regex.Match(input, greedyPattern);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (left-to-right): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);

      // Match from right-to-left using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern, RegexOptions.RightToLeft);
      if (match.Success)
         Console.WriteLine("Number at end of sentence (right-to-left): {0}", 
                           match.Groups[1].Value);
      else
         Console.WriteLine("{0} finds no match.", greedyPattern);
   }
}
// The example displays the following output:
//       Number at end of sentence (left-to-right): 5
//       Number at end of sentence (right-to-left): 107325
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim greedyPattern As String = ".+(\d+)\."
      Dim input As String = "This sentence ends with the number 107325."
      Dim match As Match

      ' Match from left-to-right using lazy quantifier .+?.
      match = Regex.Match(input, greedyPattern)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (left-to-right): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If

      ' Match from right-to-left using greedy quantifier .+.
      match = Regex.Match(input, greedyPattern, RegexOptions.RightToLeft)
      If match.Success Then
         Console.WriteLine("Number at end of sentence (right-to-left): {0}", 
                           match.Groups(1).Value)
      Else
         Console.WriteLine("{0} finds no match.", greedyPattern)
      End If
   End Sub
End Module
' The example displays the following output:
'       Number at end of sentence (left-to-right): 5
'       Number at end of sentence (right-to-left): 107325
```

Per altre informazioni sulla corrispondenza da destra a sinistra, vedere [Opzioni di espressioni regolari](options.md).

### <a name="positive-and-negative-lookbehind"></a>Lookbehind positivo e negativo

Lookbehind positivo e negativo: **(?<**=_subexpression_**)** per lookbehind positivo e **(?<!**_subexpression_**)** per lookbehind negativo. Questa funzionalità è simile a lookahead, illustrata in precedenza in questo argomento. Poiché il motore delle espressioni regolari consente la corrispondenza da destra a sinistra completa, le espressioni regolari consentono lookbehind illimitati. Il lookbehind positivo e negativo consente inoltre di evitare l'annidamento di quantificatori quando la sottoespressione annidata è un superset di un'espressione esterna. Le espressioni regolari con tali quantificatori spesso influiscono negativamente sulle prestazioni. L'esempio seguente, ad esempio, verifica se una stringa inizia e termina con un carattere alfanumerico e se qualsiasi altro carattere nella stringa appartiene a un subset più ampio. Il criterio costituisce una parte dell'espressione regolare usata per convalidare gli indirizzi di posta elettronica. Per altre informazioni, vedere [Procedura: Verificare che le stringhe siano nel formato di posta elettronica valido](verify-format.md).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "jack.sprat", "dog#", "dog#1", "me.myself", 
                          "me.myself!" };
      string pattern = @"^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$";
      foreach (string input in inputs) {
         if (Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase))
            Console.WriteLine("{0}: Valid", input);
         else
            Console.WriteLine("{0}: Invalid", input);
      }
   }
}
// The example displays the following output:
//       jack.sprat: Valid
//       dog#: Invalid
//       dog#1: Valid
//       me.myself: Valid
//       me.myself!: Invalid
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "jack.sprat", "dog#", "dog#1", "me.myself", 
                                 "me.myself!" }
      Dim pattern As String = "^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$"
      For Each input As String In inputs
         If Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase) Then
            Console.WriteLine("{0}: Valid", input)
         Else
            Console.WriteLine("{0}: Invalid", input)
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       jack.sprat: Valid
'       dog#: Invalid
'       dog#1: Valid
'       me.myself: Valid
'       me.myself!: Invalid
```

L'espressione regolare `^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$` è definita nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Inizia la ricerca della corrispondenza all'inizio della stringa.
`[A-Z0-9]` | Trova la corrispondenza con qualsiasi carattere numerico o alfanumerico. Il confronto non rileva la differenza tra maiuscole e minuscole.
`([-!#$%&'.*+/=?^`{}&#124;~\w])*` | Trova zero o più occorrenze di qualsiasi carattere alfanumerico o di uno qualsiasi dei seguenti caratteri: -, !, #, $, %, &, ', ., *, +, /, =, ?, ^, `, {, }, &#124; o ~.
`(?<=[A-Z0-9])` | Esegue il lookbehind al carattere precedente, che deve essere numerico o alfanumerico. Il confronto non rileva la differenza tra maiuscole e minuscole.
`$` | Terminare la corrispondenza alla fine della stringa.
 
Per altre informazioni sul lookbehind positivo e negativo, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).


## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | ----------- 
[Backtracking](backtracking.md) | Informazioni su come il backtracking delle espressioni regolari si dirama per trovare corrispondenze alternative.
[Compilazione e riutilizzo](compilation.md) | Informazioni sulla compilazione e sul riutilizzo di espressioni regolari per ottimizzare le prestazioni.
[Thread safety](thread-safety.md) | Informazioni sulla modalità di thread safety delle espressioni regolari in cui viene spiegato quando è necessario sincronizzare l'accesso a oggetti di espressione regolare.
[Espressioni regolari .NET](regular-expressions.md) | Panoramica dell'aspetto del linguaggio di programmazione delle espressioni regolari.
[Modello a oggetti delle espressioni regolari](object-model.md) | Esempi di codice e informazioni che illustrano l'uso delle classi di espressioni regolari.
[Esempi di espressioni regolari](regex-examples.md) | Esempi di codice che illustrano l'uso delle espressioni regolari nelle applicazioni comuni.
[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md) | Informazioni su set di caratteri, operatori e costrutti che è possibile usare per definire le espressioni regolari.
 
## <a name="reference"></a>Riferimento

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)




<!--HONumber=Nov16_HO3-->


