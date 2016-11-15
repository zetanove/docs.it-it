---
title: Sostituzioni nelle espressioni regolari
description: Sostituzioni nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 0fded615-1021-4468-a644-b491814305c6
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 3e02d18d6566c67c7fff7003671f340f97b0dfce

---

# <a name="substitutions-in-regular-expressions"></a>Sostituzioni nelle espressioni regolari

Le sostituzioni sono elementi di linguaggio riconosciuti solo all'interno dei criteri di sostituzione. Utilizzano un modello di espressione regolare per definire in tutto o in parte il testo che sostituirà il testo corrispondente nella stringa di input. Il criterio di sostituzione può essere costituito da una o più sostituzioni insieme a caratteri letterali. I criteri di sostituzione vengono offerti agli overload del metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) che possiedono un parametro *replacement* e al metodo [Match.Result](xref:System.Text.RegularExpressions.Match.Result(System.String)). I metodi sostituiscono il criterio corrispondente con il criterio definito dal parametro *replacement*.

.NET definisce gli elementi di sostituzione elencati nella tabella riportata di seguito.

Sostituzione | Descrizione
------------ | ----------- 
**$**_numero_ | Include nella stringa di sostituzione l'ultima sottostringa corrispondente al gruppo di acquisizione identificato da *numero* dove *numero* è un valore decimale. Per altre informazioni, vedere [Sostituzione di un gruppo numerato](#substituting-a-numbered-group).
**${**_nome_**}** | Include nella stringa di sostituzione l'ultima sottostringa corrispondente al gruppo denominato definito da **(?<**_nome_**>)**. Per altre informazioni, vedere [Sostituzione di un gruppo denominato](#substituting-a-named-group).
**$$** | Include un solo simbolo letterale "$" nella stringa di sostituzione. Per altre informazioni, vedere [Sostituzione di un carattere "$"](#substituting-a--character).
**$&** | Include una copia dell'intera corrispondenza nella stringa di sostituzione. Per altre informazioni, vedere [Sostituzione dell'intera corrispondenza](#substituting-the-entire-match).
**$`** | Include nella stringa di sostituzione tutto il testo della stringa di input precedente alla corrispondenza. Per altre informazioni, vedere [Sostituzione del testo prima della corrispondenza](#substituting-the-text-before-the-match).
**$'** | Include nella stringa di sostituzione tutto il testo della stringa di input successivo alla corrispondenza. Per altre informazioni, vedere [Sostituzione del testo dopo la corrispondenza](#substituting-the-text-after-the-match). 
**$+** | Include nella stringa di sostituzione l'ultimo gruppo acquisito. Per altre informazioni, vedere [Sostituzione dell'ultimo gruppo acquisito](#substituting-the-last-captured-group).
**$_** | Include l'intera stringa di input nella stringa di sostituzione. Per altre informazioni, vedere [Sostituzione dell'intera stringa di input](#substituting-the-entire-input-string).
 
## <a name="substitution-elements-and-replacement-patterns"></a>Elementi di sostituzione e criteri di sostituzione

Le sostituzioni sono gli unici costrutti speciali riconosciuti in un criterio di sostituzione. Nessuno degli altri elementi del linguaggio delle espressioni regolari, compresi i caratteri di escape e il punto (**.**), che corrispondono a qualsiasi carattere, è supportato. Analogamente, gli elementi del linguaggio di sostituzione sono riconosciuti solo nei criteri di sostituzione e non sono mai validi nei modelli di espressioni regolari. 

L'unico carattere che può essere usato in un criterio di espressione regolare o in una sostituzione è il carattere **$**, anche se presenta un significato diverso in ogni contesto. In un criterio di espressione regolare **$** è un ancoraggio che corrisponde al termine della stringa. In un criterio di sostituzione **$** indica l'inizio di una sostituzione. 

> [!NOTE]
> Per una funzionalità simile a un criterio di sostituzione all'interno di un'espressione regolare, usare un backreference. Per altre informazioni sui backreference, vedere [Costrutti di backreference](backreference.md).
 
## <a name="substituting-a-numbered-group"></a>Sostituzione di un gruppo numerato

L'elemento di linguaggio **$**_numero_ include l'ultima sottostringa corrispondente al gruppo di acquisizione numero nella stringa di sostituzione, dove *numero* è l'indice del gruppo di acquisizione. Ad esempio, il criterio di sostituzione `$1` indica che la sottostringa corrispondente deve essere sostituita dal primo gruppo acquisito. Per altre informazioni sui gruppi di acquisizione numerati, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

Tutte le cifre che seguono **$** vengono interpretate come appartenenti al gruppo numero. Se questa non è la propria intenzione, è possibile sostituire un gruppo denominato invece. Ad esempio, è possibile usare la stringa di sostituzione **${1}1** anziché **$11** per definire la stringa di sostituzione come il valore del primo gruppo acquisito con il numero "1". Per altre informazioni, vedere [Sostituzione di un gruppo denominato](#substituting-a-named-group). 

I gruppi di acquisizione a cui non sono stati assegnati nomi in modo esplicito tramite la sintassi **(?<**_nome-**>)** vengono numerati da sinistra verso destra a partire da uno. I gruppi denominati sono anche numerati da sinistra a destra, a partire dall'indice dell'ultimo gruppo senza nome più uno. Ad esempio, nell'espressione regolare `(\w)(?<digit>\d)` l'indice del gruppo denominato `digit` è 2.

Se *numero* non specifica un gruppo di acquisizione valido definito nel criterio di espressione regolare, **$**_numero_ viene interpretato come una sequenza di caratteri letterali usata per sostituire ogni corrispondenza.

Nell'esempio seguente viene usata la sostituzione **$**_numero_ per rimuovere il simbolo di valuta da un valore decimale. Rimuove i simboli di valuta trovati all'inizio o alla fine di un valore valutario e riconosce i due separatori decimali più comuni ("." e ","). 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*";
      string replacement = "$1";
      string input = "$16.32 12.19 £16.29 €18.29  €18,29";
      string result = Regex.Replace(input, pattern, replacement);
      Console.WriteLine(result);
   }
}
// The example displays the following output:
//       16.32 12.19 16.29 18.29  18,29
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*"
      Dim replacement As String = "$1"
      Dim input As String = "$16.32 12.19 £16.29 €18.29  €18,29"
      Dim result As String = Regex.Replace(input, pattern, replacement)
      Console.WriteLine(result)
   End Sub
End Module
' The example displays the following output:
'       16.32 12.19 16.29 18.29  18,29
```

Il criterio di ricerca di espressioni regolari `\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\p{Sc}*` | Trovare la corrispondenza con zero o più caratteri di simboli valutari.
`\s?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
`[.,]?` | Trova la corrispondenza con zero o con un punto o una virgola.
`\d*` | Ricerca la corrispondenza di zero o di più cifre decimali.
`(\s?\d+[.,]?\d*)` | Corrisponde a uno spazio vuoto seguito da una o più cifre decimali, seguite da zero o un punto o una virgola, seguita da zero o più cifre decimali. Equivale al primo gruppo di acquisizione. Poiché il criterio di sostituzione è `$1`, la chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) sostituisce la sottostringa corrispondente intera con questo gruppo acquisito. 
 
## <a name="substituting-a-named-group"></a>Sostituzione di un gruppo denominato

L'elemento di linguaggio **${**_nome_**}** sostituisce l'ultima sottostringa corrispondente al gruppo di acquisizione *nome*, dove *nome* è il nome di un gruppo di acquisizione definito dall'elemento di linguaggio **(?<**_nome_**>)**. Per altre informazioni sui gruppi di acquisizione denominati, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md).

Se *nome* non specifica un gruppo di acquisizione denominato valido definito nel criterio di espressione regolare ma è costituito da cifre, **${**_nome_**}** viene interpretato come un gruppo numerato. 

Se *nome* non specifica un gruppo di acquisizione denominato valido o un gruppo di acquisizione numerato valido definito nel criterio di espressione regolare, **${**_nome_**}** viene interpretato come una sequenza di caratteri letterali usata per sostituire ogni corrispondenza.

Nell'esempio seguente viene usata la sostituzione **${**_nome_**}** per rimuovere il simbolo di valuta da un valore decimale. Rimuove i simboli di valuta trovati all'inizio o alla fine di un valore valutario e riconosce i due separatori decimali più comuni ("." e ",").

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\p{Sc}*(?<amount>\s?\d+[.,]?\d*)\p{Sc}*";
      string replacement = "${amount}";
      string input = "$16.32 12.19 £16.29 €18.29  €18,29";
      string result = Regex.Replace(input, pattern, replacement);
      Console.WriteLine(result);
   }
}
// The example displays the following output:
//       16.32 12.19 16.29 18.29  18,29
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\p{Sc}*(?<amount>\s?\d+[.,]?\d*)\p{Sc}*"
      Dim replacement As String = "${amount}"
      Dim input As String = "$16.32 12.19 £16.29 €18.29  €18,29"
      Dim result As String = Regex.Replace(input, pattern, replacement)
      Console.WriteLine(result)
   End Sub
End Module
' The example displays the following output:
'       16.32 12.19 16.29 18.29  18,29
```

Il criterio di ricerca di espressioni regolari `\p{Sc}*(?<amount>\s?\d[.,]?\d*)\p{Sc}*` è definito nel modo illustrato nella tabella seguente. 

Criterio | Descrizione
------- | -----------
`\p{Sc}*` | Trovare la corrispondenza con zero o più caratteri di simboli valutari.
`\s?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`\d+` | Trova la corrispondenza con una o più cifre decimali.
`[.,]?` | Trova la corrispondenza con zero o con un punto o una virgola.
`\d*` | Ricerca la corrispondenza di zero o di più cifre decimali.
`(?<amount>\s?\d[.,]?\d*)` | Corrisponde a uno spazio vuoto seguito da una o più cifre decimali, seguite da zero o un punto o una virgola, seguita da zero o più cifre decimali. Questo è il gruppo di acquisizione denominato. Poiché il criterio di sostituzione è `${amount}`, la chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.String,System.Text.RegularExpressions.RegexOptions)) sostituisce la sottostringa corrispondente intera con questo gruppo acquisito. 
 
## <a name="substituting-a-character"></a>Sostituzione di un carattere $

La sostituzione **$$** inserisce un carattere "$" letterale nella stringa sostituita. 

Nell'esempio riportato di seguito viene usato l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) per determinare il simbolo di valuta delle impostazioni cultura correnti e la relativa posizione in una stringa di valuta. Compila quindi in modo dinamico sia un modello di espressione regolare sia un criterio di sostituzione. Se l'esempio viene eseguito in un computer le cui impostazioni cultura correnti sono en-US, tale computer genera il criterio di espressione regolare `\b(\d+)(\.(\d+))?` e il criterio di sostituzione `$$ $1$2`. Il criterio di sostituzione sostituisce il testo corrispondente con un simbolo di valuta e uno spazio seguiti dal primo e dal secondo gruppo acquisito.

```csharp
using System;
using System.Globalization;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Define array of decimal values.
      string[] values= { "16.35", "19.72", "1234", "0.99"};
      // Determine whether currency precedes (True) or follows (False) number.
      bool precedes = NumberFormatInfo.CurrentInfo.CurrencyPositivePattern % 2 == 0;
      // Get decimal separator.
      string cSeparator = NumberFormatInfo.CurrentInfo.CurrencyDecimalSeparator;
      // Get currency symbol.
      string symbol = NumberFormatInfo.CurrentInfo.CurrencySymbol;
      // If symbol is a "$", add an extra "$".
      if (symbol == "$") symbol = "$$";

      // Define regular expression pattern and replacement string.
      string pattern = @"\b(\d+)(" + cSeparator + @"(\d+))?"; 
      string replacement = "$1$2";
      replacement = precedes ? symbol + " " + replacement : replacement + " " + symbol;
      foreach (string value in values)
         Console.WriteLine("{0} --> {1}", value, Regex.Replace(value, pattern, replacement));
   }
}
// The example displays the following output:
//       16.35 --> $ 16.35
//       19.72 --> $ 19.72
//       1234 --> $ 1234
//       0.99 --> $ 0.99
```

```vb
Imports System.Globalization
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      ' Define array of decimal values.
      Dim values() As String = { "16.35", "19.72", "1234", "0.99"}
      ' Determine whether currency precedes (True) or follows (False) number.
      Dim precedes As Boolean = (NumberFormatInfo.CurrentInfo.CurrencyPositivePattern Mod 2 = 0)
      ' Get decimal separator.
      Dim cSeparator As String = NumberFormatInfo.CurrentInfo.CurrencyDecimalSeparator
      ' Get currency symbol.
      Dim symbol As String = NumberFormatInfo.CurrentInfo.CurrencySymbol
      ' If symbol is a "$", add an extra "$".
      If symbol = "$" Then symbol = "$$"

      ' Define regular expression pattern and replacement string.
      Dim pattern As String = "\b(\d+)(" + cSeparator + "(\d+))?" 
      Dim replacement As String = "$1$2"
      replacement = If(precedes, symbol + " " + replacement, replacement + " " + symbol)
      For Each value In values
         Console.WriteLine("{0} --> {1}", value, Regex.Replace(value, pattern, replacement))
      Next
   End Sub
End Module
' The example displays the following output:
'       16.35 --> $ 16.35
'       19.72 --> $ 19.72
'       1234 --> $ 1234
'       0.99 --> $ 0.99
```

Il criterio di ricerca di espressioni regolari `\b(\d+)(\.(\d+))?` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia la corrispondenza all'inizio di un confine di parola.
`(\d+)` | Trova la corrispondenza con una o più cifre decimali. Equivale al primo gruppo di acquisizione.
`\.` | Trovare la corrispondenza con un punto (ovvero il separatore decimale).
`(\d+)` | Trova la corrispondenza con una o più cifre decimali. Equivale al terzo gruppo di acquisizione.
`(\.(\d+))?` | Trovare la corrispondenza con zero o una occorrenza di un punto seguito da una o più cifre decimali. Equivale al secondo gruppo di acquisizione.
 
## <a name="substituting-the-entire-match"></a>Sostituzione dell'intera corrispondenza

La sostituzione **$&** include l'intera corrispondenza nella stringa di sostituzione. Spesso viene utilizzata per aggiungere una sottostringa all'inizio o alla fine della stringa corrispondente. Ad esempio, il criterio di sostituzione `($&)` aggiunge parentesi all'inizio e alla fine di ogni corrispondenza. Se non esiste alcuna corrispondenza, la sostituzione **$&** non ha alcun effetto.

Nell'esempio seguente viene usata la sostituzione **$&** per aggiungere virgolette all'inizio e alla fine dei titoli di libro archiviati in una matrice di stringhe.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^(\w+\s?)+$";
      string[] titles = { "A Tale of Two Cities", 
                          "The Hound of the Baskervilles", 
                          "The Protestant Ethic and the Spirit of Capitalism", 
                          "The Origin of Species" };
      string replacement = "\"$&\"";
      foreach (string title in titles)
         Console.WriteLine(Regex.Replace(title, pattern, replacement));
   }
}
// The example displays the following output:
//       "A Tale of Two Cities"
//       "The Hound of the Baskervilles"
//       "The Protestant Ethic and the Spirit of Capitalism"
//       "The Origin of Species"
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(\w+\s?)+$"
      Dim titles() As String = { "A Tale of Two Cities", _
                                 "The Hound of the Baskervilles", _
                                 "The Protestant Ethic and the Spirit of Capitalism", _
                                 "The Origin of Species" }
      Dim replacement As String = """$&"""
      For Each title As String In titles
         Console.WriteLine(Regex.Replace(title, pattern, replacement))
      Next  
   End Sub
End Module
' The example displays the following output:
'       "A Tale of Two Cities"
'       "The Hound of the Baskervilles"
'       "The Protestant Ethic and the Spirit of Capitalism"
'       "The Origin of Species"
```

Il criterio di ricerca di espressioni regolari `^(\w+\s?)+$` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`(\w+\s?)+` | Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri alfanumerici seguiti da zero o da uno spazio vuoto. 
`$` | Trova la corrispondenza con la fine della stringa di input.

Il criterio di sostituzione `"$&"` aggiunge le virgolette letterali all'inizio e alla fine di ogni corrispondenza.

## <a name="substituting-the-text-before-the-match"></a>Sostituzione del testo prima della corrispondenza

La sostituzione **$`** substitution replaces the matched string with the entire input string before the match. That is, it duplicates the input string up to the match while removing the matched text. Any text that follows the matched text is unchanged in the result string. If there are multiple matches in an input string, the replacement text is derived from the original input string, rather than from the string in which text has been replaced by earlier matches. (The example provides an illustration.) If there is no match, the **$`** non ha alcun effetto.

Nell'esempio seguente viene usato il criterio di espressione regolare `\d+` per trovare la corrispondenza con una sequenza di una o più cifre decimali nella stringa di input. La stringa di sostituzione **$`** sostituisce queste cifre con il testo che precede la corrispondenza. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aa1bb2cc3dd4ee5";
      string pattern = @"\d+";
      string substitution = "$`";
      Console.WriteLine("Matches:");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);

      Console.WriteLine("Input string:  {0}", input);
      Console.WriteLine("Output string: " + 
                        Regex.Replace(input, pattern, substitution));
   }
}
// The example displays the following output:
//    Matches:
//       1 at position 2
//       2 at position 5
//       3 at position 8
//       4 at position 11
//       5 at position 14
//    Input string:  aa1bb2cc3dd4ee5
//    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aa1bb2cc3dd4ee5"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$`"
      Console.WriteLine("Matches:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
      Console.WriteLine("Input string:  {0}", input)
      Console.WriteLine("Output string: " + _
                        Regex.Replace(input, pattern, substitution))
   End Sub
End Module
' The example displays the following output:
'    Matches:
'       1 at position 2
'       2 at position 5
'       3 at position 8
'       4 at position 11
'       5 at position 14
'    Input string:  aa1bb2cc3dd4ee5
'    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

In questo esempio, la stringa di input `"aa1bb2cc3dd4ee5"` contiene cinque corrispondenze. La tabella seguente illustra come la sostituzione $' fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna della stringa dei risultati.

Corrispondenza con | Posizione | Stringa prima della corrispondenza | Stringa di risultato
----- | -------- | ------------------- | -------------
1 | 2 | aa | aa**aa**bb2cc3dd4ee5
2 | 5 | aa1bb | aaaabb**aa1bb**cc3dd4ee5
3 | 8 | aa1bb2cc | aaaabbaa1bbcc**aa1bb2cc**dd4ee5
4 | 11 | aa1bb2cc3dd | aaaabbaa1bbccaa1bb2ccdd**aa1bb2cc3dd**ee5
5 | 14 | aa1bb2cc3dd4ee | aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddee **aa1bb2cc3dd4ee**
 
## <a name="substituting-the-text-after-the-match"></a>Sostituzione del testo dopo la corrispondenza

La sostituzione **$'** sostituisce la stringa corrispondente con l'intera stringa di input dopo la corrispondenza. Ovvero, duplica la stringa di input dopo la corrispondenza e rimuove il testo corrispondente. Qualsiasi testo che precede il testo corrispondente resta invariato nella stringa di risultato. Se non esiste alcuna corrispondenza, la sostituzione **$'** non ha alcun effetto.

Nell'esempio seguente viene usato il criterio di espressione regolare `\d+` per trovare la corrispondenza con una sequenza di una o più cifre decimali nella stringa di input. La stringa di sostituzione **$'** sostituisce queste cifre con il testo che segue la corrispondenza. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "aa1bb2cc3dd4ee5";
      string pattern = @"\d+";
      string substitution = "$'";
      Console.WriteLine("Matches:");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
      Console.WriteLine("Input string:  {0}", input);
      Console.WriteLine("Output string: " + 
                        Regex.Replace(input, pattern, substitution));
   }
}
// The example displays the following output:
//    Matches:
//       1 at position 2
//       2 at position 5
//       3 at position 8
//       4 at position 11
//       5 at position 14
//    Input string:  aa1bb2cc3dd4ee5
//    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "aa1bb2cc3dd4ee5"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$'"
      Console.WriteLine("Matches:")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
      Console.WriteLine("Input string:  {0}", input)
      Console.WriteLine("Output string: " + _
                        Regex.Replace(input, pattern, substitution))
   End Sub
End Module
' The example displays the following output:
'    Matches:
'       1 at position 2
'       2 at position 5
'       3 at position 8
'       4 at position 11
'       5 at position 14
'    Input string:  aa1bb2cc3dd4ee5
'    Output string: aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddeeaa1bb2cc3dd4ee
```

In questo esempio, la stringa di input `"aa1bb2cc3dd4ee5"` contiene cinque corrispondenze. La tabella seguente illustra come la sostituzione **$'** fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna della stringa dei risultati.

Corrispondenza con | Posizione | Stringa prima della corrispondenza | Stringa di risultato
----- | -------- | ------------------- | -------------
1 | 2 | bb2cc3dd4ee5 | aa**bb2cc3dd4ee5**bb2cc3dd4ee5
2 | 5 | cc3dd4ee5 | aabb2cc3dd4ee5bb**cc3dd4ee5**cc3dd4ee5
3 | 8 | dd4ee5 | aabb2cc3dd4ee5bbcc3dd4ee5cc**dd4ee5**dd4ee5
4 | 11 | ee5 | aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5dd**ee5**ee5
5 | 14 | [String.Empty](xref:System.String.Empty) | aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5ddee5ee
 
## <a name="substituting-the-last-captured-group"></a>Sostituzione dell'ultimo gruppo acquisito

La sostituzione **$+** sostituisce la stringa corrispondente con l'ultimo gruppo acquisito. Se non esistono gruppi acquisiti o se il valore dell'ultimo gruppo acquisito è [String.Empty](xref:System.String.Empty), la sostituzione **$+** non ha alcun effetto.

L'esempio seguente identifica le parole duplicate in una stringa e usa la sostituzione **$+** per sostituirle con una sola occorrenza della parola. L'opzione [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase) viene usata per garantire che le parole che differiscono solo in termini di maiuscole e minuscole siano considerate come parole duplicate.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)\s\1\b";
      string substitution = "$+";
      string input = "The the dog jumped over the fence fence.";
      Console.WriteLine(Regex.Replace(input, pattern, substitution, 
                        RegexOptions.IgnoreCase));
   }
}
// The example displays the following output:
//      The dog jumped over the fence.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)\s\1\b"
      Dim substitution As String = "$+"
      Dim input As String = "The the dog jumped over the fence fence."
      Console.WriteLine(Regex.Replace(input, pattern, substitution, _
                                      RegexOptions.IgnoreCase))
   End Sub
End Module
' The example displays the following output:
'      The dog jumped over the fence.
```

Il criterio di ricerca di espressioni regolari `\b(\w+)\s\1\b` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`(\w+)` | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`\1` | Trovare la corrispondenza con il primo gruppo acquisito.
`\b` | Termina la corrispondenza sul confine di parola.
 
## <a name="substituting-the-entire-input-string"></a>Sostituzione dell'intera stringa di input

La sostituzione **$_** sostituisce la stringa corrispondente con l'intera stringa di input. Ovvero, rimuove il testo corrispondente e lo sostituisce con la stringa intera, compreso il testo corrispondente.

Nell'esempio seguente vengono corrisposte una o più cifre decimali della stringa di input. Usa la sostituzione **$_** per sostituirle con l'intera stringa di input.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "ABC123DEF456";
      string pattern = @"\d+";
      string substitution = "$_";
      Console.WriteLine("Original string:          {0}", input);
      Console.WriteLine("String with substitution: {0}", 
                        Regex.Replace(input, pattern, substitution));      
   }
}
// The example displays the following output:
//       Original string:          ABC123DEF456
//       String with substitution: ABCABC123DEF456DEFABC123DEF456
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "ABC123DEF456"
      Dim pattern As String = "\d+"
      Dim substitution As String = "$_"
      Console.WriteLine("Original string:          {0}", input)
      Console.WriteLine("String with substitution: {0}", _
                        Regex.Replace(input, pattern, substitution))      
   End Sub
End Module
' The example displays the following output:
'       Original string:          ABC123DEF456
'       String with substitution: ABCABC123DEF456DEFABC123DEF456
```

In questo esempio, la stringa di input `"ABC123DEF456"` contiene due corrispondenze. La tabella seguente illustra come la sostituzione **$_** fa in modo che il motore delle espressioni regolari sostituisca ogni corrispondenza nella stringa di input. Il testo inserito viene visualizzato in grassetto nella colonna della stringa dei risultati.

Corrispondenza con | Posizione | Stringa prima della corrispondenza | Stringa di risultato
----- | -------- | ------------------- | -------------
1 | 3 | 123 | ABC**ABC123DEF456**DEF456
2 | 5 | 456 | ABCABC123DEF456DEF**ABC123DEF456**
 
## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)




<!--HONumber=Nov16_HO1-->


