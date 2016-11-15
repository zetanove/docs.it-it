---
title: Costrutti vari nelle espressioni regolari
description: Costrutti vari nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 478901dc-db6c-4d90-9d3b-f5cfdca2cbf5
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 477332f4009790727686aa3d91e35509e3766903

---

# <a name="miscellaneous-constructs-in-regular-expressions"></a>Costrutti vari nelle espressioni regolari


Le espressioni regolari in .NET includono tre costrutti vari di linguaggio. Uno consente di abilitare o disabilitare opzioni di corrispondenza specifiche all'interno di un modello dell'espressione regolare. I restanti due consentono di includere commenti in un'espressione regolare.

## <a name="inline-options"></a>Opzioni inline

È possibile impostare o disabilitare opzioni di corrispondenza specifiche del modello per una parte di espressione regolare usando la sintassi

```
(?imnsx-imnsx)
```

Elencare le opzioni da abilitare dopo il punto interrogativo e le opzioni da disabilitare dopo il segno di sottrazione. Nella tabella seguente viene descritta ciascuna opzione. Per altre informazioni su ciascuna opzione, vedere [Opzioni di espressioni regolari](options.md).

Opzione | Descrizione
------ | ----------- 
**i** | Corrispondenza senza distinzione tra maiuscole e minuscole.
**m** | Modalità multiriga.
**n** | Solo acquisizioni esplicite. Le parentesi non fungono da gruppi di acquisizione.
**s** | Modalità a riga singola.
**x** | Ignora gli spazi vuoti senza escape e consente commenti in modalità X. 
 
Qualsiasi modifica nelle opzioni dell'espressione regolare definita dal costrutto **(?imnsx-imnsx)** rimane attiva fino alla fine del gruppo di inclusione.

> [!NOTE]
> Il costrutto di raggruppamento **(?imnsx-imnsx**:_subexpression_**)** offre la stessa funzionalità per una sottoespressione. Per altre informazioni, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).
 
Nell'esempio seguente vengono usate le opzioni **i**, **n** e **x** per disabilitare la distinzione tra maiuscole e minuscole e abilitare le acquisizioni esplicite, nonché per ignorare lo spazio vuoto nel modello dell'espressione regolare all'interno di un'espressione regolare. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern; 
      string input = "double dare double Double a Drooling dog The Dreaded Deep";

      pattern = @"\b(D\w+)\s(d\w+)\b";
      // Match pattern using default options.
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
            for (int ctr = 1; ctr < match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
      }
      Console.WriteLine();

      // Change regular expression pattern to include options.
      pattern = @"\b(D\w+)(?ixn) \s (d\w+) \b";
      // Match new pattern with options. 
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
            for (int ctr = 1; ctr < match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups[ctr].Value);
      }
   }
}
// The example displays the following output:
//       Drooling dog
//          Group 1: Drooling
//          Group 2: dog
//       
//       Drooling dog
//          Group 1: 'Drooling'
//       Dreaded Deep
//          Group 1: 'Dreaded'
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String 
      Dim input As String = "double dare double Double a Drooling dog The Dreaded Deep"

      pattern = "\b(D\w+)\s(d\w+)\b"
      ' Match pattern using default options.
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
      Console.WriteLine()

      ' Change regular expression pattern to include options.
      pattern = "\b(D\w+)(?ixn) \s (d\w+) \b"
      ' Match new pattern with options. 
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: '{1}'", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'       Drooling dog
'          Group 1: Drooling
'          Group 2: dog
'       
'       Drooling dog
'          Group 1: 'Drooling'
'       Dreaded Deep
'          Group 1: 'Dreaded'
```

Nell'esempio vengono definite due espressioni regolari. La prima, `\b(D\w+)\s(d\w+)\b`, corrisponde a due parole consecutive che iniziano con una "D" maiuscola e una "d" minuscola. La seconda espressione regolare, `\b(D\w+)(?ixn) \s (d\w+) \b`, usa opzioni inline per modificare questo modello, come descritto nella tabella seguente. Confrontando i risultati viene confermato l'effetto del costrutto `(?ixn)`.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`(D\w+)` | Trovare la corrispondenza di una "D" maiuscola seguita da uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`(?ixn)` | Da questo momento eseguire confronti senza distinzione tra maiuscole e minuscole, eseguire solo acquisizioni esplicite e ignorare gli spazi vuoti nel modello dell'espressione regolare.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(d\w+)` | Trovare la corrispondenza di una "d" minuscola seguita da uno o più caratteri alfanumerici. Questo gruppo non viene acquisito perché è stata abilitata l'opzione n (acquisizione esplicita).
`\b` | Trova la corrispondenza di un confine di parola.
 
## <a name="inline-comment"></a>Commento inline

Il costrutto **(?#** _comment_**)** consente di includere un commento inline in un'espressione regolare. Il motore delle espressioni regolari non usa una parte del commento nella corrispondenza tra modelli, anche se il commento è incluso nella stringa restituita dal metodo [Regex.ToString](xref:System.Text.RegularExpressions.Regex.Unescape(System.String)). Il commento termina in corrispondenza della prima parentesi chiusa.

Nell'esempio seguente viene ripetuto il primo criterio dell'espressione regolare dell'esempio nella sezione precedente. Vengono aggiunti due commenti inline all'espressione regolare per indicare se il confronto fa distinzione tra maiuscole e minuscole. Il modello dell'espressione regolare, `\b((?# case-sensitive comparison)D\w+)\s((?#case-insensitive comparison)d\w+)\b`, viene definito nel modo seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`(?# case-sensitive comparison)` | Un commento. Non influisce sul comportamento della corrispondenza tra modelli.
`(D\w+)` | Trovare la corrispondenza di una "D" maiuscola seguita da uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`(?ixn)` |Da questo momento eseguire confronti senza distinzione tra maiuscole e minuscole, eseguire solo acquisizioni esplicite e ignorare gli spazi vuoti nel modello dell'espressione regolare.
`(?#case-insensitive comparison)` | Un commento. Non influisce sul comportamento della corrispondenza tra modelli. 
`(d\w+)` | Trovare la corrispondenza di una "d" minuscola seguita da uno o più caratteri alfanumerici. Equivale al secondo gruppo di acquisizione.
`\b` | Trova la corrispondenza di un confine di parola.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comparison)d\w+)\b";
      Regex rgx = new Regex(pattern);
      string input = "double dare double Double a Drooling dog The Dreaded Deep";

      Console.WriteLine("Pattern: " + pattern.ToString());
      // Match pattern using default options.
      foreach (Match match in rgx.Matches(input))
      {
         Console.WriteLine(match.Value);
         if (match.Groups.Count > 1)
         {
            for (int ctr = 1; ctr <match.Groups.Count; ctr++) 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups[ctr].Value);
         }
      }
   }
}
// The example displays the following output:
//    Pattern: \b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comp
//    arison)d\w+)\b
//    Drooling dog
//       Group 1: Drooling
//    Dreaded Deep
//       Group 1: Dreaded
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comparison)d\w+)\b"
      Dim rgx As New Regex(pattern)
      Dim input As String = "double dare double Double a Drooling dog The Dreaded Deep"

      Console.WriteLine("Pattern: " + pattern.ToString())
      ' Match pattern using default options.
      For Each match As Match In rgx.Matches(input)
         Console.WriteLine(match.Value)
         If match.Groups.Count > 1 Then
            For ctr As Integer = 1 To match.Groups.Count - 1 
               Console.WriteLine("   Group {0}: {1}", ctr, match.Groups(ctr).Value)
            Next
         End If
      Next
   End Sub
End Module
' The example displays the following output:
'    Pattern: \b((?# case sensitive comparison)D\w+)\s(?ixn)((?#case insensitive comp
'    arison)d\w+)\b
'    Drooling dog
'       Group 1: Drooling
'    Dreaded Deep
'       Group 1: Dreaded
```

## <a name="endofline-comment"></a>Commento di fine riga

Un simbolo di cancelletto (**#**) contrassegna un commento in modalità X, che inizia in corrispondenza del carattere senza escape # alla fine del modello dell'espressione regolare e continua fino alla fine della riga. Per usare questo costrutto, è necessario abilitare l'opzione **x** (mediante opzioni inline) o specificare il valore [RegexOptions. IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace) per il parametro *option* quando si crea l'istanza dell'oggetto [Regex](xref:System.Text.RegularExpressions.Regex) o si chiama un metodo statico [Regex](xref:System.Text.RegularExpressions.Regex). 

L'esempio seguente illustra il costrutto del commento di fine riga. Determina se una stringa è una stringa di formato composito che include almeno un elemento di formato. La tabella seguente descrive i costrutti nel modello dell'espressione regolare: 

`\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item`. 

Criterio | Descrizione
------- | ----------- 
`\{` | Trovare la corrispondenza con una parentesi graffa di apertura.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
`(,-*\d+)*` | Trovare la corrispondenza con zero o una occorrenza di una virgola, seguita da un segno di sottrazione, seguito da una o più cifre decimali.
`(\:\w{1,4}?)*` | Trovare la corrispondenza con zero o una occorrenza del segno di due punti, seguito dal numero minimo possibile di caratteri di spazio vuoto tra uno e quattro.
`(?#case insensitive comparison)` | Un commento inline. Non ha effetto sul comportamento della corrispondenza tra modelli.
`\}` | Trovare la corrispondenza con una parentesi graffa di chiusura.
`(?x)` | Abilitare l'opzione per ignorare gli spazi vuoti nel modello in modo che il commento di fine riga venga riconosciuto.
`# Looks for a composite format item.` | Un commento di fine riga.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item.";
      string input = "{0,-3:F}";
      Console.WriteLine("'{0}':", input);
      if (Regex.IsMatch(input, pattern))
         Console.WriteLine("   contains a composite format item.");
      else
         Console.WriteLine("   does not contain a composite format item.");
   }
}
// The example displays the following output:
//       '{0,-3:F}':
//          contains a composite format item.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\{\d+(,-*\d+)*(\:\w{1,4}?)*\}(?x) # Looks for a composite format item."
      Dim input As String = "{0,-3:F}"
      Console.WriteLine("'{0}':", input)
      If Regex.IsMatch(input, pattern) Then
         Console.WriteLine("   contains a composite format item.")
      Else
         Console.WriteLine("   does not contain a composite format item.")
      End If
   End Sub
End Module
' The example displays the following output:
'       '{0,-3:F}':
'          contains a composite format item.
```

Si noti che, anziché specificare il costrutto `(?x)` nell'espressione regolare, il commento può anche essere riconosciuto chiamando il metodo [Regex.IsMatch(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) e passando il valore di enumerazione [RegexOptions.IgnorePatternWhitespace](xref:System.Text.RegularExpressions.RegexOptions.IgnorePatternWhitespace).

## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)




<!--HONumber=Nov16_HO1-->


