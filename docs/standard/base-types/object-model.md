---
title: Modello a oggetti delle espressioni regolari
description: Modello a oggetti delle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a1e611ec-c6a2-48c6-9c52-0ed845787621
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 4e8744c6c7a42c3803bf9716a3ae271b7284be3d
ms.lasthandoff: 03/02/2017

---

# <a name="the-regular-expression-object-model"></a>Modello a oggetti delle espressioni regolari

In questo argomento viene illustrato il modello a oggetti usato con le espressioni regolari di .NET. Include le sezioni seguenti:

* [Motore delle espressioni regolari](#the-regular-expression-engine)

* [Oggetti MatchCollection e Match](#the-matchcollection-and-match-objects)

* [Raccolta Group](#the-group-collection)

* [Gruppo acquisito](#the-captured-group)

* [Raccolta Capture](#the-capture-collection)

* [Singola acquisizione](#the-individual-capture)

## <a name="the-regular-expression-engine"></a>Motore delle espressioni regolari

Il motore delle espressioni regolari di .NET è rappresentato dalla classe [Regex](xref:System.Text.RegularExpressions.Regex). Il motore delle espressioni regolari è responsabile dell'analisi e della compilazione di un'espressione regolare e dell'esecuzione di operazioni che associano il criterio di espressione regolare a una stringa di input. Il motore è il componente centrale del modello a oggetti delle espressioni regolari di .NET.

È possibile usare il motore delle espressioni regolari in uno dei due modi seguenti:

* Tramite la chiamata di metodi statici della classe [Regex](xref:System.Text.RegularExpressions.Regex). I parametri del metodo includono la stringa di input e il criterio di espressione regolare. Il motore delle espressioni regolari memorizza nella cache le espressioni regolari usate nelle chiamate del metodo statico. Le chiamate ripetute a metodi di espressione regolare che usano la stessa espressione regolare offrono quindi prestazioni relativamente buone.

* Tramite la creazione di istanze di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex), passando un'espressione regolare al costruttore di classe. In questo caso l'oggetto [Regex](xref:System.Text.RegularExpressions.Regex) è non modificabile (sola lettura) e rappresenta un motore delle espressioni regolari strettamente associato a una singola espressione regolare. Poiché le espressioni regolari usate dalle istanze di Regex non sono memorizzate nella cache, è consigliabile non creare più volte istanze di un oggetto [Regex](xref:System.Text.RegularExpressions.Regex) con la stessa espressione regolare.

È possibile chiamare i metodi della classe [Regex](xref:System.Text.RegularExpressions.Regex) per eseguire le operazioni seguenti: 

* Determinare se una stringa corrisponde a un criterio di espressione regolare.

* Estrarre una singola corrispondenza o la prima corrispondenza.

* Estrarre tutte le corrispondenze.

* Sostituire una sottostringa con corrispondenza.

* Suddividere una singola stringa in una matrice di stringhe.

Queste operazioni sono descritte nelle sezioni seguenti.

### <a name="matching-a-regular-expression-pattern"></a>Corrispondenza con un criterio di espressione regolare

Il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) restituisce `true` se la stringa corrisponde al criterio. In caso contrario, restituisce `false`. Il metodo [IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) è usato spesso per convalidare l'input di stringa. Ad esempio, il codice seguente assicura che una stringa corrisponda a un numero di previdenza sociale negli Stati Uniti.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] values = { "111-22-3333", "111-2-3333"};
      string pattern = @"^\d{3}-\d{2}-\d{4}$";
      foreach (string value in values) {
         if (Regex.IsMatch(value, pattern))
            Console.WriteLine("{0} is a valid SSN.", value);
         else   
            Console.WriteLine("{0}: Invalid", value);
      }
   }
}
// The example displays the following output:
//       111-22-3333 is a valid SSN.
//       111-2-3333: Invalid
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim values() As String = { "111-22-3333", "111-2-3333"}
      Dim pattern As String = "^\d{3}-\d{2}-\d{4}$"
      For Each value As String In values
         If Regex.IsMatch(value, pattern) Then
            Console.WriteLine("{0} is a valid SSN.", value)
         Else   
            Console.WriteLine("{0}: Invalid", value)
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       111-22-3333 is a valid SSN.
'       111-2-3333: Invalid
```

Il criterio di ricerca di espressioni regolari `^\d{3}-\d{2}-\d{4}$` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Trova la corrispondenza con l'inizio della stringa di input.
`\d{3}` | Trova la corrispondenza con tre cifre decimali.
`-` | Trova la corrispondenza con un segno meno.
`\d{2}` | Trova la corrispondenza con due cifre decimali.
`-` | Trova la corrispondenza con un segno meno.
`\d{4}` | Trova la corrispondenza con quattro cifre decimali.
`$` | Trova la corrispondenza con la fine della stringa di input.
 
### <a name="extracting-a-single-match-or-the-first-match"></a>Estrazione di una singola corrispondenza o della prima corrispondenza

Il metodo [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) restituisce un oggetto [Match](xref:System.Text.RegularExpressions.Match) che contiene informazioni sulla prima sottostringa corrispondente a un criterio di espressioni regolari. Se la proprietà `Match.Success` restituisce `true`, indicando che è stata rilevata una corrispondenza, sarà possibile ottenere informazioni sulle corrispondenze successive chiamando il metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch). Le chiamate ai metodi possono continuare finché la proprietà `Match.Success` non restituisce `false`. Ad esempio, il codice seguente usa il metodo [Regex.Match(String, String)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String)) per trovare la prima occorrenza di una parola duplicata in una stringa. Chiama quindi il metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) per trovare eventuali occorrenze aggiuntive. L'esempio esamina la proprietà `Match.Success` dopo ogni chiamata al metodo, per determinare se la corrispondenza corrente è riuscita e se deve essere eseguita una chiamata al metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is a a farm that that raises dairy cattle."; 
      string pattern = @"\b(\w+)\W+(\1)\b";
      Match match = Regex.Match(input, pattern);
      while (match.Success)
      {
         Console.WriteLine("Duplicate '{0}' found at position {1}.",  
                           match.Groups[1].Value, match.Groups[2].Index);
         match = match.NextMatch();
      }                       
   }
}
// The example displays the following output:
//       Duplicate 'a' found at position 10.
//       Duplicate 'that' found at position 22.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is a a farm that that raises dairy cattle." 
      Dim pattern As String = "\b(\w+)\W+(\1)\b"
      Dim match As Match = Regex.Match(input, pattern)
      Do While match.Success
         Console.WriteLine("Duplicate '{0}' found at position {1}.", _ 
                           match.Groups(1).Value, match.Groups(2).Index)
         match = match.NextMatch()
      Loop                       
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'a' found at position 10.
'       Duplicate 'that' found at position 22.
```

Il criterio di ricerca di espressioni regolari `\b(\w+)\W+(\1)\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\W+` | Trova la corrispondenza di uno o più caratteri non alfanumerici.
`(\1)` | Trova la corrispondenza con la prima stringa acquisita. Equivale al secondo gruppo di acquisizione. 
`\b` | Termina la corrispondenza sul confine di parola.
 
### <a name="extracting-all-matches"></a>Estrazione di tutte le corrispondenze

Il metodo [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) restituisce un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) che contiene informazioni su tutte le corrispondenze rilevate dal motore delle espressioni regolari nella stringa di input. Ad esempio, è possibile riscrivere l'esempio precedente per chiamare il metodo [Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) invece dei metodi [Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) e [NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch).

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "This is a a farm that that raises dairy cattle."; 
      string pattern = @"\b(\w+)\W+(\1)\b";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Duplicate '{0}' found at position {1}.",  
                           match.Groups[1].Value, match.Groups[2].Index);
   }
}
// The example displays the following output:
//       Duplicate 'a' found at position 10.
//       Duplicate 'that' found at position 22.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "This is a a farm that that raises dairy cattle." 
      Dim pattern As String = "\b(\w+)\W+(\1)\b"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Duplicate '{0}' found at position {1}.", _ 
                           match.Groups(1).Value, match.Groups(2).Index)
      Next                       
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'a' found at position 10.
'       Duplicate 'that' found at position 22.
```

### <a name="replacing-a-matched-substring"></a>Sostituzione di una sottostringa con corrispondenza

Il metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) sostituisce ogni sottostringa corrispondente al criterio di espressione regolare con una stringa specificata o con un criterio di espressioni regolari e restituisce l'intera stringa di input con le sostituzioni. Ad esempio, il codice riportato di seguito aggiunge il simbolo di valuta degli Stati Uniti prima di un numero decimale in una stringa.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\d+\.\d{2}\b";
      string replacement = "$$$&"; 
      string input = "Total Cost: 103.64";
      Console.WriteLine(Regex.Replace(input, pattern, replacement));     
   }
}
// The example displays the following output:
//       Total Cost: $103.64
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\d+\.\d{2}\b"
      Dim replacement As String = "$$$&" 
      Dim input As String = "Total Cost: 103.64"
      Console.WriteLine(Regex.Replace(input, pattern, replacement))     
   End Sub
End Module
' The example displays the following output:
'       Total Cost: $103.64
```

Il criterio di ricerca di espressioni regolari `\b\d+\.\d{2}\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
`\.` | Trova la corrispondenza con un punto.
`\d{2}` | Trova la corrispondenza con due cifre decimali.
`\b` | Termina la corrispondenza sul confine di parola.
 
Il modello di sostituzione `$$$&` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Stringa di sostituzione
------- | ------------------ 
`$$` | Carattere del simbolo di dollaro (**$**).
`$&` | Intera stringa corrispondente.
 
### <a name="splitting-a-single-string-into-an-array-of-strings"></a>Suddivisione di una singola stringa in una matrice di stringhe

Il metodo [Regex.Split](xref:System.Text.RegularExpressions.Regex.Split(System.String)) divide la stringa di input nelle posizioni definite da una corrispondenza di espressione regolare. Ad esempio, il codice seguente inserisce gli elementi di un elenco numerato in una matrice di stringhe.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "1. Eggs 2. Bread 3. Milk 4. Coffee 5. Tea";
      string pattern = @"\b\d{1,2}\.\s";
      foreach (string item in Regex.Split(input, pattern))
      {
         if (! String.IsNullOrEmpty(item))
            Console.WriteLine(item);
      }      
   }
}
// The example displays the following output:
//       Eggs
//       Bread
//       Milk
//       Coffee
//       Tea
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "1. Eggs 2. Bread 3. Milk 4. Coffee 5. Tea"
      Dim pattern As String = "\b\d{1,2}\.\s"
      For Each item As String In Regex.Split(input, pattern)
         If Not String.IsNullOrEmpty(item) Then
            Console.WriteLine(item)
         End If
      Next      
   End Sub
End Module
' The example displays the following output:
'       Eggs
'       Bread
'       Milk
'       Coffee
'       Tea
```

Il criterio di ricerca di espressioni regolari `\b\d{1,2}\.\s` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\d{1,2}` | Trova la corrispondenza con una o due cifre decimali.
`\.` | Trova la corrispondenza con un punto.
`\s` | Trova la corrispondenza con uno spazio vuoto.
 
## <a name="the-matchcollection-and-match-objects"></a>Oggetti MatchCollection e Match

I metodi [Regex](xref:System.Text.RegularExpressions.Regex) restituiscono due oggetti che fanno parte del modello a oggetti delle espressioni regolari, ovvero l'oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) e l'oggetto [Match](xref:System.Text.RegularExpressions.Match). 

### <a name="the-match-collection"></a>Raccolta Match

Il metodo [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) restituisce un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) contenente gli oggetti [Match](xref:System.Text.RegularExpressions.Match) che rappresentano tutte le corrispondenze trovate dal motore delle espressioni regolari, in base all'ordine in cui si trovano nella stringa di input. Se non ci sono corrispondenze, il metodo restituisce un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) che contiene l'oggetto [Match](xref:System.Text.RegularExpressions.Match) senza membri. La proprietà [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) `Item` consente di accedere a singoli membri della raccolta in base all'indice, da zero al valore della proprietà [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count) meno uno. 'Item' è l'indicizzatore della raccolta (in C#) e la proprietà predefinita (in Visual Basic).

Per impostazione predefinita, la chiamata al metodo [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) usa una valutazione lenta per il popolamento dell'oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection). L'accesso alle proprietà che necessitano di una raccolta completamente popolata, ad esempio le proprietà [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count) e `Item`, potrebbe ridurre le prestazioni. Per questo motivo, è consigliabile accedere alla raccolta usando l'oggetto [IEnumerator](xref:System.Collections.IEnumerator) restituito dal metodo [MatchCollection.GetEnumerator](xref:System.Text.RegularExpressions.MatchCollection.GetEnumerator). I singoli linguaggi offrono costrutti, ad esempio `foreach` in C# e 'For Each' in Visual Basic, che eseguono il wrapping dell'interfaccia IEnumerator](xref:System.Collections.IEnumerator) della raccolta.

L'esempio seguente usa il metodo [Regex.Matches(String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) per popolare un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) con tutte le corrispondenze trovate in una stringa di input. L'esempio enumera la raccolta, copia le corrispondenze a una matrice di stringhe e registra le posizioni dei caratteri in una matrice di valori di tipo Integer.

```csharp
using System;
using System.Collections.Generic;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
       MatchCollection matches;
       List<string> results = new List<string>();
       List<int> matchposition = new List<int>();

       // Create a new Regex object and define the regular expression.
       Regex r = new Regex("abc");
       // Use the Matches method to find all matches in the input string.
       matches = r.Matches("123abc4abcd");
       // Enumerate the collection to retrieve all matches and positions.
       foreach (Match match in matches)
       {
          // Add the match string to the string array.
           results.Add(match.Value);
           // Record the character position where the match was found.
           matchposition.Add(match.Index);
       }
       // List the results.
       for (int ctr = 0; ctr < results.Count; ctr++)
         Console.WriteLine("'{0}' found at position {1}.", 
                           results[ctr], matchposition[ctr]);  
   }
}
// The example displays the following output:
//       'abc' found at position 3.
//       'abc' found at position 7.
```

```vb
Imports System.Collections.Generic
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
       Dim matches As MatchCollection
       Dim results As New List(Of String)
       Dim matchposition As New List(Of Integer)

       ' Create a new Regex object and define the regular expression.
       Dim r As New Regex("abc")
       ' Use the Matches method to find all matches in the input string.
       matches = r.Matches("123abc4abcd")
       ' Enumerate the collection to retrieve all matches and positions.
       For Each match As Match In matches
          ' Add the match string to the string array.
           results.Add(match.Value)
           ' Record the character position where the match was found.
           matchposition.Add(match.Index)
       Next
       ' List the results.
       For ctr As Integer = 0 To results.Count - 1
         Console.WriteLine("'{0}' found at position {1}.", _
                           results(ctr), matchposition(ctr))  
       Next
   End Sub
End Module
' The example displays the following output:
'       'abc' found at position 3.
'       'abc' found at position 7.
```

### <a name="the-match"></a>Oggetto Match

La classe [Match](xref:System.Text.RegularExpressions.Match) rappresenta il risultato della corrispondenza di una singola espressione regolare. È possibile accedere agli oggetti [Match](xref:System.Text.RegularExpressions.Match) in due modi:

* Tramite il recupero dall'oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) restituito dal metodo Regex.Matches. Per recuperare i singoli oggetti [Match](xref:System.Text.RegularExpressions.Match), eseguire l'iterazione della raccolta usando il costrutto `foreach` (in C#) o `For Each...Next` (in Visual Basic) oppure usare la proprietà [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) `Item` per recuperare un oggetto [Match](xref:System.Text.RegularExpressions.Match) specifico in base all'indice o al nome. È anche possibile recuperare singoli oggetti [Match](xref:System.Text.RegularExpressions.Match) dalla raccolta eseguendo l'iterazione della raccolta in base all'indice, da zero al numero di oggetti della raccolta meno uno. Questo metodo, tuttavia, non consente di avvalersi della valutazione lenta, poiché accede alla proprietà [MatchCollection.Count](xref:System.Text.RegularExpressions.MatchCollection.Count). 

  L'esempio seguente recupera singoli oggetti [Match](xref:System.Text.RegularExpressions.Match) da un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) eseguendo l'iterazione della raccolta tramite il costrutto `foreach`. L'espressione regolare corrisponde semplicemente alla stringa "abc" nella stringa di input.

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "abc";
        string input = "abc123abc456abc789";
        foreach (Match match in Regex.Matches(input, pattern))
           Console.WriteLine("{0} found at position {1}.", 
                             match.Value, match.Index);
     }
  }
  // The example displays the following output:
  //       abc found at position 0.
  //       abc found at position 6.
  //       abc found at position 12.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "abc"
        Dim input As String = "abc123abc456abc789"
        For Each match As Match In Regex.Matches(input, pattern)
           Console.WriteLine("{0} found at position {1}.", _
                             match.Value, match.Index)
        Next                     
     End Sub
  End Module
  ' The example displays the following output:
  '       abc found at position 0.
  '       abc found at position 6.
  '       abc found at position 12.
  ```

* Tramite la chiamata al metodo [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)), che restituisce un oggetto [Match](xref:System.Text.RegularExpressions.Match) che rappresenta la prima corrispondenza in una stringa o in una parte di una stringa. È possibile stabilire se la corrispondenza è stata rilevata tramite il recupero del valore della proprietà `Match.Success`. Per recuperare gli oggetti [Match](xref:System.Text.RegularExpressions.Match) che rappresentano corrispondenze successive, chiamare ripetutamente il metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch), fino a quando la proprietà `Success` dell'oggetto [Match](xref:System.Text.RegularExpressions.Match) restituito non sarà `false`. 

  L'esempio seguente usa i metodi [Regex.Match(String, String)](xref:System.Text.RegularExpressions.Regex.Match(System.String,System.String)) e [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) per la corrispondenza con la stringa "abc" nella stringa di input.

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "abc";
        string input = "abc123abc456abc789";
        Match match = Regex.Match(input, pattern);
        while (match.Success)
        {
           Console.WriteLine("{0} found at position {1}.", 
                             match.Value, match.Index);
           match = match.NextMatch();                  
        }                     
     }
  }
  // The example displays the following output:
  //       abc found at position 0.
  //       abc found at position 6.
  //       abc found at position 12.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "abc"
        Dim input As String = "abc123abc456abc789"
        Dim match As Match = Regex.Match(input, pattern)
        Do While match.Success
           Console.WriteLine("{0} found at position {1}.", _
                             match.Value, match.Index)
           match = match.NextMatch()                  
        Loop                     
     End Sub
  End Module
  ' The example displays the following output:
  '       abc found at position 0.
  '       abc found at position 6.
  '       abc found at position 12.
  ```

Due proprietà della classe [Match](xref:System.Text.RegularExpressions.Match) restituiscono oggetti della raccolta:

* La proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) restituisce un oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) che contiene informazioni sulle sottostringhe che corrispondono a gruppi di acquisizione nel criterio di espressioni regolari. 

* La proprietà `Match.Captures` restituisce un oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) di uso limitato. La raccolta non è popolata per un oggetto [Match](xref:System.Text.RegularExpressions.Match) la cui proprietà `Success` è `false`. In caso contrario, contiene un singolo oggetto [Capture](xref:System.Text.RegularExpressions.Capture) che ha le stesse informazioni dell'oggetto [Match](xref:System.Text.RegularExpressions.Match). 

Per altre informazioni su questi oggetti, vedere le sezioni [Raccolta Group](#the-group-collection) e [Raccolta Capture](#the-capture-collection) più avanti in questo argomento.

Due proprietà aggiuntive della classe [Match](xref:System.Text.RegularExpressions.Match) offrono informazioni sulla corrispondenza. La proprietà `Match.Value` restituisce la sottostringa nella stringa di input corrispondente al criterio di espressione regolare. La proprietà `Match.Index` restituisce la posizione di inizio a base zero della stringa con corrispondenza nella stringa di input.

La classe [Match](xref:System.Text.RegularExpressions.Match) ha anche due metodi di criteri di ricerca:

* Il metodo [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch) trova la corrispondenza dopo la corrispondenza rappresentata dall'oggetto [Match](xref:System.Text.RegularExpressions.Match) corrente e restituisce un oggetto [Match](xref:System.Text.RegularExpressions.Match) che rappresenta la corrispondenza.

* Il metodo [Match.Result](xref:System.Text.RegularExpressions.Match.NextMatch) esegue un'operazione di sostituzione specificata nella stringa corrispondente e restituisce il risultato. 


L'esempio seguente usa il metodo [Match.Result](xref:System.Text.RegularExpressions.Match.NextMatch) per aggiungere un simbolo **$** e uno spazio davanti a tutti i numeri che includono due cifre frazionarie. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\d+(,\d{3})*\.\d{2}\b";
      string input = "16.32\n194.03\n1,903,672.08"; 

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Result("$$ $&"));
   }
}
// The example displays the following output:
//       $ 16.32
//       $ 194.03
//       $ 1,903,672.08
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\d+(,\d{3})*\.\d{2}\b"
      Dim input As String = "16.32" + vbCrLf + "194.03" + vbCrLf + "1,903,672.08" 

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Result("$$ $&"))
      Next
   End Sub
End Module
' The example displays the following output:
'       $ 16.32
'       $ 194.03
'       $ 1,903,672.08
```

Il criterio di ricerca di espressioni regolari `\b\d+(,\d{3})*\.\d{2}\b` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
`(,\d{3})*` | Trova la corrispondenza con zero o più occorrenze di una virgola seguita da tre cifre decimali.
`\.` | Trova la corrispondenza con il carattere del separatore decimale.
'\d{2} | Trova la corrispondenza con due cifre decimali.
`\b` | Termina la corrispondenza sul confine di parola.
 
Il criterio di sostituzione **$$ $&** indica che la stringa corrispondente deve essere sostituita da un simbolo di dollaro (**$**) (criterio `$$`), da uno spazio e dal valore della corrispondenza (criterio `$&`).

## <a name="the-group-collection"></a>Raccolta Group

La proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) restituisce un oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) che contiene oggetti [Group](xref:System.Text.RegularExpressions.Group) che rappresentano i gruppi acquisiti in una singola corrispondenza. Il primo oggetto [Group](xref:System.Text.RegularExpressions.Group) della raccolta (in corrispondenza dell'indice 0) rappresenta l'intera corrispondenza. Ogni oggetto successivo rappresenta i risultati di un singolo gruppo di acquisizione. 

È possibile recuperare singoli oggetti [Group](xref:System.Text.RegularExpressions.Group) nella raccolta usando la proprietà [GroupCollection.Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)). I gruppi senza nome possono essere recuperati in base alla relativa posizione ordinale nella raccolta e i gruppi con nome possono essere recuperati in base al nome o alla posizione ordinale. Le acquisizioni senza nome compaiono per prime nella raccolta e sono indicizzate da sinistra a destra nell'ordine di visualizzazione nel criterio di espressione regolare. Le acquisizioni con nome sono indicizzate dopo le acquisizioni senza nome, da sinistra a destra nell'ordine di visualizzazione nel criterio di espressione regolare. Per determinare i gruppi numerati disponibili nella raccolta restituita per un metodo dei criteri di ricerca di espressioni regolari, è possibile chiamare il metodo [Regex.GetGroupNumbers](xref:System.Text.RegularExpressions.Regex.GetGroupNumbers) dell'istanza. Per determinare i gruppi denominati disponibili nella raccolta, è possibile chiamare il metodo [Regex.GetGroupNames](xref:System.Text.RegularExpressions.Regex.GetGroupNames) dell'istanza. Entrambi i metodi sono particolarmente utili in routine di uso generale, che analizzano le corrispondenze rilevate da un'espressione regolare. 

La proprietà [GroupCollection.Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) è l'indicizzatore della raccolta in C# e la proprietà predefinita dell'oggetto della raccolta in Visual Basic. Ciò vuol dire che è possibile accedere ai singoli oggetti [Group](xref:System.Text.RegularExpressions.Group) in base all'indice oppure in base al nome, nel caso di gruppi denominati, come indicato di seguito: 

```csharp
Group group = match.Groups[ctr];
```

```vb
Dim group As Group = match.Groups(ctr)
```

L'esempio seguente definisce un'espressione regolare che usa costrutti di raggruppamento per acquisire il mese, il giorno e l'anno di una data. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)\s(\d{1,2}),\s(\d{4})\b";
      string input = "Born: July 28, 1989";
      Match match = Regex.Match(input, pattern);
      if (match.Success)
         for (int ctr = 0; ctr <  match.Groups.Count; ctr++)
            Console.WriteLine("Group {0}: {1}", ctr, match.Groups[ctr].Value);
    }
}
// The example displays the following output:
//       Group 0: July 28, 1989
//       Group 1: July
//       Group 2: 28
//       Group 3: 1989
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)\s(\d{1,2}),\s(\d{4})\b"
      Dim input As String = "Born: July 28, 1989"
      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         For ctr As Integer = 0 To match.Groups.Count - 1
            Console.WriteLine("Group {0}: {1}", ctr, match.Groups(ctr).Value)
         Next      
      End If   
   End Sub
End Module
' The example displays the following output:
'       Group 0: July 28, 1989
'       Group 1: July
'       Group 2: 28
'       Group 3: 1989
```

Il criterio di ricerca di espressioni regolari `\b(\w+)\s(\d{1,2}),\s(\d{4})\b` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(\d{1,2})` | Trova la corrispondenza con una o due cifre decimali. Equivale al secondo gruppo di acquisizione.
`,` | Trova la corrispondenza con una virgola.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(\d{4})` | Trova la corrispondenza con quattro cifre decimali. Equivale al terzo gruppo di acquisizione.
`\b` | Termina la corrispondenza sul confine di parola.
 
## <a name="the-captured-group"></a>Gruppo acquisito

La classe [Group](xref:System.Text.RegularExpressions.Group) rappresenta il risultato di un singolo gruppo di acquisizione. Gli oggetti [Group](xref:System.Text.RegularExpressions.Group) che rappresentano i gruppi di acquisizione definiti in un'espressione regolare sono restituiti dalla proprietà [Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) dell'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups). La proprietà [Item](xref:System.Text.RegularExpressions.GroupCollection.Item(System.Int32)) è l'indicizzatore (in C#) e la proprietà predefinita (in Visual Basic) della classe [Group](xref:System.Text.RegularExpressions.Group). È anche possibile recuperare singoli membri eseguendo l'iterazione della raccolta mediante il costrutto `foreach`. Per un esempio, vedere la sezione precedente.

L'esempio seguente usa i costrutti di raggruppamento annidati per acquisire le sottostringhe nei gruppi. Il criterio di espressione regolare `(a(b))c` corrisponde alla stringa "abc". Assegna la sottostringa "ab" al primo gruppo di acquisizione e la sottostringa "b" al secondo gruppo di acquisizione.

```csharp
List<int> matchposition = new List<int>();
List<string> results = new List<string>();
// Define substrings abc, ab, b.
Regex r = new Regex("(a(b))c"); 
Match m = r.Match("abdabc");
for (int i = 0; m.Groups[i].Value != ""; i++) 
{
   // Add groups to string array.
   results.Add(m.Groups[i].Value); 
   // Record character position.
   matchposition.Add(m.Groups[i].Index); 
}

// Display the capture groups.
for (int ctr = 0; ctr < results.Count; ctr++)
   Console.WriteLine("{0} at position {1}", 
                     results[ctr], matchposition[ctr]);
// The example displays the following output:
//       abc at position 3
//       ab at position 3
//       b at position 4
```

```vb
Dim matchposition As New List(Of Integer)
 Dim results As New List(Of String)
 ' Define substrings abc, ab, b.
 Dim r As New Regex("(a(b))c") 
 Dim m As Match = r.Match("abdabc")
 Dim i As Integer = 0
 While Not (m.Groups(i).Value = "")    
    ' Add groups to string array.
    results.Add(m.Groups(i).Value)     
    ' Record character position. 
    matchposition.Add(m.Groups(i).Index) 
     i += 1
 End While

 ' Display the capture groups.
 For ctr As Integer = 0 to results.Count - 1
    Console.WriteLine("{0} at position {1}", _ 
                      results(ctr), matchposition(ctr))
 Next                     
' The example displays the following output:
'       abc at position 3
'       ab at position 3
'       b at position 4
```

L'esempio seguente usa costrutti di raggruppamento con nome per acquisire sottostringhe da una stringa che include dati nel formato "DATANAME:VALUE" e viene suddivisa in corrispondenza dei due punti (:) dall'espressione regolare.

```csharp
Regex r = new Regex("^(?<name>\\w+):(?<value>\\w+)");
Match m = r.Match("Section1:119900");
Console.WriteLine(m.Groups["name"].Value);
Console.WriteLine(m.Groups["value"].Value);
// The example displays the following output:
//       Section1
//       119900
```

```vb
Dim r As New Regex("^(?<name>\w+):(?<value>\w+)")
Dim m As Match = r.Match("Section1:119900")
Console.WriteLine(m.Groups("name").Value)
Console.WriteLine(m.Groups("value").Value)
' The example displays the following output:
'       Section1
'       119900
```

Il criterio di ricerca di espressioni regolari `^(?<name>\w+):(?<value>\w+)` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`(?<name>\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è nome.
`:` | Trova la corrispondenza con i due punti.
`(?<value>\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è valore.
 
Le proprietà della classe [Group](xref:System.Text.RegularExpressions.Group) offrono informazioni sul gruppo acquisito. La proprietà `Group.Value` include la sottostringa acquisita, la proprietà `Group.Index` indica la posizione iniziale del gruppo acquisito nel testo di input, la proprietà `Group.Length` include la lunghezza del testo acquisito e la proprietà `Group.Success` indica se una sottostringa corrisponde al criterio definito dal gruppo di acquisizione.

L'applicazione di quantificatori a un gruppo (per altre informazioni, vedere [Quantificatori nelle espressioni regolari](quantifiers.md)) modifica la relazione di un'acquisizione per un gruppo di acquisizione in due modi:

* Se il quantificatore __*__ o __*?__ (che specifica zero o più corrispondenze) è applicato a un gruppo, è possibile che per un gruppo di acquisizione non siano rilevate corrispondenze nella stringa di input. Se non è presente testo acquisito, le proprietà dell'oggetto [Group](xref:System.Text.RegularExpressions.Group) sono impostate come illustrato nella tabella seguente.

  Proprietà del gruppo | Valore
  -------------- | ----- 
  `Success` | `false`
  `Value` | [String.Empty](xref:System.String.Empty) 
  `Length` | 0
 
  Nell'esempio seguente viene illustrato questo concetto. Nel criterio di espressione regolare `aaa(bbb)*ccc` per il primo gruppo di acquisizione (sottostringa "bbb") possono essere rilevate zero o più corrispondenze. Poiché la stringa di input "aaaccc" corrisponde al modello, per il gruppo di acquisizione non sono rilevate corrispondenze.

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = "aaa(bbb)*ccc";
        string input = "aaaccc";
        Match match = Regex.Match(input, pattern);
        Console.WriteLine("Match value: {0}", match.Value);
        if (match.Groups[1].Success)
           Console.WriteLine("Group 1 value: {0}", match.Groups[1].Value);
        else
           Console.WriteLine("The first capturing group has no match.");
     }
  }
  // The example displays the following output:
  //       Match value: aaaccc
  //       The first capturing group has no match.
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "aaa(bbb)*ccc"
        Dim input As String = "aaaccc"
        Dim match As Match = Regex.Match(input, pattern)
        Console.WriteLine("Match value: {0}", match.Value)
        If match.Groups(1).Success Then
           Console.WriteLine("Group 1 value: {0}", match.Groups(1).Value)
        Else
           Console.WriteLine("The first capturing group has no match.")
       End If   
     End Sub
  End Module
  ' The example displays the following output:
  '       Match value: aaaccc
  '       The first capturing group has no match.
  ```

* I quantificatori possono corrispondere a più occorrenze di un modello definito da un gruppo di acquisizione. In questo caso, le proprietà `Value` e `Length` di un oggetto [Group](xref:System.Text.RegularExpressions.Group) contengono informazioni solo sull'ultima sottostringa acquisita. Ad esempio, l'espressione regolare seguente corrisponde a una singola frase che termina con un punto. Usa due costrutti di raggruppamento: il primo acquisisce singole parole insieme a un carattere di spaziatura e il secondo acquisisce le singole parole. Come illustrato dall'output dell'esempio, anche se l'espressione regolare riesce ad acquisire un'intera frase, il secondo gruppo di acquisizione acquisisce solo l'ultima parola.

  ```csharp
  using System;
  using System.Text.RegularExpressions;

  public class Example
  {
     public static void Main()
     {
        string pattern = @"\b((\w+)\s?)+\.";
        string input = "This is a sentence. This is another sentence.";
        Match match = Regex.Match(input, pattern);
        if (match.Success)
        {
           Console.WriteLine("Match: " + match.Value);
           Console.WriteLine("Group 2: " + match.Groups[2].Value);
        }   
     }
  }
  // The example displays the following output:
  //       Match: This is a sentence.
  //       Group 2: sentence
  ```

  ```vb
  Imports System.Text.RegularExpressions

  Module Example
     Public Sub Main()
        Dim pattern As String = "\b((\w+)\s?)+\."
        Dim input As String = "This is a sentence. This is another sentence."
        Dim match As Match = Regex.Match(input, pattern)
        If match.Success Then
           Console.WriteLine("Match: " + match.Value)
           Console.WriteLine("Group 2: " + match.Groups(2).Value)
        End If   
     End Sub
  End Module
  ' The example displays the following output:
  '       Match: This is a sentence.
  '       Group 2: sentence
  ```

## <a name="the-capture-collection"></a>Raccolta Capture

L'oggetto [Group](xref:System.Text.RegularExpressions.Group) contiene informazioni solo sull'ultima acquisizione. Tuttavia, l'intero set di acquisizioni eseguite da un gruppo di acquisizione è ancora disponibile dall'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) restituito dalla proprietà [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures). Ogni membro della raccolta è un oggetto [Capture](xref:System.Text.RegularExpressions.Capture) che rappresenta un'acquisizione eseguita da quel gruppo di acquisizione, in base all'ordine di acquisizione e quindi in base all'ordine in cui sono state rilevate corrispondenze per le stringhe acquisite da sinistra a destra nella stringa di input. È possibile recuperare singoli oggetti [Capture](xref:System.Text.RegularExpressions.Capture) dalla raccolta in uno dei due modi seguenti: 

* Eseguendo un'iterazione nella raccolta tramite un costrutto, ad esempio `foreach` (in C#) o `For Each` (in Visual Basic).

* Usando la proprietà [CaptureCollection.Item](xref:System.Text.RegularExpressions.CaptureCollection.Item(System.Int32)) per recuperare un oggetto specifico in base all'indice. La proprietà Item è la proprietà predefinita (in Visual Basic) o l'indicizzatore (in C#) dell'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection).


Se a un gruppo di acquisizione non è applicato nessun quantificatore, l'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) conterrà un singolo oggetto [Capture](xref:System.Text.RegularExpressions.Capture) di scarso interesse, poiché restituisce informazioni sulla stessa corrispondenza specificata dall'oggetto [Group](xref:System.Text.RegularExpressions.Group). Se a un gruppo di acquisizione è applicato un quantificatore, l'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) conterrà tutte le acquisizioni eseguite dal gruppo di acquisizione e l'ultimo membro della raccolta rappresenterà la stessa acquisizione dell'oggetto [Group](xref:System.Text.RegularExpressions.Group). 

Ad esempio, se si usa il criterio di espressioni regolari `((a(b))c)+` (in cui il quantificatore `+` specifica una o più corrispondenze) per acquisire corrispondenze dalla stringa "abcabcabc", l'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) per ogni oggetto [Group](xref:System.Text.RegularExpressions.Group) conterrà tre membri.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "((a(b))c)+";
      string input = "abcabcabc";

      Match match = Regex.Match(input, pattern);
      if (match.Success)
      {
         Console.WriteLine("Match: '{0}' at position {1}",  
                           match.Value, match.Index);
         GroupCollection groups = match.Groups;
         for (int ctr = 0; ctr < groups.Count; ctr++) {
            Console.WriteLine("   Group {0}: '{1}' at position {2}", 
                              ctr, groups[ctr].Value, groups[ctr].Index);
            CaptureCollection captures = groups[ctr].Captures;
            for (int ctr2 = 0; ctr2 < captures.Count; ctr2++) {
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", 
                                 ctr2, captures[ctr2].Value, captures[ctr2].Index);
            }                     
         }
      }
   }
}
// The example displays the following output:
//       Match: 'abcabcabc' at position 0
//          Group 0: 'abcabcabc' at position 0
//             Capture 0: 'abcabcabc' at position 0
//          Group 1: 'abc' at position 6
//             Capture 0: 'abc' at position 0
//             Capture 1: 'abc' at position 3
//             Capture 2: 'abc' at position 6
//          Group 2: 'ab' at position 6
//             Capture 0: 'ab' at position 0
//             Capture 1: 'ab' at position 3
//             Capture 2: 'ab' at position 6
//          Group 3: 'b' at position 7
//             Capture 0: 'b' at position 1
//             Capture 1: 'b' at position 4
//             Capture 2: 'b' at position 7
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "((a(b))c)+"
      Dim input As STring = "abcabcabc"

      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Match: '{0}' at position {1}", _ 
                           match.Value, match.Index)
         Dim groups As GroupCollection = match.Groups
         For ctr As Integer = 0 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at position {2}", _
                              ctr, groups(ctr).Value, groups(ctr).Index)
            Dim captures As CaptureCollection = groups(ctr).Captures
            For ctr2 As Integer = 0 To captures.Count - 1
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", _
                                 ctr2, captures(ctr2).Value, captures(ctr2).Index)
            Next
         Next
      End If
   End Sub
End Module
' The example dosplays the following output:
'       Match: 'abcabcabc' at position 0
'          Group 0: 'abcabcabc' at position 0
'             Capture 0: 'abcabcabc' at position 0
'          Group 1: 'abc' at position 6
'             Capture 0: 'abc' at position 0
'             Capture 1: 'abc' at position 3
'             Capture 2: 'abc' at position 6
'          Group 2: 'ab' at position 6
'             Capture 0: 'ab' at position 0
'             Capture 1: 'ab' at position 3
'             Capture 2: 'ab' at position 6
'          Group 3: 'b' at position 7
'             Capture 0: 'b' at position 1
'             Capture 1: 'b' at position 4
'             Capture 2: 'b' at position 7
```

L'esempio seguente usa l'espressione regolare `(Abc)+` per trovare una o più esecuzioni consecutive della stringa "Abc" nella stringa "XYZAbcAbcAbcXYZAbcAb". L'esempio illustra l'uso della proprietà [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures) per restituire più gruppi di sottostringhe acquisite.

```csharp
{
   int counter;
   Match m;
   CaptureCollection cc;
   GroupCollection gc;

   // Look for groupings of "Abc".
   Regex r = new Regex("(Abc)+"); 
   // Define the string to search.
   m = r.Match("XYZAbcAbcAbcXYZAbcAb"); 
   gc = m.Groups;

   // Display the number of groups.
   Console.WriteLine("Captured groups = " + gc.Count.ToString());

   // Loop through each group.
   for (int i=0; i < gc.Count; i++) 
   {
      cc = gc[i].Captures;
      counter = cc.Count;

      // Display the number of captures in this group.
      Console.WriteLine("Captures count = " + counter.ToString());

      // Loop through each capture in the group.
      for (int ii = 0; ii < counter; ii++) 
      {
         // Display the capture and its position.
         Console.WriteLine(cc[ii] + "   Starts at character " + 
              cc[ii].Index);
      }
   }
}
// The example displays the following output:
//       Captured groups = 2
//       Captures count = 1
//       AbcAbcAbc   Starts at character 3
//       Captures count = 3
//       Abc   Starts at character 3
//       Abc   Starts at character 6
//       Abc   Starts at character 9  
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "((a(b))c)+"
      Dim input As STring = "abcabcabc"

      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Match: '{0}' at position {1}", _ 
                           match.Value, match.Index)
         Dim groups As GroupCollection = match.Groups
         For ctr As Integer = 0 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at position {2}", _
                              ctr, groups(ctr).Value, groups(ctr).Index)
            Dim captures As CaptureCollection = groups(ctr).Captures
            For ctr2 As Integer = 0 To captures.Count - 1
               Console.WriteLine("      Capture {0}: '{1}' at position {2}", _
                                 ctr2, captures(ctr2).Value, captures(ctr2).Index)
            Next
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Match: 'abcabcabc' at position 0
'          Group 0: 'abcabcabc' at position 0
'             Capture 0: 'abcabcabc' at position 0
'          Group 1: 'abc' at position 6
'             Capture 0: 'abc' at position 0
'             Capture 1: 'abc' at position 3
'             Capture 2: 'abc' at position 6
'          Group 2: 'ab' at position 6
'             Capture 0: 'ab' at position 0
'             Capture 1: 'ab' at position 3
'             Capture 2: 'ab' at position 6
'          Group 3: 'b' at position 7
'             Capture 0: 'b' at position 1
'             Capture 1: 'b' at position 4
'             Capture 2: 'b' at position 7
```

## <a name="the-individual-capture"></a>Singola acquisizione

La classe [Capture](xref:System.Text.RegularExpressions.Capture) contiene i risultati di una singola acquisizione di sottoespressione. La proprietà [Capture.Value](xref:System.Text.RegularExpressions.Capture.Value) contiene il testo corrispondente e la proprietà [Capture.Index](xref:System.Text.RegularExpressions.Capture.Index) indica la posizione a base zero nella stringa di input in cui inizia la sottostringa corrispondente. 

L'esempio seguente analizza una stringa di input per ottenere la temperatura di città selezionate. Una città e la relativa temperatura sono separate da una virgola (",") e un punto e virgola (";") separa i dati di ogni città. L'intera stringa di input rappresenta una singola corrispondenza. Nel criterio di espressione regolare `((\w+(\s\w+)*),(\d+);)+`, usato per analizzare la stringa, il nome della città è assegnato al secondo gruppo di acquisizione e la temperatura al quarto.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "Miami,78;Chicago,62;New York,67;San Francisco,59;Seattle,58;"; 
      string pattern = @"((\w+(\s\w+)*),(\d+);)+";
      Match match = Regex.Match(input, pattern);
      if (match.Success)
      {
         Console.WriteLine("Current temperatures:");
         for (int ctr = 0; ctr < match.Groups[2].Captures.Count; ctr++)
            Console.WriteLine("{0,-20} {1,3}", match.Groups[2].Captures[ctr].Value, 
                              match.Groups[4].Captures[ctr].Value);
      }
   }
}
// The example displays the following output:
//       Current temperatures:
//       Miami                 78
//       Chicago               62
//       New York              67
//       San Francisco         59
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "Miami,78;Chicago,62;New York,67;San Francisco,59;Seattle,58;" 
      Dim pattern As String = "((\w+(\s\w+)*),(\d+);)+"
      Dim match As Match = Regex.Match(input, pattern)
      If match.Success Then
         Console.WriteLine("Current temperatures:")
         For ctr As Integer = 0 To match.Groups(2).Captures.Count - 1
            Console.WriteLine("{0,-20} {1,3}", match.Groups(2).Captures(ctr).Value, _
                              match.Groups(4).Captures(ctr).Value)
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Current temperatures:
'       Miami                 78
'       Chicago               62
'       New York              67
'       San Francisco         59
```

L'espressione regolare è definita nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`(\s\w+)*` | Trova la corrispondenza con zero o più occorrenze di un carattere di spaziatura seguito da uno o più caratteri di parola. Questo modello corrisponde a nomi di città composti da più parole. Equivale al terzo gruppo di acquisizione.
`(\w+(\s\w+)*)` | Trova la corrispondenza con uno o più caratteri di parola seguiti da zero o più caratteri di spaziatura e uno o più caratteri di parola. Equivale al secondo gruppo di acquisizione.
`,` | Trova la corrispondenza con una virgola.
`(\d+)` | Trova la corrispondenza con una o più cifre. Questo è il quarto gruppo di acquisizione.
`;` | Trova la corrispondenza con un punto e virgola.
`((\w+(\s\w+)*),(\d+);)+` | Trova la corrispondenza con modello di una parola seguita da parole aggiuntive seguite da una virgola, una o più cifre e un punto e virgola, una o più volte. Equivale al primo gruppo di acquisizione. 
 
## <a name="see-also"></a>Vedere anche

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[Espressioni regolari .NET](regular-expressions.md)

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)


