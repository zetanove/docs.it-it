---
title: Opzioni di espressione regolare
description: Opzioni di espressione regolare
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2db2c3e6-953e-4913-8168-d707c437f2df
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 21672e28d0e76b98f6dac698096fccb2ce4edd03

---

# <a name="regular-expression-options"></a>Opzioni di espressione regolare

Per impostazione predefinita, il confronto di una stringa di input con qualsiasi carattere letterale in un criterio di ricerca di espressioni regolari prevede la distinzione tra maiuscole e minuscole. Gli spazi vuoti in un criterio di ricerca di espressioni regolari vengono interpretati come caratteri di spazio vuoto letterali e i gruppi di acquisizione in un'espressione regolare sono denominati in modo sia implicito che esplicito. È possibile modificare questi e molti altri aspetti del comportamento predefinito delle espressioni regolari specificando le relative opzioni. Queste opzioni, elencate nella tabella seguente, possono essere incluse inline come parte del criterio di ricerca di espressioni regolari o in alternativa fornite a un costruttore della classe [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) o a un metodo statico dei criteri di ricerca come valore di enumerazione [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions). 

Membro RegexOptions | Carattere inline | Effetto
------------------- | ---------------- | ------ 
[None](xref:System.Text.RegularExpressions.RegexOptions.None) | Non disponibile | Usare il comportamento predefinito. Per altre informazioni, vedere [Opzioni predefinite](#default-options).
[IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) | **i** | Usa la corrispondenza che non fa distinzione tra maiuscole e minuscole. Per altre informazioni, vedere [Corrispondenza senza distinzione tra maiuscole e minuscole](#case-insensitive-matching).
[Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) | **m** | Usare la modalità multiriga, in cui **^ ** e **$** corrispondono all'inizio e alla fine di una riga, anziché all'inizio e alla fine della stringa di input. Per altre informazioni, vedere [Modalità multiriga](#multiline-mode).
[Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) | **s** | Usare la modalità a riga singola, in cui il punto (**.**) corrisponde a qualsiasi carattere anziché a tutti i caratteri tranne **\n**. Per altre informazioni, vedere [Modalità a riga singola](#single-line-mode).
[ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) | **n** | Non acquisire gruppi senza nome. Le uniche acquisizioni valide sono i gruppi denominati o numerati in modo esplicito in formato **(?<**_nome_**>** _sottoespressione_**)**. Per altre informazioni, vedere [Solo acquisizioni esplicite](#explicit-captures-only).
[Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) | Non disponibile | Compila l'espressione regolare in un assembly. Per altre informazioni, vedere [Espressioni regolari compilate](#compiled-regular-expressions).
[IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) | **x** | Escludere gli spazi vuoti senza caratteri di escape nel criterio e abilitare i commenti dopo un simbolo di cancelletto (**#**). Per altre informazioni, vedere [Ignora spazi vuoti](#ignore-white-space).
[RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) | Non disponibile | Modifica la direzione di ricerca. La ricerca viene eseguita da destra verso sinistra, anziché da sinistra verso destra. Per altre informazioni, vedere [Modalità da destra a sinistra](#right-to-left-mode).
[ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) | Non disponibile | Abilita un comportamento conforme a ECMAScript per l'espressione. Per altre informazioni, vedere [Comportamento di corrispondenza ECMAScript](#ecmascript-matching-behavior).
[CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) | Non disponibile | Ignora le differenze di cultura nella lingua. Per altre informazioni, vedere [Confronto con impostazioni cultura non dipendenti da paese/area geografica](#comparison-using-the-invariant-culture).
 
## <a name="specifying-the-options"></a>Specifica delle opzioni

È possibile specificare le opzioni per le espressioni regolari in tre modi:

* Nel parametro *options* di un costruttore della classe [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex), ad esempio [Regex.Regex(String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.%23ctor(System.String,System.Text.RegularExpressions.RegexOptions)), o un metodo statico (Shared in Visual Basic) dei criteri di ricerca, ad esempio [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)). Il parametro *options* è una combinazione OR bit per bit dei valori enumerati [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions). 

  Quando vengono specificate opzioni per un'istanza di [Regex](xref:System.Text.RegularExpressions.Regex) usando il parametro *options* di un costruttore di classe, le opzioni vengono assegnate alla proprietà [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions). Tuttavia, la proprietà [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) non rispecchia le opzioni inline nel criterio di ricerca di espressioni regolari stesso. 

  Nell'esempio seguente viene illustrato questo concetto. Il parametro *options* del metodo [Regex.Match(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene usato per abilitare la corrispondenza senza distinzione tra maiuscole e minuscole e per ignorare gli spazi vuoti nel criterio durante l'identificazione delle parole che iniziano con la lettera "d".

  ```csharp
  string pattern = @"d \w+ \s";
  string input = "Dogs are decidedly good pets.";
  RegexOptions options = RegexOptions.IgnoreCase | RegexOptions.IgnorePatternWhitespace;
  
  foreach (Match match in Regex.Matches(input, pattern, options))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "d \w+ \s"
  Dim input As String = "Dogs are decidedly good pets."
  Dim options As RegexOptions = RegexOptions.IgnoreCase Or RegexOptions.IgnorePatternWhitespace

  For Each match As Match In Regex.Matches(input, pattern, options)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9.  
  ```

* Applicando le opzioni inline in un criterio di ricerca di espressioni regolari con la sintassi **(?imnsx-imnsx)**. L'opzione si applica al criterio dal punto in cui viene definita fino alla fine del criterio oppure fino al punto in cui viene annullata da un'altra opzione inline. Si noti che la proprietà [System.Text.RegularExpressions.RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) di un'istanza di [Regex](xref:System.Text.RegularExpressions.Regex) non rispecchia queste opzioni inline. Per altre informazioni, vedere l'argomento [Costrutti vari nelle espressioni regolari](miscellaneous.md).

  Nell'esempio seguente viene illustrato questo concetto. Le opzioni online vengono usate per abilitare la corrispondenza senza distinzione tra maiuscole e minuscole e per ignorare gli spazi vuoti nel criterio durante l'identificazione delle parole che iniziano con la lettera "d".

  ```csharp
  string pattern = @"(?ix) d \w+ \s";
  string input = "Dogs are decidedly good pets.";
  
  foreach (Match match in Regex.Matches(input, pattern))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "\b(?ix) d \w+ \s"
  Dim input As String = "Dogs are decidedly good pets."

  For Each match As Match In Regex.Matches(input, pattern)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9.  
  ```

* Applicando opzioni inline in un particolare costrutto di raggruppamento in un criterio di ricerca di espressioni regolari con la sintassi **(?imnsx-imnsx:**_sottoespressione_**)**. Nessun segno prima di un set di opzioni attiva il set. Un segno meno prima di un set di opzioni disattiva il set. **?** è una parte fissa della sintassi del costrutto di linguaggio richiesta se vengono abilitate o disabilitate funzioni. L'opzione si applica solo al gruppo specificato. Per altre informazioni, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

  Nell'esempio seguente viene illustrato questo concetto. Le opzioni online vengono usate in un costrutto di raggruppamento per abilitare la corrispondenza senza distinzione tra maiuscole e minuscole e per ignorare gli spazi vuoti nel criterio durante l'identificazione delle parole che iniziano con la lettera "d".

  ```csharp
  string pattern = @"\b(?ix: d \w+)\s";
  string input = "Dogs are decidedly good pets.";
  
  foreach (Match match in Regex.Matches(input, pattern))
     Console.WriteLine("'{0}// found at index {1}.", match.Value, match.Index);
  // The example displays the following output:
  //    'Dogs // found at index 0.
  //    'decidedly // found at index 9.      
  ```

  ```vb
  Dim pattern As String = "\b(?ix: d \w+)\s"
  Dim input As String = "Dogs are decidedly good pets."

  For Each match As Match In Regex.Matches(input, pattern)
     Console.WriteLine("'{0}' found at index {1}.", match.Value, match.Index)
  Next
  ' The example displays the following output:
  '    'Dogs ' found at index 0.
  '    'decidedly ' found at index 9. 
  ```


Se le opzioni vengono specificate inline, un segno meno (-) prima di un'opzione o di un set di opzioni consente di disattivare tali opzioni. Ad esempio, il costrutto inline **(?ix-ms)** consente di attivare le opzioni [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) e [RegexOptions. IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) e di disattivare le opzioni [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) e [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline). Per impostazione predefinita, tutte le opzioni di espressioni regolari sono disattivate.

> [!NOTE]
> In caso di conflitto tra le opzioni di espressione regolare specificate nel parametro options di un costruttore o di una chiamata a metodo e le opzioni specificate inline in un criterio di ricerca di espressioni regolari, vengono usate le opzioni inline.
 

Le cinque opzioni di espressione regolare seguenti possono essere impostate sia con il parametro *options* che inline:

* [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase)

* [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline)

* [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline)

* [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture)

* [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace)

Le cinque opzioni di espressione regolare seguenti possono essere impostate usando il parametro *options* ma non inline:

* [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None)

* [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled)

* [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft)

* [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant)

* [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript)

## <a name="determining-the-options"></a>Determinazione delle opzioni

È possibile determinare le opzioni fornite a un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) al momento della creazione dell'istanza recuperando il valore della proprietà [Regex.Options](xref:System.Text.RegularExpressions.Regex.Options) di sola lettura.

Per testare la presenza di qualsiasi opzione eccetto [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None), eseguire un'operazione AND con il valore della proprietà [Regex.Options](xref:System.Text.RegularExpressions.Regex.Options) e il valore [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) che interessa. Testare quindi se il risultato corrisponde al valore [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions). L'esempio seguente verifica se l'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) è stata impostata. 

```csharp
if ((rgx.Options & RegexOptions.IgnoreCase) == RegexOptions.IgnoreCase)
   Console.WriteLine("Case-insensitive pattern comparison.");
else
   Console.WriteLine("Case-sensitive pattern comparison.");
```

```vb
If (rgx.Options And RegexOptions.IgnoreCase) = RegexOptions.IgnoreCase Then
   Console.WriteLine("Case-insensitive pattern comparison.")
Else
   Console.WriteLine("Case-sensitive pattern comparison.")
End If 
```

Per testare [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None), determinare se il valore della proprietà [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) è uguale a [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None), come illustrato nell'esempio seguente. 

```csharp
if (rgx.Options == RegexOptions.None)
   Console.WriteLine("No options have been set.");
```

```vb
If rgx.Options = RegexOptions.None Then
   Console.WriteLine("No options have been set.")
End If
```

Nelle sezioni che seguono sono riportate le opzioni supportate dalle espressioni regolari in .NET. 

## <a name="default-options"></a>Opzioni predefinite

L'opzione [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) indica che non sono state specificate opzioni e che il motore delle espressioni regolari usa il comportamento predefinito. Il comportamento predefinito include quanto segue:

* Il criterio viene interpretato come canonico anziché come espressione regolare ECMAScript.

* Il criterio di ricerca di espressioni regolari viene messo in corrispondenza nella stringa di input da sinistra verso destra.

* Nei confronti viene fatta distinzione tra maiuscole e minuscole.

* Gli elementi language **^** e **$** corrispondono all'inizio e alla fine della stringa di input.

* L'elemento language **.** corrisponde a qualsiasi carattere tranne **\n**.

* Qualsiasi spazio vuoto in un criterio di ricerca di espressioni regolari viene interpretato come spazio letterale.

* Nel confronto del criterio con la stringa di input vengono usate le convenzioni delle impostazioni cultura correnti. 

* I gruppi di acquisizione nel criterio di ricerca di espressioni regolari sono sia impliciti che espliciti. 

> [!NOTE]
> L'opzione [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) non ha un equivalente inline. Quando le opzioni di espressioni regolari vengono applicate inline, il comportamento predefinito viene ripristinato opzione per opzione, disattivando una particolare opzione. Ad esempio, `(?i)` disattiva il confronto senza distinzione tra maiuscole e minuscole e `(?-i)` lo ripristina.
 
Poiché l'opzione [RegexOptions.None](xref:System.Text.RegularExpressions.RegexOptions.None) rappresenta il comportamento predefinito del motore delle espressioni regolari, raramente viene specificata in modo esplicito in una chiamata a metodo. Viene invece chiamato un costruttore o un metodo statico dei criteri di ricerca senza un parametro options.

## <a name="caseinsensitive-matching"></a>Corrispondenza senza distinzione tra maiuscole e minuscole

L'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) o l'opzione inline **i** definisce la corrispondenza senza distinzione tra maiuscole e minuscole. Per impostazione predefinita, vengono usate le convenzioni sulla combinazione di maiuscole e minuscole delle impostazioni cultura correnti.

L'esempio seguente definisce un criterio di ricerca di espressioni regolari, `\bthe\w*\b`, che trova la corrispondenza di tutte le parole che iniziano con "the". Poiché la prima chiamata al metodo Match usa il confronto predefinito con distinzione tra maiuscole e minuscole, l'output indica che la stringa "The" che inizia la frase non viene individuata come corrispondenza. La corrispondenza viene individuata quando il metodo [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con le opzioni impostate su [IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase). 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bthe\w*\b";
      string input = "The man then told them about that event.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);

      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern, 
                                            RegexOptions.IgnoreCase))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found then at index 8.
//       Found them at index 18.
//       
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bthe\w*\b"
      Dim input As String = "The man then told them about that event."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern, _
                                               RegexOptions.IgnoreCase)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Found then at index 8.
'       Found them at index 18.
'       
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
```

L'esempio seguente modifica il criterio di ricerca di espressioni regolari dell'esempio precedente in modo da usare opzioni inline anziché il parametro *options* per eseguire il confronto senza distinzione fra maiuscole e minuscole. Il primo criterio definisce l'opzione che non prevede la distinzione tra maiuscole e minuscole in un costrutto di raggruppamento che si applica solo alla lettera "t" nella stringa "the". Poiché il costrutto di opzione si trova all'inizio del criterio, il secondo criterio applica l'opzione che non prevede la distinzione tra maiuscole e minuscole all'intera espressione regolare.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?i:t)he\w*\b";
      string input = "The man then told them about that event.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);

      Console.WriteLine();
      pattern = @"(?i)\bthe\w*\b";
      foreach (Match match in Regex.Matches(input, pattern, 
                                            RegexOptions.IgnoreCase))
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
//       
//       Found The at index 0.
//       Found then at index 8.
//       Found them at index 18.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?i:t)he\w*\b"
      Dim input As String = "The man then told them about that event."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
      Console.WriteLine()
      pattern = "(?i)\bthe\w*\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found {0} at index {1}.", match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
'       
'       Found The at index 0.
'       Found then at index 8.
'       Found them at index 18.
```

## <a name="multiline-mode"></a>Modalità multiriga

L'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline), o l'opzione inline **m**, consente al motore delle espressioni regolari di gestire una stringa di input composta da più righe. Modifica l'interpretazione degli elementi language **^** e **$** in modo che corrispondano all'inizio e alla fine di una riga invece che all'inizio e alla fine della stringa di input. 

Per impostazione predefinita, **$** trova la corrispondenza solo alla fine della stringa di input. Se si specifica l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline), viene trovata la corrispondenza di un carattere di nuova riga **(\n)** o della fine della stringa di input. Non viene tuttavia trovata la corrispondenza di una combinazione carattere di ritorno a capo/avanzamento riga. A questo scopo, usare la sottoespressione **\r?$** anziché semplicemente **$**. 

L'esempio seguente estrae i nomi e i punteggi dei giocatori di bowling e li aggiunge a una raccolta [SortedList&lt;TKey, TValue&gt;](xref:System.Collections.Generic.SortedList%602) che li ordina in ordine decrescente. Il metodo [Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) viene chiamato due volte. Nella prima chiamata al metodo, l'espressione regolare è `^(\w+)\s(\d+)$` e non sono impostate opzioni. Come mostra l'output, poiché il motore delle espressioni regolari non trova corrispondenza tra il criterio di input e l'inizio e la fine della stringa di input, non vengono individuate corrispondenze. Nella seconda chiamata al metodo, l'espressione regolare viene modificata in `^(\w+)\s(\d+)\r?$` e le opzioni sono impostate su [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline). Come mostra l'output, la corrispondenza tra i nomi e i punteggi viene individuata correttamente e i punteggi vengono visualizzati in ordine decrescente.

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      SortedList<int, string> scores = new SortedList<int, string>(new DescendingComparer<int>());

      string input = "Joe 164\n" + 
                     "Sam 208\n" + 
                     "Allison 211\n" + 
                     "Gwen 171\n"; 
      string pattern = @"^(\w+)\s(\d+)$";
      bool matched = false;

      Console.WriteLine("Without Multiline option:");
      foreach (Match match in Regex.Matches(input, pattern))
      {
         scores.Add(Int32.Parse(match.Groups[2].Value), (string) match.Groups[1].Value);
         matched = true;
      }
      if (! matched)
         Console.WriteLine("   No matches.");
      Console.WriteLine();

      // Redefine pattern to handle multiple lines.
      pattern = @"^(\w+)\s(\d+)\r*$";
      Console.WriteLine("With multiline option:");
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
         scores.Add(Int32.Parse(match.Groups[2].Value), (string) match.Groups[1].Value);

      // List scores in descending order. 
      foreach (KeyValuePair<int, string> score in scores)
         Console.WriteLine("{0}: {1}", score.Value, score.Key);
   }
}

public class DescendingComparer<T> : IComparer<T>
{
   public int Compare(T x, T y)
   {
      return Comparer<T>.Default.Compare(x, y) * -1;       
   }
}
// The example displays the following output:
//   Without Multiline option:
//      No matches.
//   
//   With multiline option:
//   Allison: 211
//   Sam: 208
//   Gwen: 171
//   Joe: 164
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim scores As New SortedList(Of Integer, String)(New DescendingComparer(Of Integer)())

      Dim input As String = "Joe 164" + vbCrLf + _
                            "Sam 208" + vbCrLf + _
                            "Allison 211" + vbCrLf + _
                            "Gwen 171" + vbCrLf
      Dim pattern As String = "^(\w+)\s(\d+)$"
      Dim matched As Boolean = False

      Console.WriteLine("Without Multiline option:")
      For Each match As Match In Regex.Matches(input, pattern)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
         matched = True
      Next
      If Not matched Then Console.WriteLine("   No matches.")
      Console.WriteLine()

      ' Redefine pattern to handle multiple lines.
      pattern = "^(\w+)\s(\d+)\r*$"
      Console.WriteLine("With multiline option:")
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
      Next
      ' List scores in descending order. 
      For Each score As KeyValuePair(Of Integer, String) In scores
         Console.WriteLine("{0}: {1}", score.Value, score.Key)
      Next
   End Sub
End Module

Public Class DescendingComparer(Of T) : Implements IComparer(Of T)
   Public Function Compare(x As T, y As T) As Integer _
          Implements IComparer(Of T).Compare
      Return Comparer(Of T).Default.Compare(x, y) * -1       
   End Function
End Class
' The example displays the following output:
'    Without Multiline option:
'       No matches.
'    
'    With multiline option:
'    Allison: 211
'    Sam: 208
'    Gwen: 171
'    Joe: 164
```

Il criterio di ricerca di espressioni regolari `^(\w+)\s(\d+)\r*$` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Comincia all'inizio della riga.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(\d+)` | Trova la corrispondenza con una o più cifre decimali. Equivale al secondo gruppo di acquisizione.
`\r?` | Trova la corrispondenza di zero o un carattere di ritorno a capo.
`$` | Termina alla fine della riga.
 
L'esempio di seguito equivale al precedente, tranne il fatto che viene usata l'opzione inline **(?m)** per impostare l'opzione multiriga.

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      SortedList<int, string> scores = new SortedList<int, string>(new DescendingComparer<int>());

      string input = "Joe 164\n" +  
                     "Sam 208\n" +  
                     "Allison 211\n" +  
                     "Gwen 171\n"; 
      string pattern = @"(?m)^(\w+)\s(\d+)\r*$";

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Multiline))
         scores.Add(Convert.ToInt32(match.Groups[2].Value), match.Groups[1].Value);

      // List scores in descending order. 
      foreach (KeyValuePair<int, string> score in scores)
         Console.WriteLine("{0}: {1}", score.Value, score.Key);
   }
}

public class DescendingComparer<T> : IComparer<T>
{
   public int Compare(T x, T y) 
   {
      return Comparer<T>.Default.Compare(x, y) * -1;       
   }
}
// The example displays the following output:
//    Allison: 211
//    Sam: 208
//    Gwen: 171
//    Joe: 164
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim scores As New SortedList(Of Integer, String)(New DescendingComparer(Of Integer)())

      Dim input As String = "Joe 164" + vbCrLf + _
                            "Sam 208" + vbCrLf + _
                            "Allison 211" + vbCrLf + _
                            "Gwen 171" + vbCrLf
      Dim pattern As String = "(?m)^(\w+)\s(\d+)\r*$"

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.Multiline)
         scores.Add(CInt(match.Groups(2).Value), match.Groups(1).Value)
      Next
      ' List scores in descending order. 
      For Each score As KeyValuePair(Of Integer, String) In scores
         Console.WriteLine("{0}: {1}", score.Value, score.Key)
      Next
   End Sub
End Module

Public Class DescendingComparer(Of T) : Implements IComparer(Of T)
   Public Function Compare(x As T, y As T) As Integer _
          Implements IComparer(Of T).Compare
      Return Comparer(Of T).Default.Compare(x, y) * -1       
   End Function
End Class
' The example displays the following output:
'    Allison: 211
'    Sam: 208
'    Gwen: 171
'    Joe: 164
```

## <a name="singleline-mode"></a>Modalità a riga singola

L'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline), o l'opzione inline s, consente al motore delle espressioni regolari di gestire la stringa di input come se fosse composta da una sola riga. Lo fa modificando il comportamento dell'elemento language punto (**.**) in modo che corrisponda a qualsiasi carattere anziché a qualsiasi carattere ad eccezione del carattere di nuova riga **\n** o \u000A.

Nell'esempio seguente viene illustrato come cambia il comportamento dell'elemento language quando si usa l'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline). L'espressione regolare `^.+` parte dall'inizio della stringa e individua una corrispondenza per ogni carattere. Per impostazione predefinita, la corrispondenza termina alla fine della prima riga. Il modello di espressione regolare corrisponde al carattere di ritorno a capo, **\r** o \u000D, ma non corrisponde a **\n**. Poiché l'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) interpreta l'intera stringa di input come riga singola, ottiene una corrispondenza per ogni carattere nella stringa di input, incluso **\n**.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "^.+";
      string input = "This is one line and" + Environment.NewLine + "this is the second.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(Regex.Escape(match.Value));

      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.Singleline))
         Console.WriteLine(Regex.Escape(match.Value));
   }
}
// The example displays the following output:
//       This\ is\ one\ line\ and\r
//       
//       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^.+"
      Dim input As String = "This is one line and" + vbCrLf + "this is the second."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.SingleLine)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
   End Sub
End Module
' The example displays the following output:
'       This\ is\ one\ line\ and\r
'       
'       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

L'esempio seguente equivale al precedente, tranne per il fatto che viene usata l'opzione inline **(?s)** per impostare la modalità a riga singola. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {      
      string pattern = "(?s)^.+";
      string input = "This is one line and" + Environment.NewLine + "this is the second.";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(Regex.Escape(match.Value));
   }
}
// The example displays the following output:
//       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?s)^.+"
      Dim input As String = "This is one line and" + vbCrLf + "this is the second."

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(Regex.Escape(match.Value))
      Next
   End Sub
End Module
' The example displays the following output:
'       This\ is\ one\ line\ and\r\nthis\ is\ the\ second\.
```

## <a name="explicit-captures-only"></a>Solo acquisizioni esplicite

Per impostazione predefinita, i gruppi di acquisizione vengono definiti dall'uso di parentesi nel criterio di ricerca di espressioni regolari. Ai gruppi denominati viene assegnato un nome o un numero dall'opzione lingua **(?<**_nome_**>** _sottoespressione_**)** mentre i gruppi non denominati sono accessibili mediante indice. Nell'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) i gruppi non denominati precedono i gruppi denominati. 

I costrutti di raggruppamento vengono spesso usati solo per applicare quantificatori a più elementi di linguaggio e le sottostringhe acquisite non sono di alcun interesse. Ad esempio, se l'espressione regolare seguente:

```
\b\(?((\w+),?\s?)+[\.!?]\)?
```

è intesa solo per l'estrazione di frasi che terminano con un punto, un punto esclamativo o un punto interrogativo da un documento, solo la frase risultante (rappresentata dall'oggetto [Match](xref:System.Text.RegularExpressions.Match)) è un elemento di interesse. Le singola parole nella raccolta non lo sono. 

I gruppi di acquisizione che successivamente non vengono usati possono risultare costosi, in quanto il motore delle espressioni regolari deve popolare entrambi gli oggetti raccolta [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) e [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection). In alternativa è possibile usare l'opzione [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) o l'opzione inline **n** per specificare che le sole acquisizioni valide sono i gruppi denominati o numerati in modo esplicito definiti dal costrutto **(?<**_nome_**>** _sottoespressione_**)**. 

Nell'esempio seguente appaiono le informazioni sulle corrispondenze restituite dal criterio di espressione regolare `\b\(?((\w+),?\s?)+[\.!?]\)?` quando viene chiamato il metodo [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.Int32)) con e senza l'opzione [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture). Come indica l'output della prima chiamata al metodo, il motore delle espressioni regolari popola interamente gli oggetti raccolta [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) e [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) con informazioni sulle sottostringhe acquisite. Poiché il secondo metodo viene chiamato con il parametro options impostato su [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture), non acquisisce informazioni sui gruppi.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?((?>\w+),?\s?)+[\.!?]\)?";
      Console.WriteLine("With implicit captures:");
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
      Console.WriteLine();
      Console.WriteLine("With explicit captures only:");
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.ExplicitCapture))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//    With implicit captures:
//    The match: This is the first sentence.
//       Group 0: This is the first sentence.
//          Capture 0: This is the first sentence.
//       Group 1: sentence
//          Capture 0: This
//          Capture 1: is
//          Capture 2: the
//          Capture 3: first
//          Capture 4: sentence
//       Group 2: sentence
//          Capture 0: This
//          Capture 1: is
//          Capture 2: the
//          Capture 3: first
//          Capture 4: sentence
//    The match: Is it the beginning of a literary masterpiece?
//       Group 0: Is it the beginning of a literary masterpiece?
//          Capture 0: Is it the beginning of a literary masterpiece?
//       Group 1: masterpiece
//          Capture 0: Is
//          Capture 1: it
//          Capture 2: the
//          Capture 3: beginning
//          Capture 4: of
//          Capture 5: a
//          Capture 6: literary
//          Capture 7: masterpiece
//       Group 2: masterpiece
//          Capture 0: Is
//          Capture 1: it
//          Capture 2: the
//          Capture 3: beginning
//          Capture 4: of
//          Capture 5: a
//          Capture 6: literary
//          Capture 7: masterpiece
//    The match: I think not.
//       Group 0: I think not.
//          Capture 0: I think not.
//       Group 1: not
//          Capture 0: I
//          Capture 1: think
//          Capture 2: not
//       Group 2: not
//          Capture 0: I
//          Capture 1: think
//          Capture 2: not
//    The match: Instead, it is a nonsensical paragraph.
//       Group 0: Instead, it is a nonsensical paragraph.
//          Capture 0: Instead, it is a nonsensical paragraph.
//       Group 1: paragraph
//          Capture 0: Instead,
//          Capture 1: it
//          Capture 2: is
//          Capture 3: a
//          Capture 4: nonsensical
//          Capture 5: paragraph
//       Group 2: paragraph
//          Capture 0: Instead
//          Capture 1: it
//          Capture 2: is
//          Capture 3: a
//          Capture 4: nonsensical
//          Capture 5: paragraph
//    
//    With explicit captures only:
//    The match: This is the first sentence.
//       Group 0: This is the first sentence.
//          Capture 0: This is the first sentence.
//    The match: Is it the beginning of a literary masterpiece?
//       Group 0: Is it the beginning of a literary masterpiece?
//          Capture 0: Is it the beginning of a literary masterpiece?
//    The match: I think not.
//       Group 0: I think not.
//          Capture 0: I think not.
//    The match: Instead, it is a nonsensical paragraph.
//       Group 0: Instead, it is a nonsensical paragraph.
//          Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b\(?((?>\w+),?\s?)+[\.!?]\)?"
      Console.WriteLine("With implicit captures:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
      Console.WriteLine()
      Console.WriteLine("With explicit captures only:")
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.ExplicitCapture)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'    With implicit captures:
'    The match: This is the first sentence.
'       Group 0: This is the first sentence.
'          Capture 0: This is the first sentence.
'       Group 1: sentence
'          Capture 0: This
'          Capture 1: is
'          Capture 2: the
'          Capture 3: first
'          Capture 4: sentence
'       Group 2: sentence
'          Capture 0: This
'          Capture 1: is
'          Capture 2: the
'          Capture 3: first
'          Capture 4: sentence
'    The match: Is it the beginning of a literary masterpiece?
'       Group 0: Is it the beginning of a literary masterpiece?
'          Capture 0: Is it the beginning of a literary masterpiece?
'       Group 1: masterpiece
'          Capture 0: Is
'          Capture 1: it
'          Capture 2: the
'          Capture 3: beginning
'          Capture 4: of
'          Capture 5: a
'          Capture 6: literary
'          Capture 7: masterpiece
'       Group 2: masterpiece
'          Capture 0: Is
'          Capture 1: it
'          Capture 2: the
'          Capture 3: beginning
'          Capture 4: of
'          Capture 5: a
'          Capture 6: literary
'          Capture 7: masterpiece
'    The match: I think not.
'       Group 0: I think not.
'          Capture 0: I think not.
'       Group 1: not
'          Capture 0: I
'          Capture 1: think
'          Capture 2: not
'       Group 2: not
'          Capture 0: I
'          Capture 1: think
'          Capture 2: not
'    The match: Instead, it is a nonsensical paragraph.
'       Group 0: Instead, it is a nonsensical paragraph.
'          Capture 0: Instead, it is a nonsensical paragraph.
'       Group 1: paragraph
'          Capture 0: Instead,
'          Capture 1: it
'          Capture 2: is
'          Capture 3: a
'          Capture 4: nonsensical
'          Capture 5: paragraph
'       Group 2: paragraph
'          Capture 0: Instead
'          Capture 1: it
'          Capture 2: is
'          Capture 3: a
'          Capture 4: nonsensical
'          Capture 5: paragraph
'    
'    With explicit captures only:
'    The match: This is the first sentence.
'       Group 0: This is the first sentence.
'          Capture 0: This is the first sentence.
'    The match: Is it the beginning of a literary masterpiece?
'       Group 0: Is it the beginning of a literary masterpiece?
'          Capture 0: Is it the beginning of a literary masterpiece?
'    The match: I think not.
'       Group 0: I think not.
'          Capture 0: I think not.
'    The match: Instead, it is a nonsensical paragraph.
'       Group 0: Instead, it is a nonsensical paragraph.
'          Capture 0: Instead, it is a nonsensical paragraph.
```

Il criterio di ricerca di espressioni regolari `\b\(?((?>\w+),?\s?)+[\.!?]\)?` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`\(?` | Trova la corrispondenza di una o nessuna parentesi di apertura ("(").
`(?>\w+),?` | Trova la corrispondenza di uno o più caratteri alfanumerici seguiti da una o nessuna virgola. Non eseguire il backtracking quando viene trovata la corrispondenza di caratteri alfanumerici.
`\s?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`((\w+),?\s?)+` | Trova una o più volte la corrispondenza di una combinazione di uno o più caratteri alfanumerici, una o nessuna virgola e uno o nessuno spazio vuoto.
`[\.!?]\)?` | Trova la corrispondenza di qualsiasi dei tre simboli di punteggiatura, seguiti da una o nessuna parentesi di chiusura (")").
 
È anche possibile usare l'elemento inline **(?n)** per disattivare le acquisizioni automatiche. Nell'esempio seguente il criterio di espressione regolare precedente viene modificato in modo da usare l'elemento inline **(?n)** anziché l'opzione [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"(?n)\b\(?((?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//       The match: This is the first sentence.
//          Group 0: This is the first sentence.
//             Capture 0: This is the first sentence.
//       The match: Is it the beginning of a literary masterpiece?
//          Group 0: Is it the beginning of a literary masterpiece?
//             Capture 0: Is it the beginning of a literary masterpiece?
//       The match: I think not.
//          Group 0: I think not.
//             Capture 0: I think not.
//       The match: Instead, it is a nonsensical paragraph.
//          Group 0: Instead, it is a nonsensical paragraph.
//             Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "(?n)\b\(?((?>\w+),?\s?)+[\.!?]\)?"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       The match: This is the first sentence.
'          Group 0: This is the first sentence.
'             Capture 0: This is the first sentence.
'       The match: Is it the beginning of a literary masterpiece?
'          Group 0: Is it the beginning of a literary masterpiece?
'             Capture 0: Is it the beginning of a literary masterpiece?
'       The match: I think not.
'          Group 0: I think not.
'             Capture 0: I think not.
'       The match: Instead, it is a nonsensical paragraph.
'          Group 0: Instead, it is a nonsensical paragraph.
'             Capture 0: Instead, it is a nonsensical paragraph.
```

Infine, si può usare l'elemento di gruppo inline **(?n:)** per disattivare le acquisizioni automatiche gruppo per gruppo. L'esempio di seguito modifica il criterio precedente per disattivare le acquisizioni non denominate nel gruppo esterno, `((?>\w+),?\s?)`. Notare che in questo modo vengono disattivare le acquisizioni non denominate anche nel gruppo interno.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?(?n:(?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("The match: {0}", match.Value);
         int groupCtr = 0;
         foreach (Group group in match.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value);
            groupCtr++;
            int captureCtr = 0;
            foreach (Capture capture in group.Captures)
            {
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value);
               captureCtr++;
            }
         }
      }
   }
}
// The example displays the following output:
//       The match: This is the first sentence.
//          Group 0: This is the first sentence.
//             Capture 0: This is the first sentence.
//       The match: Is it the beginning of a literary masterpiece?
//          Group 0: Is it the beginning of a literary masterpiece?
//             Capture 0: Is it the beginning of a literary masterpiece?
//       The match: I think not.
//          Group 0: I think not.
//             Capture 0: I think not.
//       The match: Instead, it is a nonsensical paragraph.
//          Group 0: Instead, it is a nonsensical paragraph.
//             Capture 0: Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b\(?(?n:(?>\w+),?\s?)+[\.!?]\)?"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("The match: {0}", match.Value)
         Dim groupCtr As Integer = 0
         For Each group As Group In match.Groups
            Console.WriteLine("   Group {0}: {1}", groupCtr, group.Value)
            groupCtr += 1
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               Console.WriteLine("      Capture {0}: {1}", captureCtr, capture.Value)
               captureCtr += 1
            Next
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       The match: This is the first sentence.
'          Group 0: This is the first sentence.
'             Capture 0: This is the first sentence.
'       The match: Is it the beginning of a literary masterpiece?
'          Group 0: Is it the beginning of a literary masterpiece?
'             Capture 0: Is it the beginning of a literary masterpiece?
'       The match: I think not.
'          Group 0: I think not.
'             Capture 0: I think not.
'       The match: Instead, it is a nonsensical paragraph.
'          Group 0: Instead, it is a nonsensical paragraph.
'             Capture 0: Instead, it is a nonsensical paragraph.
```

## <a name="compiled-regular-expressions"></a>Espressioni regolari compilate

Per impostazione predefinita, le espressioni regolari in .NET vengono interpretate. Quando viene creata un'istanza di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) o viene chiamato un metodo [Regex](xref:System.Text.RegularExpressions.Regex) statico, il criterio di espressione regolare viene convertito in un set di codici operativi personalizzati, che vengono usati da un interprete per eseguire l'espressione regolare. Questo comporta un compromesso: il tempo di inizializzazione del motore delle espressioni regolari viene ridotto al minimo, a scapito delle prestazioni in fase di esecuzione.

È possibile usare espressioni regolari compilate anziché interpretate usando l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled). In questo caso, quando un criterio viene passato al motore delle espressioni regolari, viene convertito in un set di codici operativi e quindi in MSIL, che può essere passato direttamente a Common Language Runtime. Le espressioni regolari compilate massimizzano le prestazioni in fase di esecuzione a scapito del tempo di inizializzazione.

> [!NOTE]
> Un'espressione regolare può essere compilata solo fornendo il valore [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) al parametro options di un costruttore di classe [Regex](xref:System.Text.RegularExpressions.Regex) o di un metodo statico dei criteri di ricerca. Non è disponibile come opzione inline. 
 

È possibile usare le espressioni regolari compilate sia nelle chiamate a occorrenze statiche che nelle chiamate a istanze di espressioni regolari. Nelle espressioni regolari statiche, l'opzione [RegexOptions.Compiled](xref:System.Text.RegularExpressions.RegexOptions.Compiled) viene passata al parametro options del metodo dei criteri di ricerca di espressioni regolari. Nelle istanze di espressioni regolari, viene passato al parametro options del costruttore della classe [Regex](xref:System.Text.RegularExpressions.Regex). In entrambi i casi, le prestazioni risultano migliorate. 

Il miglioramento delle prestazioni, tuttavia, si verifica solo in presenza delle condizioni seguenti:

* Un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) che rappresenta una particolare espressione regolare viene usato in più chiamate a metodi dei criteri di ricerca di espressioni regolari.

* L'oggetto [Regex](xref:System.Text.RegularExpressions.Regex) non può uscire dall'ambito, quindi può essere riutilizzato.

* Un'espressione regolare statica viene usata in più chiamate a metodi dei criteri di ricerca di espressioni regolari. (Il miglioramento delle prestazioni è possibile perché le espressioni regolari usate nelle chiamate al metodo statico vengono memorizzate nella cache dal motore delle espressioni regolari.) 

## <a name="ignore-white-space"></a>Ignora spazi vuoti

Per impostazione predefinita, gli spazi vuoti in un criterio di ricerca di espressioni regolari sono significativi. Forzano il motore delle espressioni regolari a trovare una corrispondenza del carattere spazio nella stringa di input. Per questo motivo, l'espressione regolare `"\b\w+\s"` e `"\b\w+ "` sono espressioni regolari pressoché equivalenti. E quando il simbolo di cancelletto (**#**) viene rilevato in un criterio di ricerca di espressioni regolari, viene interpretato come carattere letterale di cui trovare la corrispondenza.

L'opzione [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace), o l'opzione inline **x**, modifica questo comportamento predefinito come indicato di seguito:

* Gli spazi vuoti non di escape nel criterio di ricerca di espressioni regolari vengono ignorati. Per far parte di un criterio di espressione regolare, gli spazi vuoti devono essere preceduti da un carattere di escape (ad esempio **\s** o "**\**").

* Il simbolo di cancelletto (**#**) viene interpretato come l'inizio di un commento anziché come un carattere letterale. Tutto il testo nel criterio di espressione regolare, dal carattere **#** alla fine della stringa, viene interpretato come un commento.

Nei casi seguenti, tuttavia, gli spazi vuoti in un'espressione regolare non vengono ignorati anche se si usa l'opzione [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace): 

* Uno spazio vuoto in una classe di caratteri viene sempre interpretato letteralmente. Ad esempio, il criterio di ricerca di espressioni regolari `[ .,;:]` trova la corrispondenza di qualsiasi spazio vuoto, punto, virgola, punto e virgola o due punti. 

* Gli spazi vuoti non sono consentiti all'interno di un quantificatore tra parentesi, ad esempio **{**_n_**}**, **{**_n_**,}** e **{**_n_**,**_m_**}**. Ad esempio, il criterio di espressione regolare **\d{1. 3}** non è in grado di trovare sequenze di cifre da una a tre cifre perché contiene uno spazio vuoto. 

* Gli spazi vuoti non sono consentiti all'interno di una sequenza di caratteri che introduce un elemento di linguaggio. Ad esempio: 

    * L'elemento language **(?:**_sottoespressione_**)** rappresenta un gruppo di non acquisizione e la porzione **(?:** dell'elemento non può contenere spazi vuoti. Il criterio **(? :**_subexpression_**)** genera un'eccezione [ArgumentException](xref:System.ArgumentException) in fase di esecuzione, perché il motore delle espressioni regolari non può analizzare il criterio e il criterio **(? :**_sottoespressione_**)** non riesce a trovare la corrispondenza di *sottoespressione*.

    * L'elemento language **\p{**_nome_**}**, che rappresenta una categoria Unicode o un blocco denominato, non può includere spazi vuoti nella porzione **\p{** dell'elemento. Se si include uno spazio vuoto, l'elemento genera un'eccezione [ArgumentException](xref:System.ArgumentException) in fase di esecuzione. 

Abilitare questa opzione consente di semplificare espressioni regolari spesso difficili da analizzare e capire. Migliora la leggibilità e rende possibile documentare un'espressione regolare. 

L'esempio di seguito definisce il criterio di ricerca di espressioni regolari seguente:

`\b \(? ( (?>\w+) ,?\s? )+ [\.!?] \)? # Matches an entire sentence`.

Questo criterio è simile a quello definito nella sezione [Solo acquisizioni esplicite](#explicit-captures-only), ad eccezione del fatto che usa l'opzione [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) per ignorare lo spazio vuoto del criterio.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"\b\(?((?>\w+),?\s?)+[\.!?]\)?";

      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       This is the first sentence.
//       Is it the beginning of a literary masterpiece?
//       I think not.
//       Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence."

      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       This is the first sentence.
'       Is it the beginning of a literary masterpiece?
'       I think not.
'       Instead, it is a nonsensical paragraph.
```

L'esempio seguente usa l'opzione inline **(?x)** per ignorare lo spazio vuoto del criterio.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is the first sentence. Is it the beginning " + 
                     "of a literary masterpiece? I think not. Instead, " + 
                     "it is a nonsensical paragraph.";
      string pattern = @"(?x)\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence.";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       This is the first sentence.
//       Is it the beginning of a literary masterpiece?
//       I think not.
//       Instead, it is a nonsensical paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is the first sentence. Is it the beginning " + _
                            "of a literary masterpiece? I think not. Instead, " + _
                            "it is a nonsensical paragraph."
      Dim pattern As String = "(?x)\b \(? ( (?>\w+) ,?\s? )+  [\.!?] \)? # Matches an entire sentence."

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       This is the first sentence.
'       Is it the beginning of a literary masterpiece?
'       I think not.
'       Instead, it is a nonsensical paragraph.
```

## <a name="righttoleft-mode"></a>Modalità da destra a sinistra

Per impostazione predefinita, il motore delle espressioni regolari effettua la ricerca da sinistra a destra. È possibile invertire la direzione della ricerca usando l'opzione [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft). La ricerca inizia automaticamente nella posizione dell'ultimo carattere della stringa. Per i metodi dei criteri di ricerca che includono un parametro della posizione iniziale, ad esempio [Regex.Match(String, Int32)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.Int32)), la posizione iniziale è l'indice della posizione dell'ultimo carattere a destra in corrispondenze del quale ha inizio la ricerca. 

> [!NOTE]
> La modalità da destra a sinistra è disponibile solo specificando il valore [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) al parametro options di un costruttore della classe [Regex](xref:System.Text.RegularExpressions.Regex) o un metodo statico dei criteri di ricerca. Non è disponibile come opzione inline. 
 

L'opzione [RegexOptions.RightToLeft](xref:System.Text.RegularExpressions.RegexOptions.RightToLeft) modifica solo la direzione di ricerca, non interpreta il criterio di espressione regolare da destra a sinistra. Ad esempio, l'espressione regolare `\bb\w+\s` trova le corrispondenze di parole che iniziano con la lettera "b" e sono seguite da uno spazio vuoto. Nell'esempio seguente, la stringa di input è costituita da tre parole che comprendono uno o più caratteri "b". La prima parola inizia con "b", la seconda termina con "b" e la terza contiene due caratteri "b" al centro. Come mostra l'output dell'esempio, solo le prime parole corrispondono al criterio di ricerca di espressioni regolari. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bb\w+\s";
      string input = "builder rob rabble";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.RightToLeft))
         Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);     
   }
}
// The example displays the following output:
//       'builder ' found at position 0.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bb\w+\s"
      Dim input As String = "builder rob rabble"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.RightToLeft)
         Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)     
      Next
   End Sub
End Module
' The example displays the following output:
'       'builder ' found at position 0.
```

Notare anche che l'asserzione lookahead (l'elemento language **(?**=_sottoespressione_**)**) e l'asserzione lookbehind (l'elemento language **(?<**=_sottoespressione_**)**) non cambiano direzione. Le asserzioni lookahead cercano a destra, mentre le asserzioni lookbehind cercano a sinistra. Ad esempio, l'espressione regolare `(?<=\d{1,2}\s)\w+,?\s\d{4}` usa l'asserzione lookbehind per testare una data che precede il nome di un mese. L'espressione regolare trova quindi la corrispondenza di mese e anno. Per informazioni sulle asserzioni lookahead e lookbehind, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "1 May 1917", "June 16, 2003" };
      string pattern = @"(?<=\d{1,2}\s)\w+,?\s\d{4}";

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern, RegexOptions.RightToLeft);
         if (match.Success)
            Console.WriteLine("The date occurs in {0}.", match.Value);
         else
            Console.WriteLine("{0} does not match.", input);
      }
   }
}
// The example displays the following output:
//       The date occurs in May 1917.
//       June 16, 2003 does not match.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "1 May 1917", "June 16, 2003" }
      Dim pattern As String = "(?<=\d{1,2}\s)\w+,?\s\d{4}"

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern, RegexOptions.RightToLeft)
         If match.Success Then
            Console.WriteLine("The date occurs in {0}.", match.Value)
         Else
            Console.WriteLine("{0} does not match.", input)
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'       The date occurs in May 1917.
'       June 16, 2003 does not match.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`(?<=\d{1,2}\s)` | L'inizio della corrispondenza deve essere preceduto da una o due cifre decimali seguite da uno spazio.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`,?` | Trova la corrispondenza di una o nessuna virgola.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`\d{4}` | Trova la corrispondenza con quattro cifre decimali.
 
## <a name="ecmascript-matching-behavior"></a>Comportamento di corrispondenza ECMAScript

Per impostazione predefinita, il motore delle espressioni regolari usa un comportamento canonico nella ricerca di corrispondenza di un criterio di ricerca di espressioni regolari nel testo di input. Si può però istruire il motore delle espressioni regolari in modo che usi il comportamento di corrispondenza ECMAScript specificando l'opzione [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript). 

> [!NOTE]
> Il comportamento conforme a ECMAScript è disponibile solo specificando il valore [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) al parametro options di un costruttore della classe [Regex](xref:System.Text.RegularExpressions.Regex) o un metodo statico dei criteri di ricerca. Non è disponibile come opzione inline. 
 
L'opzione [RegexOptions.ECMAScript](xref:System.Text.RegularExpressions.RegexOptions.ECMAScript) può essere combinata solo con le opzioni [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) e [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline). L'uso di qualsiasi altra opzione in un'espressione regolare genera un'eccezione [ArgumentOutOfRangeException](xref:System.ArgumentOutOfRangeException).

Il comportamento di ECMAScript e quello delle espressioni regolari canoniche differiscono in tre aspetti: sintassi delle classi di caratteri, gruppi di acquisizione autoreferenziali e interpretazione degli ottali rispetto a quella dei backreference. 

* Sintassi delle classi di caratteri. Poiché le espressioni regolari canoniche supportano Unicode a differenza di ECMAScript, le classi di caratteri in ECMAScript hanno una sintassi più limitata e alcuni elementi di linguaggio delle classi di caratteri hanno un significato diverso. Ad esempio, ECMAScript non supporta elementi language come la categoria Unicode o gli elementi di blocco *\p* e **\P**. Analogamente, l'elemento **\w**, che trova la corrispondenza di un carattere alfanumerico, è equivalente alla classe di caratteri **[a-zA-Z_0-9]** quando si usa ECMAScript e a **[\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]** quando si usa il comportamento canonico. Per altre informazioni, vedere [Classi di caratteri nelle espressioni regolari](classes.md).

  L'esempio seguente illustra le differenze tra i criteri di ricerca canonici ed ECMAScript. Definisce un'espressione regolare, `\b(\w+\s*)+`, che trova la corrispondenza di parole seguite da spazi vuoti. L'input è costituito da due stringhe, una che usa il set di caratteri latini e l'altra che usa il set di caratteri cirillici. Come indica l'output, la chiamata al metodo [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) che usa i criteri di ricerca ECMAScript non riesce a trovare la corrispondenza delle parole in cirillico, mentre la chiamata al metodo che usa i criteri di ricerca canonici trova la corrispondenza. 

  ```csharp
  using System;
  using System.Text.RegularExpressions;
  
  public class Example
  {
     public static void Main()
     {
        string[] values = { "целый мир", "the whole world" };
        string pattern = @"\b(\w+\s*)+";
        foreach (var value in values)
        {
           Console.Write("Canonical matching: ");
           if (Regex.IsMatch(value, pattern))
              Console.WriteLine("'{0}' matches the pattern.", value);
           else
              Console.WriteLine("{0} does not match the pattern.", value);
  
           Console.Write("ECMAScript matching: ");
           if (Regex.IsMatch(value, pattern, RegexOptions.ECMAScript))
              Console.WriteLine("'{0}' matches the pattern.", value);
           else
              Console.WriteLine("{0} does not match the pattern.", value);
           Console.WriteLine();
        }
     }
  }
  // The example displays the following output:
  //       Canonical matching: 'целый мир' matches the pattern.
  //       ECMAScript matching: целый мир does not match the pattern.
  //       
  //       Canonical matching: 'the whole world' matches the pattern.
  //       ECMAScript matching: 'the whole world' matches the pattern.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim values() As String = { "целый мир", "the whole world" }
        Dim pattern As String = "\b(\w+\s*)+"
        For Each value In values
           Console.Write("Canonical matching: ")
           If Regex.IsMatch(value, pattern)
              Console.WriteLine("'{0}' matches the pattern.", value)
           Else
              Console.WriteLine("{0} does not match the pattern.", value)
           End If

           Console.Write("ECMAScript matching: ")
           If Regex.IsMatch(value, pattern, RegexOptions.ECMAScript)
              Console.WriteLine("'{0}' matches the pattern.", value)
           Else
              Console.WriteLine("{0} does not match the pattern.", value)
           End If
           Console.WriteLine()
        Next
     End Sub
  End Module
  ' The example displays the following output:
  '       Canonical matching: 'целый мир' matches the pattern.
  '       ECMAScript matching: целый мир does not match the pattern.
  '       
  '       Canonical matching: 'the whole world' matches the pattern.
  '       ECMAScript matching: 'the whole world' matches the pattern.
  ```

* Gruppi di acquisizione autoreferenziali. È necessario aggiornare una classe di acquisizione di espressioni regolari con un backreference autoreferenziale ogni volta che viene eseguita un'iterazione dell'acquisizione. Come mostra l'esempio seguente, questa funzionalità consente all'espressione regolare `((a+)(\1) ?)+` di trovare la corrispondenza della stringa di input " aa aaaa aaaaaa " quando si usa ECMAScript, ma non quando si usano i criteri di ricerca canonici. 

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     static string pattern;
  
     public static void Main()
     {
        string input = "aa aaaa aaaaaa "; 
        pattern = @"((a+)(\1) ?)+";
  
        // Match input using canonical matching.
        AnalyzeMatch(Regex.Match(input, pattern));

        // Match input using ECMAScript.
        AnalyzeMatch(Regex.Match(input, pattern, RegexOptions.ECMAScript));
     }   

     private static void AnalyzeMatch(Match m)
     {
        if (m.Success)
        {
           Console.WriteLine("'{0}' matches {1} at position {2}.",  
                             pattern, m.Value, m.Index);
           int grpCtr = 0;
           foreach (Group grp in m.Groups)
           {
              Console.WriteLine("   {0}: '{1}'", grpCtr, grp.Value);
              grpCtr++;
              int capCtr = 0;
              foreach (Capture cap in grp.Captures)
              {
                 Console.WriteLine("      {0}: '{1}'", capCtr, cap.Value);
                 capCtr++;
              }
           }
        }
        else
        {
           Console.WriteLine("No match found.");
        }   
        Console.WriteLine();
     }
  }
  // The example displays the following output:
  //    No match found.
  //    
  //    '((a+)(\1) ?)+' matches aa aaaa aaaaaa  at position 0.
  //       0: 'aa aaaa aaaaaa '
  //          0: 'aa aaaa aaaaaa '
  //       1: 'aaaaaa '
  //          0: 'aa '
  //          1: 'aaaa '
  //          2: 'aaaaaa '
  //       2: 'aa'
  //          0: 'aa'
  //          1: 'aa'
  //          2: 'aa'
  //       3: 'aaaa '
  //          0: ''
  //          1: 'aa '
  //          2: 'aaaa '
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Dim pattern As String

     Public Sub Main()
        Dim input As String = "aa aaaa aaaaaa " 
        pattern = "((a+)(\1) ?)+"
  
        ' Match input using canonical matching.
        AnalyzeMatch(Regex.Match(input, pattern))

        ' Match input using ECMAScript.
        AnalyzeMatch(Regex.Match(input, pattern, RegexOptions.ECMAScript))
     End Sub   

     Private Sub AnalyzeMatch(m As Match)
        If m.Success
           Console.WriteLine("'{0}' matches {1} at position {2}.", _ 
                             pattern, m.Value, m.Index)
           Dim grpCtr As Integer = 0
           For Each grp As Group In m.Groups
              Console.WriteLine("   {0}: '{1}'", grpCtr, grp.Value)
              grpCtr += 1
              Dim capCtr As Integer = 0
              For Each cap As Capture In grp.Captures
                 Console.WriteLine("      {0}: '{1}'", capCtr, cap.Value)
                 capCtr += 1
              Next
           Next
        Else
           Console.WriteLine("No match found.")
        End If   
        Console.WriteLine()
     End Sub
  End Module
  ' The example displays the following output:
  '    No match found.
  '    
  '    '((a+)(\1) ?)+' matches aa aaaa aaaaaa  at position 0.
  '       0: 'aa aaaa aaaaaa '
  '          0: 'aa aaaa aaaaaa '
  '       1: 'aaaaaa '
  '          0: 'aa '
  '          1: 'aaaa '  
  '          2: 'aaaaaa '
  '       2: 'aa'
  '          0: 'aa'
  '          1: 'aa'
  '          2: 'aa'
  '       3: 'aaaa '
  '          0: ''
  '          1: 'aa '
  '          2: 'aaaa '
  ``

  The regular expression is defined as shown in the following table.

Pattern | Description
------- | ----------- 
`(a+)` | Match the letter "a" one or more times. This is the second capturing group.
`(\1)` | Match the substring captured by the first capturing group. This is the third capturing group.
`?` | Match zero or one space characters.
`((a+)(\1) ?)+` | Match the pattern of one or more "a" characters followed by a string that matches the first capturing group followed by zero or one space characters one or more times. This is the first capturing group.
  
* Resolution of ambiguities between octal escapes and backreferences. The following table summarizes the differences in octal versus backreference interpretation by canonical and ECMAScript regular expressions.

Regular expression | Canonical behavior | ECMAScript behavior
------------------ | ------------------ | ------------------- 
`\0` followed by 0 to 2 octal digits | Interpret as an octal. For example, `\044` is always interpreted as an octal value and means "**$**". | Same behavior.
**\** followed by a digit from 1 to 9, followed by no additional decimal digits | Interpret as a backreference. For example, \9 always means backreference 9, even if a ninth capturing group does not exist. If the capturing group does not exist, the regular expression parser throws an [ArgumentException](xref:System.ArgumentException). | If a single decimal digit capturing group exists, backreference to that digit. Otherwise, interpret the value as a literal.
**\** followed by a digit from 1 to 9, followed by additional decimal digits | Interpret the digits as a decimal value. If that capturing group exists, interpret the expression as a backreference. Otherwise, interpret the leading octal digits up to octal 377; that is, consider only the low 8 bits of the value. Interpret the remaining digits as literals. For example, in the expression `\3000`, if capturing group 300 exists, interpret as backreference 300; if capturing group 300 does not exist, interpret as octal 300 followed by 0. | Interpret as a backreference by converting as many digits as possible to a decimal value that can refer to a capture. If no digits can be converted, interpret as an octal by using the leading octal digits up to octal 377; interpret the remaining digits as literals.
 
## Comparison using the invariant culture

By default, when the regular expression engine performs case-insensitive comparisons, it uses the casing conventions of the current culture to determine equivalent uppercase and lowercase characters. 

However, this behavior is undesirable for some types of comparisons, particularly when comparing user input to the names of system resources, such as passwords, files, or URLs. The following example illustrates such as scenario. The code is intended to block access to any resource whose URL is prefaced with **FILE://**. The regular expression attempts a case-insensitive match with the string by using the regular expression `$FILE://`. However, when the current system culture is tr-TR (Turkish-Turkey), "I" is not the uppercase equivalent of "i". As a result, the call to the [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) method returns `false`, and access to the file is allowed. 

```csharp
CultureInfo defaultCulture = Thread.CurrentThread.CurrentCulture;
Thread.CurrentThread.CurrentCulture = new CultureInfo("tr-TR");

string input = "file://c:/Documents.MyReport.doc";
string pattern = "FILE://";

Console.WriteLine("Culture-sensitive matching ({0} culture)...", 
                  Thread.CurrentThread.CurrentCulture.Name);
if (Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("URLs that access files are not allowed.");      
else
   Console.WriteLine("Access to {0} is allowed.", input);

Thread.CurrentThread.CurrentCulture = defaultCulture;
// The example displays the following output:
//       Culture-sensitive matching (tr-TR culture)...
//       Access to file://c:/Documents.MyReport.doc is allowed.
```

```vb
Dim defaultCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
Thread.CurrentThread.CurrentCulture = New CultureInfo("tr-TR")

Dim input As String = "file://c:/Documents.MyReport.doc"
Dim pattern As String = "$FILE://"

Console.WriteLine("Culture-sensitive matching ({0} culture)...", _
                  Thread.CurrentThread.CurrentCulture.Name)
If Regex.IsMatch(input, pattern, RegexOptions.IgnoreCase) Then
   Console.WriteLine("URLs that access files are not allowed.")      
Else
   Console.WriteLine("Access to {0} is allowed.", input)
End If

Thread.CurrentThread.CurrentCulture = defaultCulture
' The example displays the following output:
'       Culture-sensitive matching (tr-TR culture)...
'       Access to file://c:/Documents.MyReport.doc is allowed.
```

> [!NOTE]
>   Per altre informazioni sui confronti di stringhe che supportano la distinzione tra maiuscole e minuscole e che usano la lingua inglese, vedere [Procedure consigliate per l'uso di stringhe](best-practices.md).
 
Anziché usare i confronti senza distinzione fra maiuscole e minuscole delle impostazioni cultura correnti, è possibile specificare l'opzione [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) per ignorare le differenze culturali di lingua e usare le convenzioni della lingua inglese.

> [!NOTE]
> Il confronto usando la lingua inglese è disponibile solo specificando il valore [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant) per il parametro options di un costruttore della classe [Regex](xref:System.Text.RegularExpressions.Regex) o un metodo statico dei criteri di ricerca. Non è disponibile come opzione inline. 
 
L'esempio che segue è identico al precedente, tranne per il fatto che il metodo statico [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con opzioni che includono [RegexOptions.CultureInvariant](xref:System.Text.RegularExpressions.RegexOptions.CultureInvariant). Anche quando le impostazioni cultura correnti sono quelle del turco (Turchia), il motore delle espressioni regolari consente di individuare la corrispondenza tra "FILE" e "file" e di bloccare l'accesso alla risorsa del file. 

```csharp
CultureInfo defaultCulture = Thread.CurrentThread.CurrentCulture;
Thread.CurrentThread.CurrentCulture = new CultureInfo("tr-TR");

string input = "file://c:/Documents.MyReport.doc";
string pattern = "FILE://";

Console.WriteLine("Culture-insensitive matching...");
if (Regex.IsMatch(input, pattern, 
                  RegexOptions.IgnoreCase | RegexOptions.CultureInvariant)) 
   Console.WriteLine("URLs that access files are not allowed.");
else
   Console.WriteLine("Access to {0} is allowed.", input);

Thread.CurrentThread.CurrentCulture = defaultCulture;
// The example displays the following output:
//       Culture-insensitive matching...
//       URLs that access files are not allowed.
```

```vb
Dim defaultCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
Thread.CurrentThread.CurrentCulture = New CultureInfo("tr-TR")

Dim input As String = "file://c:/Documents.MyReport.doc"
Dim pattern As String = "$FILE://"

Console.WriteLine("Culture-insensitive matching...")
If Regex.IsMatch(input, pattern, _
               RegexOptions.IgnoreCase Or RegexOptions.CultureInvariant) Then
   Console.WriteLine("URLs that access files are not allowed.")      
Else
   Console.WriteLine("Access to {0} is allowed.", input)
End If
Thread.CurrentThread.CurrentCulture = defaultCulture
' The example displays the following output:
'        Culture-insensitive matching...
'        URLs that access files are not allowed.
```

## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)




<!--HONumber=Nov16_HO1-->


