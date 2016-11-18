---
title: Costrutti di backreference nelle espressioni regolari
description: Costrutti di backreference nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: c453ed78-650f-4c3c-9ab4-9d89d250bf88
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 757c8c4e71bbafb12c8add925723daf1a24e06d1

---

# <a name="backreference-constructs-in-regular-expressions"></a>Costrutti di backreference nelle espressioni regolari

I backreference sono uno strumento utile per identificare un carattere ripetuto o una sottostringa all'interno di una stringa. Se la stringa di input contiene ad esempio più occorrenze di una sottostringa arbitraria, è possibile trovare la prima occorrenza con un gruppo di acquisizione e usare un backreference per trovare le occorrenze successive della sottostringa. 

> [!NOTE]
> Per fare riferimento a gruppi di acquisizione denominati e numerati in stringhe sostitutive, si usa una sintassi separata. Per altre informazioni, vedere [Sostituzioni nelle espressioni regolari](substitutions.md).
 
.NET definisce elementi di linguaggio separati per fare riferimento a gruppi di acquisizione denominati e numerati. Per altre informazioni sui gruppi di acquisizione, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

## <a name="numbered-backreferences"></a>Backreference numerati

Nei backreference numerati si usa la sintassi seguente:

**\**_numero_

dove *numero* è la posizione corretta del gruppo di acquisizione nell'espressione regolare. Ad esempio, `\4` corrisponde al contenuto del quarto gruppo di acquisizione. Se nel modello di espressione regolare *numero* non è definito, si verifica un errore di analisi e il motore delle espressioni regolari genera un'eccezione [ArgumentException](xref:System.ArgumentException). Ad esempio, l'espressione regolare `\b(\w+)\s\1` è valida, poiché `(\w+)` è il primo e l'unico gruppo di acquisizione nell'espressione. D'altra parte, `\b(\w+)\s\2` non è un'espressione valida e genera un'eccezione di argomento, perché non esistono gruppi di acquisizione numerati `\2`.

Si noti l'ambiguità tra i codici di escape ottale, ad esempio `\16`, e i backreference **\**_numero_ che usano la stessa notazione. Questa ambiguità viene risolta nel modo seguente:

* Le espressioni da `\1` a `\9` vengono sempre interpretate come backreference e non come codici ottali.

* Se la prima cifra di un'espressione composta da più cifre è 8 o 9, ad esempio `\80` o `\91`, l'espressione viene interpretata come valore letterale.

* Le espressioni con numerazione a partire da `\10` vengono considerate backreference se esiste un backreference a tale numero; in caso contrario, vengono interpretate come codici ottali.

* Se l'espressione regolare contiene un backreference a un numero di gruppo non definito, si verifica un errore di analisi e il motore delle espressioni regolari genera un'eccezione [ArgumentException](xref:System.ArgumentException).

Se il problema è dovuto all'ambiguità, è possibile usare la notazione **\k<**_nome_**>** che, non essendo ambigua, non può essere confusa con codici di caratteri ottali. Analogamente, i codici esadecimale come `\xdd` non sono ambigui e non possono essere confusi con backreference.

L'esempio seguente consente di trovare caratteri alfanumerici doppi all'interno di una stringa. Viene definita un'espressione regolare `(\w)\1,` costituita dagli elementi seguenti.

Elemento | Descrizione
------- | -----------
`(\w)` | Trova la corrispondenza di un carattere alfanumerico e la assegna al primo gruppo di acquisizione.
`\1` | Trova la corrispondenza del carattere successivo, uguale al valore del primo gruppo di acquisizione.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w)\1";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w)\1"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

## <a name="named-backreferences"></a>Backreference denominati

Per definire un backreference denominato, usare la sintassi seguente:

**\k<**_nome_**>**

oppure:

**\k'**_nome_**'**

dove *nome* è il nome di un gruppo di acquisizione definito nel modello di espressione regolare. Se nel modello di espressione regolare *nome* non è definito, si verifica un errore di analisi e il motore delle espressioni regolari genera un'eccezione [ArgumentException](xref:System.ArgumentException).

L'esempio seguente consente di trovare caratteri alfanumerici doppi all'interno di una stringa. Viene definita un'espressione regolare `(?<char>\w)\k<char>` costituita dagli elementi seguenti.

Elemento | Descrizione
------- | -----------
`(?<char>\w)` | Trova la corrispondenza di un carattere alfanumerico e la assegna a un gruppo di acquisizione denominato char.
`\k<char>` | Trova la corrispondenza del carattere successivo, uguale al valore del gruppo di acquisizione denominato char.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<char>\w)\k<char>";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<char>\w)\k<char>"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

Si noti che *nome* può anche essere la rappresentazione di stringa di un numero. Nell'esempio seguente viene usata l'espressione regolare `(?<2>\w)\k<2>` per trovare caratteri alfanumerici doppi all'interno di una stringa.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<2>\w)\k<2>";
      string input = "trellis llama webbing dresser swagger";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("Found '{0}' at position {1}.", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Found 'll' at position 3.
//       Found 'll' at position 8.
//       Found 'bb' at position 16.
//       Found 'ss' at position 25.
//       Found 'gg' at position 33.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<2>\w)\k<2>"
      Dim input As String = "trellis llama webbing dresser swagger"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Found '{0}' at position {1}.", _
                           match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Found 'll' at position 3.
'       Found 'll' at position 8.
'       Found 'bb' at position 16.
'       Found 'ss' at position 25.
'       Found 'gg' at position 33.
```

## <a name="what-backreferences-match"></a>Corrispondenza dei backreference

Un backreference fa riferimento alla definizione più recente di un gruppo, vale a dire alla definizione all'estrema sinistra, in caso di corrispondenza da sinistra a destra. Quando un gruppo esegue più acquisizioni, un backreference fa riferimento all'acquisizione più recente. 

L'esempio seguente include un modello di espressione regolare `(?<1>a)(?<1>\1b)*`, che ridefinisce il gruppo denominato \1. Nella tabella seguente sono descritti i modelli di espressione regolare. 

Criterio | Descrizione
------- | -----------
`(?<1>a)` | Trova la corrispondenza del carattere "a" e assegna il risultato al gruppo di acquisizione denominato 1.
`(?<1>\1b)*` |Trova la corrispondenza dell'occorrenza 0 o 1 del gruppo denominato 1 con una "b" e assegna il risultato al gruppo di acquisizione denominato 1. 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(?<1>a)(?<1>\1b)*";
      string input = "aababb";
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine("Match: " + match.Value);
         foreach (Group group in match.Groups)
            Console.WriteLine("   Group: " + group.Value);
      }
   }
}
// The example displays the following output:
//          Group: aababb
//          Group: abb
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(?<1>a)(?<1>\1b)*"
      Dim input As String = "aababb"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("Match: " + match.Value)
         For Each group As Group In match.Groups
            Console.WriteLIne("   Group: " + group.Value)
         Next
      Next
   End Sub
End Module
' The example display the following output:
'          Group: aababb
'          Group: abb
```

Confrontando l'espressione regolare con la stringa di input ("aababb"), il motore delle espressioni regolari esegue le operazioni seguenti:

1. Parte dall'inizio della stringa e trova una corrispondenza per "a" con l'espressione `(?<1>a)`. Il valore del 1 gruppo è ora "a".

2. Passa al secondo carattere e trova una corrispondenza per la stringa "ab" con l'espressione `\1b` o "ab". Assegna il risultato "ab" a `\1`.

3. Passa al quarto carattere. Per l'espressione `(?<1>\1b)` la corrispondenza individuata deve essere zero o più volte, ai fini di una corrispondenza corretta della stringa "abb" con l'espressione `\1b`. Assegna il risultato "abb" nuovamente a `\1`.

In questo esempio \* è un quantificatore di cicli, vale a dire che viene eseguito ripetutamente finché il motore delle espressioni regolari non trova una corrispondenza con il modello che definisce. I quantificatori di cicli non cancellano le definizioni di gruppi.

Se un gruppo non ha acquisito alcuna sottostringa, un backreference a tale gruppo risulterà non definito e non troverà mai corrispondenza. Questo comportamento è illustrato dal modello delle espressioni regolari `\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b,`, definito nel modo seguente:

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza sul confine di parola.
`(\p{Lu}{2})` | Trova la corrispondenza di due maiuscole. Equivale al primo gruppo di acquisizione.
`(\d{2})?` | Trova la corrispondenza di zero o di una occorrenza di due cifre decimali. Equivale al secondo gruppo di acquisizione.
`(\p{Lu}{2})` | Trova la corrispondenza di due maiuscole. Equivale al terzo gruppo di acquisizione.
`\b` | Termina la corrispondenza sul confine di parola.

Una stringa di input può corrispondere a questa espressione regolare, anche se le due cifre decimali definite dal secondo gruppo di acquisizione non sono presenti. L'esempio seguente illustra che, nonostante una corrispondenza corretta, viene individuato un gruppo di acquisizione vuoto tra due gruppi di acquisizione con corrispondenza corretta.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b";
      string[] inputs = { "AA22ZZ", "AABB" };
      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success)
         {
            Console.WriteLine("Match in {0}: {1}", input, match.Value);
            if (match.Groups.Count > 1)
            {
               for (int ctr = 1; ctr <= match.Groups.Count - 1; ctr++)
               {
                  if (match.Groups[ctr].Success)
                     Console.WriteLine("Group {0}: {1}", 
                                       ctr, match.Groups[ctr].Value);
                  else
                     Console.WriteLine("Group {0}: <no match>", ctr);
               }
            }
         }
         Console.WriteLine();
      }      
   }
}
// The example displays the following output:
//       Match in AA22ZZ: AA22ZZ
//       Group 1: AA
//       Group 2: 22
//       Group 3: ZZ
//       
//       Match in AABB: AABB
//       Group 1: AA
//       Group 2: <no match>
//       Group 3: BB
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\p{Lu}{2})(\d{2})?(\p{Lu}{2})\b"
      Dim inputs() As String = { "AA22ZZ", "AABB" }
      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("Match in {0}: {1}", input, match.Value)
            If match.Groups.Count > 1 Then
               For ctr As Integer = 1 To match.Groups.Count - 1
                  If match.Groups(ctr).Success Then
                     Console.WriteLine("Group {0}: {1}", _
                                       ctr, match.Groups(ctr).Value)
                  Else
                     Console.WriteLine("Group {0}: <no match>", ctr)
                  End If      
               Next
            End If
         End If
         Console.WriteLine()
      Next      
   End Sub
End Module
' The example displays the following output:
'       Match in AA22ZZ: AA22ZZ
'       Group 1: AA
'       Group 2: 22
'       Group 3: ZZ
'       
'       Match in AABB: AABB
'       Group 1: AA
'       Group 2: <no match>
'       Group 3: BB
```

## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)




<!--HONumber=Nov16_HO3-->


