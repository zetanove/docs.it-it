---
title: Costrutti di raggruppamento nelle espressioni regolari
description: Costrutti di raggruppamento nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e0bf3718-e64b-460b-b73d-66678cec6093
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: d27c8c68ea49f150fa0ae5c5c8b437c8c42c9c90

---

# <a name="grouping-constructs-in-regular-expressions"></a>Costrutti di raggruppamento nelle espressioni regolari

I costrutti di raggruppamento delineano sottoespressioni di un'espressione regolare e acquisiscono sottostringhe di una stringa di input. È possibile usare i costrutti di raggruppamento per effettuare le operazioni seguenti:

* Trovare la corrispondenza di una sottoespressione ripetuta nella stringa di input.

* Applicare un quantificatore a una sottoespressione che dispone di più elementi del linguaggio di espressioni regolari. Per altre informazioni sui quantificatori, vedere [Quantificatori nelle espressioni regolari](quantifiers.md).

* Includere una sottoespressione nella stringa restituita dai metodi [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) e [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)).

* Recuperare le singole sottoespressioni dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups) ed elaborarle separatamente dal testo corrispondente nel suo complesso.

La tabella seguente elenca i costrutti di raggruppamento supportati dal motore delle espressioni regolari di .NET e indica se sono di acquisizione o non acquisizione. 

Costrutto di raggruppamento | Acquisizione o non acquisizione
------------------ | -------------------------
[Sottoespressioni corrispondenti](#matched-subexpressions) | Acquisizione
[Sottoespressioni corrispondenti denominate](#named-matched-subexpressions) | Acquisizione
[Definizioni di gruppo di bilanciamento](#balancing-group-definitions) | Acquisizione
[Gruppi di non acquisizione](#noncapturing-groups) | Non acquisizione
[Opzioni di gruppo](#group-options) | Non acquisizione
[Asserzioni lookahead positive di larghezza zero](#zero-width-positive-lookahead-assertions) | Non acquisizione
[Asserzioni lookahead negative di larghezza zero](#zero-width-negative-lookahead-assertions) | Non acquisizione
[Asserzioni lookbehind positive di larghezza zero](#zero-width-positive-lookbehind-assertions) | Non acquisizione
[Asserzioni lookbehind negative di larghezza zero](#zero-width-negative-lookbehind-assertions) | Non acquisizione
[Sottoespressioni di non backtracking](#nonbacktracking-subexpressions) | Non acquisizione

Per informazioni sui gruppi e sul modello a oggetti delle espressioni regolari, vedere [Costrutti di raggruppamento e oggetti di espressione regolare](#grouping-constructs-and-regular-expression-objects). 

## <a name="matched-subexpressions"></a>Sottoespressioni corrispondenti

Nel costrutto di raggruppamento seguente viene acquisita una sottoespressione corrispondente: 

**(**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari valido. Le acquisizioni che usano parentesi sono numerate automaticamente da sinistra verso destra in base all'ordine delle parentesi di apertura nell'espressione regolare, a partire da uno. L'acquisizione che viene numerata zero è il testo corrispondente all'intero criterio dell'espressione regolare.

> [!NOTE]
> Per impostazione predefinita, l'elemento di linguaggio (sottoespressione) acquisisce la sottoespressione corrispondente. Tuttavia, se il parametro RegexOptions di un metodo dei criteri di ricerca di espressioni regolari include il flag RegexOptions.ExplicitCapture o se viene applicata l'opzione n a questa sottoespressione (vedere Opzioni di gruppo più avanti in questo argomento), la sottoespressione corrispondente non viene acquisita.
 
È possibile accedere a questi gruppi acquisiti in quattro modi diversi:

* Tramite il costrutto del backreference all'interno dell'espressione regolare. Tramite la sintassi **\**_numero_, dove *numero* è il numero ordinale della sottoespressione acquisita, è possibile fare riferimento alla sottoespressione corrispondente nella stessa espressione regolare.

* Tramite il costrutto del backreference denominato all'interno dell'espressione regolare. Tramite la sintassi **\k<**_nome_**>**, dove *nome* è il nome di un gruppo di acquisizione, o **\k**_<numero_**>**, dove *numero* è il numero ordinale di un gruppo di acquisizione, è possibile fare riferimento alla sottoespressione corrispondente nella stessa espressione regolare. Un gruppo di acquisizione ha un nome predefinito identico al relativo numero ordinale. Per altre informazioni, vedere Costrutti di raggruppamento e oggetti di espressione regolare più avanti in questo argomento.

* Tramite la sequenza di sostituzione **$**_numero_ in una chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) o [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)), dove *numero* è il numero ordinale della sottoespressione acquisita.

* A livello di programmazione, tramite l'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups). Il membro alla posizione zero nella raccolta rappresenta l'intera corrispondenza dell'espressione regolare. Ogni membro successivo rappresenta una sottoespressione corrispondente. Per altre informazioni, vedere la sezione [Costrutti di raggruppamento e oggetti di espressione regolare](#grouping-constructs-and-regular-expression-objects).

Nell'esempio seguente viene illustrata un'espressione regolare che identifica le parole duplicate in un testo. I due gruppi di acquisizione del criterio di ricerca di espressioni regolari rappresentano le due istanze della parola duplicata. La seconda istanza è acquisita per riportare la posizione iniziale nella stringa di input.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w+)\s(\1)";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.", 
                           match.Groups[1].Value, match.Groups[1].Index, match.Groups[2].Index);
   }
}
// The example displays the following output:
//       Duplicate 'that' found at positions 8 and 13.
//       Duplicate 'the' found at positions 22 and 26.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w+)\s(\1)\W"
      Dim input As String = "He said that that was the the correct answer."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("Duplicate '{0}' found at positions {1} and {2}.", _
                           match.Groups(1).Value, match.Groups(1).Index, match.Groups(2).Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Duplicate 'that' found at positions 8 and 13.
'       Duplicate 'the' found at positions 22 and 26.
```

Il criterio dell'espressione regolare è il seguente:

```
(\w+)\s(\1)\W
```

Nella tabella seguente è illustrata l'interpretazione del criterio di ricerca di espressioni regolari. 

Criterio | Descrizione
------- | ----------- 
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(\1)` | Trova la corrispondenza con la stringa nel primo gruppo acquisito. Equivale al secondo gruppo di acquisizione. L'esempio lo assegna a un gruppo acquisito in modo che sia possibile recuperare la posizione iniziale della parola duplicata dalla proprietà `Match.Index`.
`\W` | Trova la corrispondenza con un carattere non alfanumerico, inclusi spazio vuoto e punteggiatura. Impedisce al criterio dell'espressione regolare di trovare la corrispondenza con una parola che inizia con la parola del primo gruppo acquisito.
 
## <a name="named-matched-subexpressions"></a>Sottoespressioni corrispondenti denominate

Il costrutto di raggruppamento seguente acquisisce una sottoespressione corrispondente e consente di accedervi tramite nome o numero: 

```
(?<name>subexpression)
```

oppure:

```
(?'name'subexpression)
```

dove *nome* è un nome di gruppo valido e *sottoespressione* è un qualsiasi criterio di espressioni regolari valido. *nome* non deve contenere alcun simbolo di punteggiatura e non può iniziare con un numero.

> [!NOTE]
> Se il parametro [RegexOptions](xref:System.Text.RegularExpressions.RegexOptions) di un metodo dei criteri di ricerca di espressioni regolari include il flag [RegexOptions.ExplicitCapture](xref:System.Text.RegularExpressions.RegexOptions.ExplicitCapture) o se l'opzione **n** viene applicata a questa sottoespressione (vedere [Opzioni di gruppo](#group-options) più avanti in questo argomento), l'unico modo per acquisire una sottoespressione è assegnare esplicitamente un nome ai gruppi di acquisizione.
 
È possibile accedere ai gruppi acquisiti denominati nei modi seguenti:

* Tramite il costrutto del backreference denominato all'interno dell'espressione regolare. Tramite la sintassi **\k<**_nome_**>**, dove *nome* è il nome della sottoespressione acquisita, è possibile fare riferimento alla sottoespressione corrispondente nella stessa espressione regolare. 

* Tramite il costrutto del backreference all'interno dell'espressione regolare. Tramite la sintassi **\**_numero_, dove *numero* è il numero ordinale della sottoespressione acquisita, è possibile fare riferimento alla sottoespressione corrispondente nella stessa espressione regolare. Le sottoespressioni corrispondenti denominate sono numerate consecutivamente da sinistra a destra dopo le sottoespressioni corrispondenti.

* Tramite la sequenza di sostituzione **${**_nome_**}** in una chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) o [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)), dove *nome* è il nome della sottoespressione acquisita.

* Tramite la sequenza di sostituzione **$**_numero_ in una chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) o [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)), dove *numero* è il numero ordinale della sottoespressione acquisita.

* A livello di programmazione, tramite l'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups). Il membro alla posizione zero nella raccolta rappresenta l'intera corrispondenza dell'espressione regolare. Ogni membro successivo rappresenta una sottoespressione corrispondente. I gruppi acquisiti denominati vengono archiviati nella raccolta dopo i gruppi acquisiti numerati.

* A livello di codice, specificando il nome della sottoespressione all'indicizzatore dell'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) (in C#) o alla relativa proprietà Item (in Visual Basic).

Un criterio di ricerca di espressioni regolari semplice illustra in che modo è possibile fare riferimento a gruppi denominati e numerati (non denominati) a livello di codice o tramite la sintassi del linguaggio delle espressioni regolari. L'espressione regolare `((?<One>abc)\d+)?(?<Two>xyz)(.*)` crea i gruppi di acquisizione seguenti in base a numero e nome. Il primo gruppo di acquisizione (numero 0) fa sempre riferimento all'intero criterio.

Numero | Nome | Criterio
------ | ---- | ------- 
0 | 0 (nome predefinito) | `((?<One>abc)\d+)?(?<Two>xyz)(.*)`
1 | 1 (nome predefinito) | `((?<One>abc)\d+)`
2 | 2 (nome predefinito) | `(.*)`
3 | Uno | `(?<One>abc)`
4 | Due | `(?<Two>xyz)`
 
Nell'esempio seguente viene illustrata un'espressione regolare che identifica parole duplicate e la parola che segue immediatamente ogni parola duplicata. Il criterio di ricerca di espressioni regolari definisce due sottoespressioni denominate: `duplicateWord` che rappresenta la parola duplicata e `nextWord` che rappresenta la parola che segue la parola duplicata. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)";
      string input = "He said that that was the the correct answer.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("A duplicate '{0}' at position {1} is followed by '{2}'.", 
                           match.Groups["duplicateWord"].Value, match.Groups["duplicateWord"].Index, 
                           match.Groups["nextWord"].Value);

   }
}
// The example displays the following output:
//       A duplicate 'that' at position 8 is followed by 'was'.
//       A duplicate 'the' at position 22 is followed by 'correct'.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)"
      Dim input As String = "He said that that was the the correct answer."
      Console.WriteLine(Regex.Matches(input, pattern, RegexOptions.IgnoreCase).Count)
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("A duplicate '{0}' at position {1} is followed by '{2}'.", _
                           match.Groups("duplicateWord").Value, match.Groups("duplicateWord").Index, _
                           match.Groups("nextWord").Value)
      Next
   End Sub
End Module
' The example displays the following output:
'    A duplicate 'that' at position 8 is followed by 'was'.
'    A duplicate 'the' at position 22 is followed by 'correct'.
```

Il criterio di ricerca di espressioni regolari è il seguente:

```
(?<duplicateWord>\w+)\s\k<duplicateWord>\W(?<nextWord>\w+)
```

Nella tabella seguente viene illustrato come viene interpretata l'espressione regolare.

Criterio | Descrizione
------- | -----------
`(?<duplicateWord>\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è `duplicateWord`.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`\k<duplicateWord>` | Trova la corrispondenza con la stringa del gruppo acquisito che è denominata `duplicateWord`. 
`\W` | Trova la corrispondenza con un carattere non alfanumerico, inclusi spazio vuoto e punteggiatura. Impedisce al criterio dell'espressione regolare di trovare la corrispondenza con una parola che inizia con la parola del primo gruppo acquisito.
`(?<nextWord>\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Il nome di questo gruppo di acquisizione è `nextWord`.
 
Il nome di un gruppo può essere ripetuto in un'espressione regolare. Ad esempio, è possibile che più di un gruppo sia denominato `digit`, come illustrato nell'esempio seguente. Nel caso di nomi duplicati, il valore dell'oggetto [Group](xref:System.Text.RegularExpressions.Group) è determinato dall'ultima acquisizione corretta nella stringa di input. L'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) viene anche popolato con informazioni su ogni acquisizione, secondo la normale procedura usata quando il nome del gruppo non è duplicato. 

Nell'esempio seguente l'espressione regolare `\D+(?<digit>\d+)\D+(?<digit>\d+)?` include due occorrenze di un gruppo denominato `digit`. Il primo gruppo denominato `digit` acquisisce una o più cifre. Il secondo gruppo denominato `digit` acquisisce zero o un'occorrenza di una o più cifre. Come illustrato nell'esempio, se il secondo gruppo di acquisizione corrisponde al testo, il valore del testo definisce il valore dell'oggetto [Group](xref:System.Text.RegularExpressions.Group). Se il secondo gruppo di acquisizione non corrisponde alla stringa di input, il valore dell'ultima corrispondenza corretta definisce il valore dell'oggetto [Group](xref:System.Text.RegularExpressions.Group). 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      String pattern = @"\D+(?<digit>\d+)\D+(?<digit>\d+)?";
      String[] inputs = { "abc123def456", "abc123def" };
      foreach (var input in inputs) {
         Match m = Regex.Match(input, pattern);
         if (m.Success) {
            Console.WriteLine("Match: {0}", m.Value);
            for (int grpCtr = 1; grpCtr < m.Groups.Count; grpCtr++) {
               Group grp = m.Groups[grpCtr];
               Console.WriteLine("Group {0}: {1}", grpCtr, grp.Value);
               for (int capCtr = 0; capCtr < grp.Captures.Count; capCtr++)
                  Console.WriteLine("   Capture {0}: {1}", capCtr,
                                    grp.Captures[capCtr].Value);
            }
         }
         else {
            Console.WriteLine("The match failed.");
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//       Match: abc123def456
//       Group 1: 456
//          Capture 0: 123
//          Capture 1: 456
//
//       Match: abc123def
//       Group 1: 123
//          Capture 0: 123
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\D+(?<digit>\d+)\D+(?<digit>\d+)?"
      Dim inputs() As String = { "abc123def456", "abc123def" }
      For Each input As String In inputs
         Dim m As Match = Regex.Match(input, pattern)
         If m.Success Then
            Console.WriteLine("Match: {0}", m.Value)
            For grpCtr As Integer = 1 to m.Groups.Count - 1
               Dim grp As Group = m.Groups(grpCtr)
               Console.WriteLine("Group {0}: {1}", grpCtr, grp.Value)
               For capCtr As Integer = 0 To grp.Captures.Count - 1
                  Console.WriteLine("   Capture {0}: {1}", capCtr,
                                    grp.Captures(capCtr).Value)
               Next
            Next
         Else
            Console.WriteLine("The match failed.")
         End If
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: abc123def456
'       Group 1: 456
'          Capture 0: 123
'          Capture 1: 456
'
'       Match: abc123def
'       Group 1: 123
'          Capture 0: 123
```

Nella tabella seguente viene illustrato come viene interpretata l'espressione regolare.

Criterio | Descrizione
------- | -----------
`\D+` | Corrisponde a una o più cifre non decimali. 
`(?<digit>\d+)` | Corrisponde a una o più cifre decimali. Assegna la corrispondenza al gruppo denominato `digit`. 
`\D+` | Corrisponde a una o più cifre non decimali. 
`(?<digit>\d+)?` | Corrisponde a zero o a un'occorrenza di una o più cifre decimali. Assegna la corrispondenza al gruppo denominato `digit`.
 
## <a name="balancing-group-definitions"></a>Definizioni di gruppo di bilanciamento

Una definizione di gruppo di bilanciamento elimina la definizione di un gruppo precedentemente definito e archivia nel gruppo corrente l'intervallo tra il gruppo precedentemente definito e il gruppo corrente. Questo costrutto di raggruppamento presenta il formato seguente: 

```
(?<name1-name2>subexpression)
```

oppure:

```
(?'name1-name2' subexpression)
```

dove *nome1* è il gruppo corrente (facoltativo), *nome2* è un gruppo precedentemente definito e *sottoespressione* è un qualsiasi criterio di espressioni regolari valido. La definizione di gruppo di bilanciamento elimina la definizione di *nome2* e archivia l'intervallo tra *nome2* e *nome1* in *nome1*. Se non è definito alcun gruppo *nome2*, viene eseguito il backtracking della corrispondenza. Poiché l'eliminazione dell'ultima definizione di *nome2* rivela la definizione precedente di *nome2*, questo costrutto consente di usare lo stack di acquisizioni per il gruppo *nome2* come contatore per tenere traccia dei costrutti annidati, come ad esempio le parentesi o le parentesi quadre di apertura e chiusura. 

La definizione del gruppo di bilanciamento usa *nome2* come stack. Il carattere iniziale di ogni costrutto annidato viene posizionato nel gruppo e nella relativa raccolta [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures). Quando viene trovata la corrispondenza con il carattere di chiusura, il carattere di apertura associato viene rimosso dal gruppo e la raccolta [Captures](xref:System.Text.RegularExpressions.Group.Captures) viene ridotta di una unità. Dopo aver trovato la corrispondenza dei caratteri di apertura e chiusura di tutti i costrutti annidati, *nome1* sarà vuoto.

> [!NOTE]
> Dopo avere modificato l'espressione regolare dell'esempio seguente affinché usi il carattere di apertura e chiusura appropriato di un costrutto annidato, è possibile usarla per gestire più costrutti annidati, come ad esempio espressioni matematiche o righe di codice del programma che includono più chiamate al metodo annidate. 
 
Nell'esempio seguente viene usata una definizione di gruppo di bilanciamento per trovare una corrispondenza di parentesi uncinate aperte e chiuse (<>) in una stringa di input. Nell'esempio vengono definiti due gruppi denominati, `Open` e `Close`, usati come uno stack per rilevare coppie corrispondenti di parentesi uncinate. Ogni parentesi uncinata aperta acquisita viene inserita nella raccolta di acquisizioni del gruppo `Open` e ogni parentesi uncinata chiusa acquisita viene inserita nella raccolta di acquisizioni del gruppo `Close`. La definizione di gruppo di bilanciamento si assicura che sia presente una parentesi uncinata chiusa corrispondente per ogni parentesi uncinata aperta. In caso contrario, il criterio secondario `(?(Open)(?!))` finale viene valutato solo se il gruppo `Open` non è vuoto e, pertanto, se tutti i costrutti annidati non sono stati chiusi. Se il criterio secondario finale viene valutato, non viene trovata la corrispondenza perché il criterio secondario `(?!)` è un'asserzione lookahead negativa di larghezza zero che ha sempre esito negativo. 

```csharp
using System;
using System.Text.RegularExpressions;

class Example
{
   public static void Main() 
   {
      string pattern = "^[^<>]*" +
                       "(" + 
                       "((?'Open'<)[^<>]*)+" +
                       "((?'Close-Open'>)[^<>]*)+" +
                       ")*" +
                       "(?(Open)(?!))$";
      string input = "<abc><mno<xyz>>";

      Match m = Regex.Match(input, pattern);
      if (m.Success == true)
      {
         Console.WriteLine("Input: \"{0}\" \nMatch: \"{1}\"", input, m);
         int grpCtr = 0;
         foreach (Group grp in m.Groups)
         {
            Console.WriteLine("   Group {0}: {1}", grpCtr, grp.Value);
            grpCtr++;
            int capCtr = 0;
            foreach (Capture cap in grp.Captures)
            {            
                Console.WriteLine("      Capture {0}: {1}", capCtr, cap.Value);
                capCtr++;
            }
          }
      }
      else
      {
         Console.WriteLine("Match failed.");
      }   
    }
}
// The example displays the following output:
//    Input: "<abc><mno<xyz>>"
//    Match: "<abc><mno<xyz>>"
//       Group 0: <abc><mno<xyz>>
//          Capture 0: <abc><mno<xyz>>
//       Group 1: <mno<xyz>>
//          Capture 0: <abc>
//          Capture 1: <mno<xyz>>
//       Group 2: <xyz
//          Capture 0: <abc
//          Capture 1: <mno
//          Capture 2: <xyz
//       Group 3: >
//          Capture 0: >
//          Capture 1: >
//          Capture 2: >
//       Group 4:
//       Group 5: mno<xyz>
//          Capture 0: abc
//          Capture 1: xyz
//          Capture 2: mno<xyz>
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main() 
        Dim pattern As String = "^[^<>]*" & _
                                "(" + "((?'Open'<)[^<>]*)+" & _
                                "((?'Close-Open'>)[^<>]*)+" + ")*" & _
                                "(?(Open)(?!))$"
        Dim input As String = "<abc><mno<xyz>>"
        Dim rgx AS New Regex(pattern)'
        Dim m As Match = Regex.Match(input, pattern)
        If m.Success Then
            Console.WriteLine("Input: ""{0}"" " & vbCrLf & "Match: ""{1}""", _
                               input, m)
            Dim grpCtr As Integer = 0
            For Each grp As Group In m.Groups
               Console.WriteLine("   Group {0}: {1}", grpCtr, grp.Value)
               grpCtr += 1
               Dim capCtr As Integer = 0
               For Each cap As Capture In grp.Captures            
                  Console.WriteLine("      Capture {0}: {1}", capCtr, cap.Value)
                  capCtr += 1
               Next
            Next
        Else
            Console.WriteLine("Match failed.")
        End If
    End Sub
End Module  
' The example displays the following output:
'       Input: "<abc><mno<xyz>>"
'       Match: "<abc><mno<xyz>>"
'          Group 0: <abc><mno<xyz>>
'             Capture 0: <abc><mno<xyz>>
'          Group 1: <mno<xyz>>
'             Capture 0: <abc>
'             Capture 1: <mno<xyz>>
'          Group 2: <xyz
'             Capture 0: <abc
'             Capture 1: <mno
'             Capture 2: <xyz
'          Group 3: >
'             Capture 0: >
'             Capture 1: >
'             Capture 2: >
'          Group 4:
'          Group 5: mno<xyz>
'             Capture 0: abc
'             Capture 1: xyz
'             Capture 2: mno<xyz>
```

Il criterio di ricerca di espressioni regolari è:

```
^[^<>]*(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*(?(Open)(?!))$
```

L'espressione regolare viene interpretata nel modo seguente.

Criterio | Descrizione
------- | -----------
`^` | Comincia all'inizio della stringa.
`[^<>]*` | Trova la corrispondenza di zero o più caratteri diversi da parentesi uncinate aperte o chiuse.
`(?'Open'<)` | Trova la corrispondenza di una parentesi uncinata aperta e la assegna a un gruppo denominato `Open`.
`[^<>]*` | Trova la corrispondenza di zero o più caratteri diversi da parentesi uncinate aperte o chiuse.
`((?'Open'<)[^<>]*) +` | Trova la corrispondenza di una o più occorrenze di una parentesi uncinata aperta seguita da zero o più caratteri diversi da parentesi uncinate aperte o chiuse. Equivale al secondo gruppo di acquisizione.
`(?'Close-Open'>)` | Trova la corrispondenza di una parentesi uncinata chiusa, assegna la sottostringa tra il gruppo `Open` e il gruppo corrente al gruppo `Close` ed elimina la definizione del gruppo `Open`.
`[^<>]*` | Trova la corrispondenza di zero o più occorrenze di qualsiasi carattere diverso da parentesi uncinate aperte o chiuse. 
`((?'Close-Open'>)[^<>]*)+` | Trova la corrispondenza di una o più occorrenze di una parentesi uncinata chiusa seguita da zero o più occorrenze di caratteri diversi da parentesi uncinate aperte o chiuse. In caso di corrispondenza di una parentesi uncinata chiusa, assegna la sottostringa tra il gruppo `Open` e il gruppo corrente al gruppo `Close` ed elimina la definizione del gruppo `Open`. Equivale al terzo gruppo di acquisizione.
`(((?'Open'<)[^<>]*)+((?'Close-Open'>)[^<>]*)+)*` | Trova la corrispondenza di zero o più occorrenze del criterio seguente: una o più occorrenze di una parentesi uncinata aperta seguite da zero o più parentesi uncinate, seguite da zero o più parentesi non uncinate, seguite da una o più occorrenze di parentesi uncinate chiuse, seguite da zero o più occorrenze di parentesi non uncinate. In caso di corrispondenza di una parentesi uncinata chiusa, elimina la definizione del gruppo `Open` e assegna la sottostringa tra il gruppo `Open` e il gruppo corrente al gruppo `Close`. Equivale al primo gruppo di acquisizione.
`(?(Open)(?!))` | Se il gruppo `Open` esiste, abbandona la corrispondenza se è possibile trovare una corrispondenza per una stringa vuota, ma non avanza la posizione del motore delle espressioni regolari nella stringa. Si tratta di un'asserzione lookahead negativa di larghezza zero. Poiché una stringa vuota è sempre presente in modo implicito in una stringa di input, questa corrispondenza ha sempre esito negativo. L'esito negativo della corrispondenza indica che le parentesi uncinate non sono bilanciate. 
`$` | Trova la corrispondenza con la fine della stringa di input.
 
La sottoespressione finale, `(?(Open)(?!))`, indica se i costrutti annidati nella stringa di input sono bilanciati correttamente, ad esempio se a ogni parentesi uncinata aperta corrisponde una parentesi uncinata chiusa. Usa la corrispondenza condizionale in base a un gruppo acquisito valido. Per altre informazioni, vedere [Costrutti di alternanza nelle espressioni regolari](alternation.md). Se il gruppo `Open` è definito, il motore delle espressioni regolari tenta di stabilire una corrispondenza con la sottoespressione `(?!)` nella stringa di input. Il gruppo `Open` deve essere definito solo se i costrutti annidati non sono bilanciati. Di conseguenza, il criterio per cui trovare la corrispondenza nella stringa di input deve essere inclusi tra quelli che determinano sempre un esito negativo della corrispondenza. In questo caso, `(?!)` è un'asserzione lookahead negativa di larghezza zero che ha sempre esito negativo, in quanto una stringa vuota è sempre implicitamente presente nella posizione successiva nella stringa di input.

Nell'esempio, il motore delle espressioni regolari valuta la stringa di input "<abc><mno<xyz>>", come illustrato nella tabella seguente.

Passaggio | Criterio | Risultato
---- | ------- | ------ 
1 | `^` | Inizia la corrispondenza all'inizio della stringa di input.
2 | `[^<>]*` | Cerca parentesi non uncinate prima della parentesi uncinata aperta; non trova corrispondenze. 
3 | `(((?'Open'<)` | Trova la corrispondenza della parentesi uncinata aperta in "<abc>" e la assegna al gruppo `Open`.
4 | `[^<>]*` | Trova la corrispondenza con "abc".
5 | `)+` | "<abc" è il valore del secondo gruppo acquisito. Il carattere successivo nella stringa di input non è una parentesi uncinata aperta, pertanto il motore delle espressioni regolari non esegue il loopback al criterio secondario `(?'Open'<)[^<>]*)`.
6 | `((?'Close-Open'>)` | Trova la corrispondenza della parentesi uncinata chiusa in "<abc>", assegna "abc", che è la sottostringa tra il gruppo `Open` e la parentesi uncinata chiusa, al gruppo `Close` ed elimina il valore corrente ("<") del gruppo `Open`, lasciandolo vuoto.
7 | `[^<>]*` | Cerca parentesi non uncinate dopo la parentesi uncinata chiusa; non trova corrispondenze.
8 | `)+` | Il valore del terzo gruppo acquisito è ">". Il carattere successivo nella stringa di input non è una parentesi uncinata chiusa, pertanto il motore delle espressioni regolari non esegue il loopback al criterio secondario `((?'Close-Open'>)[^<>]*)`.
9 | `)*` | Il valore del primo gruppo acquisito è "<abc>". Il carattere successivo nella stringa di input è una parentesi uncinata aperta, pertanto il motore delle espressioni regolari esegue il loopback al criterio secondario `(((?'Open'<)`.
10 | `(((?'Open'<)` | Trova la corrispondenza della parentesi uncinata aperta in "<mno>" e la assegna al gruppo `Open`. Nella raccolta `Group.Captures` è ora presente un solo valore, "<".
11 | `[^<>]*` | Trova la corrispondenza con "mno".
12 | `)+` | "<mno" è il valore del secondo gruppo acquisito. Il carattere successivo nella stringa di input è una parentesi uncinata aperta, pertanto il motore delle espressioni regolari esegue il loopback al criterio secondario `(?'Open'<)[^<>]*)`.
13 | `(((?'Open'<)` | Trova la corrispondenza della parentesi uncinata aperta in "<xyz>" e la assegna al gruppo `Open`. Nella raccolta `Group.Captures` del gruppo `Open` sono ora incluse due acquisizioni: la parentesi uncinata aperta di "<mno>" e la parentesi uncinata aperta di "<xyz>".
14 | `[^<>]*` | Trova la corrispondenza con "xyz".
15 | `)+` | "<xyz" è il valore del secondo gruppo acquisito. Il carattere successivo nella stringa di input non è una parentesi uncinata aperta, pertanto il motore delle espressioni regolari non esegue il loopback al criterio secondario `(?'Open'<)[^<>]*)`.
16 | `((?'Close-Open'>)` | Trova la corrispondenza della parentesi uncinata chiusa in "<xyz>". "xyz", assegna la sottostringa tra il gruppo `Open` e la parentesi uncinata chiusa al gruppo `Close` ed elimina il valore corrente dal gruppo `Open`. Il valore dell'acquisizione precedente (la parentesi uncinata aperta in "<mno>") diventa il valore corrente del gruppo `Open`. La raccolta `Captures` del gruppo `Open` include ora una sola acquisizione, ovvero la parentesi uncinata aperta di "<xyz>".
17 | `[^<>]*` | Cerca parentesi non uncinate; non trova corrispondenze.
18 | `)+` | Il valore del terzo gruppo acquisito è ">". Il carattere successivo nella stringa di input è una parentesi uncinata chiusa, pertanto il motore delle espressioni regolari esegue il loopback al criterio secondario `((?'Close-Open'>)[^<>]*)`.
19 | `((?'Close-Open'>)` | Trova la corrispondenza della parentesi uncinata chiusa finale in "xyz>>", assegna "mno<xyz>" (la sottostringa tra il gruppo `Open` e la parentesi uncinata chiusa) al gruppo `Close` ed elimina il valore corrente del gruppo `Open`. Il gruppo `Open` è ora vuoto.
20 | `[^<>]*` | Cerca parentesi non uncinate; non trova corrispondenze.
21 | `)+` | Il valore del terzo gruppo acquisito è ">". Il carattere successivo nella stringa di input non è una parentesi uncinata chiusa, pertanto il motore delle espressioni regolari non esegue il loopback al criterio secondario `((?'Close-Open'>)[^<>]*)`.
22 | `)*` | Il valore del primo gruppo acquisito è "<mno<xyz>>". Il carattere successivo nella stringa di input non è una parentesi uncinata aperta, pertanto il motore delle espressioni regolari non esegue il loopback al criterio secondario `(((?'Open'<)`.
23 | `(?(Open)(?!))` | Il gruppo `Open` non è definito, pertanto non viene tentato di trovare corrispondenze.
24 | `$` | Trova la corrispondenza della fine della stringa di input.

## <a name="noncapturing-groups"></a>Gruppi di non acquisizione

Nel costrutto di raggruppamento seguente non viene acquisita la sottostringa quando viene trovata una corrispondenza con una sottoespressione:

```
**(?**:_subexpression_**)**
```

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari valido. Il costrutto del gruppo non di acquisizione viene generalmente usato quando un quantificatore è applicato a un gruppo, ma le sottostringhe acquisite dal gruppo non sono di alcun interesse.

>[!NOTE]
> Se un'espressione regolare include costrutti di raggruppamento annidati, un costrutto del gruppo di non acquisizione esterno non si applica ai costrutti del gruppo annidati interni. 
 
Nell'esempio seguente viene illustrata un'espressione regolare che include gruppi di non acquisizione. Si noti che nell'output non sono inclusi gruppi acquisiti.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?:\b(?:\w+)\W*)+\.";
      string input = "This is a short sentence.";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: {0}", match.Value);
      for (int ctr = 1; ctr < match.Groups.Count; ctr++)
         Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
   }
}
// The example displays the following output:
//       Match: This is a short sentence.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?:\b(?:\w+)\W*)+\."
      Dim input As String = "This is a short sentence."
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: {0}", match.Value)
      For ctr As Integer = 1 To match.Groups.Count - 1
         Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: This is a short sentence.
```

L'espressione regolare `(?:\b(?:\w+)\W*)+\.` trova la corrispondenza di una frase che termina con un punto. Poiché l'espressione regolare si concentra sulle frasi e non sulle singole parole, i costrutti di raggruppamento vengono usati esclusivamente come quantificatori. Il criterio di ricerca di espressioni regolari viene interpretato come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(?:\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Non assegna il testo corrispondente a un gruppo acquisito.
`\W*` | Trova la corrispondenza di zero o più caratteri non alfanumerici.
`(?:\b(?:\w+)\W*)+` | Trova la corrispondenza con il criterio di ricerca di uno o più caratteri alfanumerici a partire dal confine di una parola, seguiti da zero o più caratteri non alfanumerici, una o più volte. Non assegna il testo corrispondente a un gruppo acquisito.
`\.` | Trova la corrispondenza con un punto.
 
## <a name="group-options"></a>Opzioni di gruppo

Il costrutto di raggruppamento applica o disabilita le opzioni specificate all'interno di una sottoespressione:

**(?imnsx-imnsx:**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari valido. Ad esempio, `(?i-s:)` disattiva la differenziazione tra maiuscole e minuscole e disabilita la modalità riga singola. Per altre informazioni sulle opzioni inline che è possibile specificare, vedere [Opzioni di espressioni regolari](options.md).

> [!NOTE]
> È possibile specificare opzioni che si applicano a un'espressione regolare intera anziché a una sottoespressione usando un costruttore della classe [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) o un metodo statico. È possibile specificare anche opzioni inline che si applicano dopo un punto specifico in un'espressione regolare usando il costrutto di linguaggio `(?imnsx-imnsx)`.
 
Il costrutto delle opzioni di gruppo non è un gruppo di acquisizione. Sebbene qualsiasi parte di una stringa acquisita dalla *sottoespressione* sia inclusa nella corrispondenza, non viene inclusa in un gruppo acquisito né usata per popolare l'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection).

Ad esempio, l'espressione regolare `\b(?ix: d \w+)\s ` nell'esempio seguente usa le opzioni inline in un costrutto di raggruppamento per abilitare la corrispondenza tra maiuscole e minuscole e per ignorare gli spazi vuoti nel criterio durante l'identificazione delle parole che iniziano con la lettera "d". L'espressione regolare è definita nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
 `(?ix: d \w+)` | Usando la corrispondenza senza distinzione tra maiuscole e minuscole e ignorando lo spazio vuoto in questo criterio, trova la corrispondenza con una "d" seguita da uno o più caratteri alfanumerici. 
`\s` | Trova la corrispondenza con uno spazio vuoto.
 
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

## <a name="zerowidth-positive-lookahead-assertions"></a>Asserzioni lookahead positive di larghezza zero

Il costrutto di raggruppamento seguente definisce un'asserzione lookbehind positiva di larghezza zero:

**(?**=*sottoespressione*__)__

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari. Per trovare una corrispondenza, la stringa di input deve corrispondere al criterio di espressioni regolari in *sottoespressione*, sebbene la sottostringa corrispondente non venga inclusa nel risultato della corrispondenza. Un'asserzione lookahead positiva di larghezza zero non esegue il backtracking.

In genere, un'asserzione lookahead positiva di larghezza zero viene trovata alla fine di un criterio di ricerca di espressioni regolari Definisce una sottostringa che deve essere trovata alla fine di una stringa affinché venga stabilita una corrispondenza ma che non deve essere inclusa nella corrispondenza. È anche utile per impedire un backtracking eccessivo. È possibile usare un'asserzione lookahead positiva di larghezza zero per assicurarsi che un particolare gruppo acquisito inizi con il testo che corrisponde a un subset del criterio definito per tale gruppo acquisito. Se, ad esempio, viene trovata la corrispondenza di un gruppo di acquisizioni con caratteri alfanumerici consecutivi, è possibile usare un'asserzione positiva lookahead di larghezza zero per richiedere che il primo carattere sia un carattere alfabetico maiuscolo.

Nell'esempio seguente viene usata un'asserzione lookahead positiva di larghezza zero per trovare la corrispondenza con la parola che precede il verbo "is" nella stringa di input. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+(?=\sis\b)";
      string[] inputs = { "The dog is a Malamute.", 
                          "The island has beautiful birds.", 
                          "The pitch missed home plate.", 
                          "Sunday is a weekend day." };

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("'{0}' precedes 'is'.", match.Value);
         else
            Console.WriteLine("'{0}' does not match the pattern.", input); 
      }
   }
}
// The example displays the following output:
//    'dog' precedes 'is'.
//    'The island has beautiful birds.' does not match the pattern.
//    'The pitch missed home plate.' does not match the pattern.
//    'Sunday' precedes 'is'.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+(?=\sis\b)"
      Dim inputs() As String = { "The dog is a Malamute.", _
                                 "The island has beautiful birds.", _
                                 "The pitch missed home plate.", _
                                 "Sunday is a weekend day." }

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("'{0}' precedes 'is'.", match.Value)
         Else
            Console.WriteLine("'{0}' does not match the pattern.", input) 
         End If     
      Next
   End Sub
End Module
' The example displays the following output:
'       'dog' precedes 'is'.
'       'The island has beautiful birds.' does not match the pattern.
'       'The pitch missed home plate.' does not match the pattern.
'       'Sunday' precedes 'is'.
```

L'espressione regolare \b\w+(?=\sis\b) viene interpretata nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`(?=\sis\b)` | Determina se i caratteri alfanumerici vengono seguiti da uno spazio vuoto e dalla stringa "is", che termina su un confine di parola. In tal caso, la corrispondenza ha esito positivo.

## <a name="zerowidth-negative-lookahead-assertions"></a>Asserzioni lookahead negative di larghezza zero

Nel costrutto di raggruppamento seguente viene definita un'asserzione lookahead negativa di larghezza zero:

**(?!**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari. Per trovare una corrispondenza, la stringa di input non deve corrispondere al criterio di espressioni regolari in *sottoespressione*, sebbene la stringa corrispondente non venga inclusa nel risultato della corrispondenza. 

Un'asserzione lookahead negativa di larghezza zero viene usata in genere all'inizio o alla fine di un'espressione regolare. All'inizio di un'espressione regolare, può definire un criterio specifico per il quale non deve essere trovata una corrispondenza quando l'inizio dell'espressione regolare definisce un criterio simile ma più generale per cui stabilire la corrispondenza. In questo caso, viene spesso usata per limitare il backtracking. Alla fine di un'espressione regolare, può definire una sottoespressione che non può verificarsi alla fine di una corrispondenza. 

Nell'esempio seguente viene definita un'espressione regolare che usa un'asserzione lookahead di larghezza zero all'inizio dell'espressione regolare per trovare la corrispondenza con parole che non iniziano con "un". 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?!un)\w+\b";
      string input = "unite one unethical ethics use untie ultimate";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       one
//       ethics
//       use
//       ultimate
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?!un)\w+\b"
      Dim input As String = "unite one unethical ethics use untie ultimate"
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       one
'       ethics
'       use
'       ultimate
```

L'espressione regolare \b(?!un)\w+\b viene interpretata nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(?!un)` | Determina se i due caratteri successivi sono "un". Se non lo sono, è possibile stabilire la corrispondenza.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`\b` | Termina la corrispondenza sul confine di parola.
 
Nell'esempio seguente viene definita un'espressione regolare che usa un'asserzione lookahead di larghezza zero alla fine dell'espressione regolare per trovare la corrispondenza con parole che non terminano con un carattere di punteggiatura.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+\b(?!\p{P})";
      string input = "Disconnected, disjointed thoughts in a sentence fragment.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       disjointed
//       thoughts
//       in
//       a
//       sentence
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+\b(?!\p{P})"
      Dim input As String = "Disconnected, disjointed thoughts in a sentence fragment."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       disjointed
'       thoughts
'       in
'       a
'       sentence
```

L'espressione regolare `\b\w+\b(?!\p{P})` viene interpretata come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`\b` | Termina la corrispondenza sul confine di parola.
`\p{P})` | Se il carattere successivo non è un simbolo di punteggiatura (quale un punto o una virgola), la corrispondenza ha esito positivo.
 
## <a name="zerowidth-positive-lookbehind-assertions"></a>Asserzioni lookbehind positive di larghezza zero

Nel costrutto di raggruppamento seguente viene definita un'asserzione lookbehind positiva di larghezza zero:

**(?<=**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari. Per trovare una corrispondenza, *sottoespressione* deve trovarsi nella stringa di input a sinistra della posizione corrente, sebbene la sottoespressione non venga inclusa nel risultato della corrispondenza. Un'asserzione lookbehind positiva di larghezza zero non esegue il backtracking.

Le asserzioni lookbehind positive di larghezza zero vengono usate in genere all'inizio delle espressioni regolari. Il criterio definito è una precondizione per una corrispondenza, anche se non fa parte del risultato della corrispondenza. 

Ad esempio, nell'esempio seguente viene cercata la corrispondenza con le ultime due cifre dell'anno per il ventunesimo secolo ovvero, richiede che la cifra "20" preceda la stringa corrispondente.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "2010 1999 1861 2140 2009";
      string pattern = @"(?<=\b20)\d{2}\b";

      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       10
//       09
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "2010 1999 1861 2140 2009"
      Dim pattern As String = "(?<=\b20)\d{2}\b"

      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next      
   End Sub
End Module
' The example displays the following output:
'       10
'       09
```

Il criterio di ricerca di espressioni regolari `(?<=\b20)\d{2}\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\d{2}` | Trova la corrispondenza con due cifre decimali.
`{?<=\b20)` | Continua la corrispondenza per verificare se le due cifre decimali sono precedute dalle cifre decimali "20" su un confine di parola.
`\b` | Termina la corrispondenza sul confine di parola.
 
Le asserzioni lookbehind positive di larghezza zero vengono usate anche per limitare il backtracking quando l'ultimo carattere o gli ultimi caratteri in un gruppo acquisito devono essere costituiti da un subset di caratteri corrispondenti al criterio di ricerca di espressioni regolari di tale gruppo. Se, ad esempio, un gruppo acquisisce tutti i caratteri alfanumerici consecutivi, è possibile usare un'asserzione positiva lookbehind di larghezza zero per richiedere che l'ultimo carattere sia un carattere alfabetico. 

## <a name="zerowidth-negative-lookbehind-assertions"></a>Asserzioni lookbehind negative di larghezza zero

Nel costrutto di raggruppamento seguente viene definita un'asserzione lookbehind negativa di larghezza zero:

**(?<!**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari. Per trovare una corrispondenza, *sottoespressione* non deve trovarsi nella stringa di input a sinistra della posizione corrente. Tuttavia, qualsiasi sottostringa che non corrisponde a sottoespressione non viene inclusa nel risultato della corrispondenza.

Le asserzioni lookbehind negative di larghezza zero vengono usate in genere all'inizio delle espressioni regolari. Il criterio definito preclude una corrispondenza nella stringa che segue. Queste asserzioni vengono usate anche per limitare il backtracking quando l'ultimo carattere o gli ultimi caratteri in un gruppo acquisito non devono essere costituiti da uno o più caratteri corrispondenti al criterio di ricerca di espressioni regolari di tale gruppo. Se, ad esempio, un gruppo acquisisce tutti i caratteri alfanumerici consecutivi, è possibile usare un'asserzione positiva lookbehind di larghezza zero per richiedere che l'ultimo carattere non sia un carattere di sottolineatura (_).

Nell'esempio seguente viene cercata la corrispondenza della data per qualsiasi giorno della settimana diverso da un fine settimana (ovvero, che non è né sabato né domenica). 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] dates = { "Monday February 1, 2010", 
                         "Wednesday February 3, 2010", 
                         "Saturday February 6, 2010", 
                         "Sunday February 7, 2010", 
                         "Monday, February 8, 2010" };
      string pattern = @"(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b";

      foreach (string dateValue in dates)
      {
         Match match = Regex.Match(dateValue, pattern);
         if (match.Success)
            Console.WriteLine(match.Value);
      }      
   }
}
// The example displays the following output:
//       February 1, 2010
//       February 3, 2010
//       February 8, 2010
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim dates() As String = { "Monday February 1, 2010", _
                                "Wednesday February 3, 2010", _
                                "Saturday February 6, 2010", _
                                "Sunday February 7, 2010", _
                                "Monday, February 8, 2010" }
      Dim pattern As String = "(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b"

      For Each dateValue As String In dates
         Dim match As Match = Regex.Match(dateValue, pattern)
         If match.Success Then
            Console.WriteLine(match.Value)
         End If   
      Next      
   End Sub
End Module
' The example displays the following output:
'       February 1, 2010
'       February 3, 2010
'       February 8, 2010
```

Il criterio di ricerca di espressioni regolari `(?<!(Saturday|Sunday) )\b\w+ \d{1,2}, \d{4}\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`\w+` | Trova la corrispondenza con uno o più caratteri alfanumerici seguiti da uno spazio vuoto.
`\d{1,2},` | Trova la corrispondenza con una o due cifre digitali seguite da uno spazio vuoto e da una virgola.
`\d{4}\b` | Trova la corrispondenza di quattro cifre digitali e termina la corrispondenza sul confine di parola.
'(?<! (Sabato|Domenica) )' | Se la corrispondenza viene preceduta da un elemento diverso dalle stringhe "Saturday" o "Sunday" seguito da uno spazio, la corrispondenza ha esito positivo.

## <a name="nonbacktracking-subexpressions"></a>Sottoespressioni di non backtracking

Nel costrutto di raggruppamento seguente viene rappresentata una sottoespressione di non backtracking (nota anche come sottoespressione "greedy"):

**(?>**_sottoespressione_**)**

dove *sottoespressione* è un qualsiasi criterio di espressioni regolari.

Normalmente, se un'espressione regolare include un criterio di ricerca facoltativo o alternativo e una corrispondenza ha esito negativo, il motore delle espressioni regolari può creare un ramo in più direzioni per trovare la corrispondenza di una stringa di input con un criterio. Se non viene trovata una corrispondenza quando viene esaminato il primo ramo, il motore delle espressioni regolari può tornare, o eseguire il backtracking, al punto in cui ha trovato la prima corrispondenza e tenta la corrispondenza usando il secondo ramo. Questo processo può continuare fino a che non sono stati provati tutti i rami.

Il costrutto di linguaggio **(?>**_sottoespressione_**)** disabilita il backtracking. Il motore delle espressioni regolari troverà la corrispondenza con il numero massimo possibile di caratteri nella stringa di input. Quando non sarà più possibile trovare altre corrispondenze, non eseguirà il backtracking per trovare corrispondenze alternative con i criteri. Viene pertanto trovata la corrispondenza della sottoespressione solo con stringhe corrispondenti esclusivamente alla sottoespressione; non tenta di trovare una corrispondenza per una stringa in base alla sottoespressione e a qualsiasi sottoespressione successiva. 

Questa opzione è consigliata solo se si è certi che il backtracking avrà esito negativo. Impedendo al motore delle espressioni regolari di eseguire ricerche non necessarie si registra un miglioramento delle prestazioni. 

Nell'esempio seguente viene illustrato come una sottoespressione di non backtracking modifica i risultati dei criteri di ricerca. L'espressione regolare di backtracking trova una corrispondenza per una serie di caratteri ripetuti seguiti da una o più occorrenze dello stesso carattere su un confine di parola, diversamente dall'espressione regolare di non backtracking. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "cccd.", "aaad", "aaaa" };
      string back = @"(\w)\1+.\b";
      string noback = @"(?>(\w)\1+).\b";

      foreach (string input in inputs)
      {
         Match match1 = Regex.Match(input, back);
         Match match2 = Regex.Match(input, noback);
         Console.WriteLine("{0}: ", input);

         Console.Write("   Backtracking : ");
         if (match1.Success)
            Console.WriteLine(match1.Value);
         else
            Console.WriteLine("No match");

         Console.Write("   Nonbacktracking: ");
         if (match2.Success)
            Console.WriteLine(match2.Value);
         else
            Console.WriteLine("No match");
      }
   }
}
// The example displays the following output:
//    cccd.:
//       Backtracking : cccd
//       Nonbacktracking: cccd
//    aaad:
//       Backtracking : aaad
//       Nonbacktracking: aaad
//    aaaa:
//       Backtracking : aaaa
//       Nonbacktracking: No match
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "cccd.", "aaad", "aaaa" }
      Dim back As String = "(\w)\1+.\b"
      Dim noback As String = "(?>(\w)\1+).\b"

      For Each input As String In inputs
         Dim match1 As Match = Regex.Match(input, back)
         Dim match2 As Match = Regex.Match(input, noback)
         Console.WriteLine("{0}: ", input)

         Console.Write("   Backtracking : ")
         If match1.Success Then
            Console.WriteLine(match1.Value)
         Else
            Console.WriteLine("No match")
         End If

         Console.Write("   Nonbacktracking: ")
         If match2.Success Then
            Console.WriteLine(match2.Value)
         Else
            Console.WriteLine("No match")
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'    cccd.:
'       Backtracking : cccd
'       Nonbacktracking: cccd
'    aaad:
'       Backtracking : aaad
'       Nonbacktracking: aaad
'    aaaa:
'       Backtracking : aaaa
'       Nonbacktracking: No match
```

L'espressione regolare di non backtracking `(?>(\w)\1+).\b` è definita nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`(\w)` | Trova la corrispondenza di un singolo carattere alfanumerico e la assegna al primo gruppo di acquisizione.
`\1+` | Trova la corrispondenza con il valore della prima sottostringa acquisita una o più volte.
`.` | Trova la corrispondenza con qualsiasi carattere.
`\b` | Termina la corrispondenza sul confine di parola.
`(?>(\w)\1+)` | Trova una o più occorrenze di un carattere alfanumerico duplicato ma non esegue il backtracking per trovare la corrispondenza con l'ultimo carattere su un confine di parola.
 
## <a name="grouping-constructs-and-regular-expression-objects"></a>Costrutti di raggruppamento e oggetti di espressione regolare

Le sottostringhe corrispondenti a un gruppo di acquisizione di espressioni regolari sono rappresentate da oggetti [System.Text.RegularExpressions.Group](xref:System.Text.RegularExpressions.Group), che possono essere recuperati dall'oggetto [System.Text.RegularExpressions.GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups). L'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) è popolato nel modo seguente:

* Il primo oggetto [Group](xref:System.Text.RegularExpressions.Group) della raccolta (in corrispondenza dell'indice zero) rappresenta l'intera corrispondenza.

* Il set di oggetti [Group](xref:System.Text.RegularExpressions.Group) successivo rappresenta i gruppi di acquisizione non denominati (numerati). Vengono visualizzati nell'ordine in cui sono definiti nell'espressione regolare, da sinistra a destra. I valori di indice di questi gruppi sono compresi tra 1 e il numero dei gruppi di acquisizione non denominati nella raccolta. L'indice di un gruppo specifico è equivalente al relativo backreference numerato. Per altre informazioni sui backreference, vedere [Costrutti di backreference nelle espressioni regolari](backreference.md)

* Il set di oggetti [Group](xref:System.Text.RegularExpressions.Group) finale rappresenta i gruppi di acquisizione denominati. Vengono visualizzati nell'ordine in cui sono definiti nell'espressione regolare, da sinistra a destra. Il valore di indice del primo gruppo di acquisizione denominato è maggiore di uno rispetto all'ultimo gruppo di acquisizione non denominato. Se l'espressione regolare non contiene gruppi di acquisizione non denominati, il valore di indice del primo gruppo di acquisizione denominato è uno. 


Se si applica un quantificatore a un gruppo di acquisizione, le proprietà [Capture.Value](xref:System.Text.RegularExpressions.Capture.Value), [Capture.Index](xref:System.Text.RegularExpressions.Capture.Index) e [Capture.Length](xref:System.Text.RegularExpressions.Capture.Length) dell'oggetto [Group](xref:System.Text.RegularExpressions.Group) corrispondente riflettono l'ultima sottostringa acquisita da un gruppo di acquisizione. È possibile recuperare un set completo di sottostringhe acquisite da gruppi che hanno quantificatori dall'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) restituito dalla proprietà [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures).

Nell'esempio seguente viene illustrata la relazione tra gli oggetti [Group](xref:System.Text.RegularExpressions.Group) e [Capture](xref:System.Text.RegularExpressions.Capture). 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\b(\w+)\W+)+";
      string input = "This is a short sentence.";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}'", match.Value);
      for (int ctr = 1; ctr < match.Groups.Count; ctr++)
      {
         Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups[ctr].Value);
         int capCtr = 0;
         foreach (Capture capture in match.Groups[ctr].Captures)
         {
            Console.WriteLine("      Capture {0}: '{1}'", capCtr, capture.Value);
            capCtr++;
         }
      }
   }
}
// The example displays the following output:
//       Match: 'This is a short sentence. '
//          Group 1: 'sentence.'
//             Capture 0: 'This '
//             Capture 1: 'is '
//             Capture 2: 'a '
//             Capture 3: 'short '
//             Capture 4: 'sentence.'
//          Group 2: 'sentence'
//             Capture 0: 'This'
//             Capture 1: 'is'
//             Capture 2: 'a'
//             Capture 3: 'short'
//             Capture 4: 'sentence'
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\b(\w+)\W+)+"
      Dim input As String = "This is a short sentence."
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}'", match.Value)
      For ctr As Integer = 1 To match.Groups.Count - 1
         Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups(ctr).Value)
         Dim capCtr As Integer = 0
         For Each capture As Capture In match.Groups(ctr).Captures
            Console.WriteLine("      Capture {0}: '{1}'", capCtr, capture.Value)
            capCtr += 1
         Next
      Next
   End Sub
End Module
' The example displays the following output:
'       Match: 'This is a short sentence.'
'          Group 1: 'sentence.'
'             Capture 0: 'This '
'             Capture 1: 'is '
'             Capture 2: 'a '
'             Capture 3: 'short '
'             Capture 4: 'sentence.'
'          Group 2: 'sentence'
'             Capture 0: 'This'
'             Capture 1: 'is'
'             Capture 2: 'a'
'             Capture 3: 'short'
'             Capture 4: 'sentence'
```

Il criterio di ricerca di espressioni regolari `\b(\w+)\W+)+` estrae singole parole da una stringa e viene definito come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Insieme, questi caratteri formano una parola. Equivale al secondo gruppo di acquisizione.
`\W+` | Trova la corrispondenza di uno o più caratteri non alfanumerici.
`(\w+)\W+)+` | Trova la corrispondenza con il criterio di uno o più caratteri alfanumerici seguiti da uno o più caratteri non alfanumerici, una o più volte. Equivale al primo gruppo di acquisizione.
 
Il primo gruppo di acquisizione trova la corrispondenza per ogni parola della frase. Il secondo gruppo di acquisizione trova la corrispondenza per ogni parola insieme alla punteggiatura e allo spazio vuoto che seguono la parola. L'oggetto [Group](xref:System.Text.RegularExpressions.Group) il cui indice è 2 offre informazioni sul testo corrispondente in base al secondo gruppo di acquisizione. Il set completo di parole acquisite dal gruppo di acquisizione è disponibile dall'oggetto [CaptureCollection](xref:System.Text.RegularExpressions.CaptureCollection) restituito dalla proprietà [Group.Captures](xref:System.Text.RegularExpressions.Group.Captures).

## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)

[Backtracking nelle espressioni regolari](backtracking.md)



<!--HONumber=Nov16_HO1-->


