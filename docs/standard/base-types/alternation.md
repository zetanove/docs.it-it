---
title: Costrutti di alternanza nelle espressioni regolari
description: Costrutti di alternanza nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 59ffac4d-fc6e-461f-8783-d9f8dc88ce2c
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: fa2a880e5bcc36354bd59d3dc032180c89984f1d
ms.lasthandoff: 03/02/2017

---

# <a name="alternation-constructs-in-regular-expressions"></a>Costrutti di alternanza nelle espressioni regolari

I costrutti di alternanza modificano un'espressione regolare per abilitare la corrispondenza di tipo either/or o condizionale. .NET supporta tre costrutti di alternanza:

* Criteri di ricerca con **|**

* Corrispondenza condizionale con **(?(**_espressione_**)**_yes_**|**_no_**)**

* Corrispondenza condizionale in base a un gruppo acquisito valido

## <a name="pattern-matching-with-"></a>Criteri di ricerca con |

È possibile usare la barra verticale (|) per trovare la corrispondenza con uno qualsiasi di una serie di criteri, dove i singoli criteri sono separati dal carattere|. 

Analogamente alla classe di caratteri positivi, il carattere | può essere usato per trovare la corrispondenza con uno qualsiasi tra diversi caratteri singoli. L'esempio seguente usa sia una classe di caratteri positivi sia criteri di ricerca di tipo either/or con il carattere | per individuare le occorrenze delle parole "gray" o "grey" in una stringa. In questo caso il carattere | produce un'espressione regolare più dettagliata. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Regular expression using character class.
      string pattern1 = @"\bgr[ae]y\b";
      // Regular expression using either/or.
      string pattern2 = @"\bgr(a|e)y\b";

      string input = "The gray wolf blended in among the grey rocks.";
      foreach (Match match in Regex.Matches(input, pattern1))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
      Console.WriteLine();
      foreach (Match match in Regex.Matches(input, pattern2))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       'gray' found at position 4
//       'grey' found at position 35
//       
//       'gray' found at position 4
//       'grey' found at position 35           
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      ' Regular expression using character class.
      Dim pattern1 As String = "\bgr[ae]y\b"
      ' Regular expression using either/or.
      Dim pattern2 As String = "\bgr(a|e)y\b"

      Dim input As String = "The gray wolf blended in among the grey rocks."
      For Each match As Match In Regex.Matches(input, pattern1)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next      
      Console.WriteLine()
      For Each match As Match In Regex.Matches(input, pattern2)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next      
   End Sub
End Module
' The example displays the following output:
'       'gray' found at position 4
'       'grey' found at position 35
'       
'       'gray' found at position 4
'       'grey' found at position 35 
```

L'espressione regolare che usa il carattere |, `\bgr(a|e)y\b,`, viene interpretata nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`gr` | Corrisponde ai caratteri "gr".
`(a|e)` | Corrisponde a una "a" o una "e".
`y\b` |    Corrisponde a una "y" in un confine di parola.


Il carattere | può essere usato anche per trovare una corrispondenza di tipo either/or con più caratteri o sottoesspressioni, che possono includere qualsiasi combinazione di valori letterali carattere ed elementi language di espressioni regolari. La classe di caratteri non offre questa funzionalità. L'esempio seguente usa il carattere | per estrarre un numero di previdenza sociale (SSN, Social Security Number) degli Stati Uniti, che corrisponde a un numero a 9 cifre (d, digit) con il formato *ddd-dd-dddd* oppure un identificativo del datore di lavoro (EIN, Employer Identification Number) degli Stati Uniti, che corrisponde a un numero a 9 cifre (d, digit) con il formato *dd-ddddddd*.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

L'espressione regolare `\b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` viene interpretata come illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`(\d{2}-\d{7}|;\d{3}-\d{2}-\d{4})` | Corrisponde a una delle due opzioni seguenti: due cifre decimali seguite da un trattino seguito da sette cifre decimali oppure tre cifre decimali, un trattino, due cifre decimali, un altro trattino e quattro cifre decimali. 
`\d` | Termina la corrispondenza sul confine di parola.
                                         
## <a name="conditional-matching-with-an-expression"></a>Corrispondenza condizionale con un'espressione

Questo elemento del linguaggio tenta di trovare una corrispondenza con uno di due criteri, a seconda della possibilità di trovare una corrispondenza con un criterio iniziale. La sintassi è la seguente:

**(? (**_espressione_**)**_yes_**|**_no_**)**

dove *espressione* è il criterio iniziale per la corrispondenza, *yes* è il criterio di corrispondenza se viene trovata una corrispondenza per l'espressione e *no* è il criterio facoltativo di corrispondenza se non viene trovata una corrispondenza per *espressione*. Il motore delle espressioni regolari considera *espressione* come un'asserzione di larghezza zero, ovvero questo motore non avanza nel flusso di input dopo aver valutato *espressione*. Questo costrutto è pertanto equivalente a quanto segue:

**(?(?**=_espressione_**)**_yes_**|**_no_**)**

dove **(?**=_espressione_**)** è un costrutto di asserzione di larghezza zero. Per altre informazioni, vedere [Costrutti di raggruppamento nelle espressioni regolari](grouping.md). Poiché il motore delle espressioni regolari interpreta *espressione* come un ancoraggio (un'asserzione di larghezza zero), *espressione* deve essere un'asserzione di larghezza zero (per altre informazioni, vedere [Ancoraggi nelle espressioni regolari](anchors.md)) o una sottoespressione anch'essa contenuta in *yes*. In caso contrario, non è possibile trovare una corrispondenza per il criterio *yes*. 

> [!NOTE]
> Se *espressione* è un gruppo di acquisizione denominato o numerato, il costrutto di alternanza viene interpretato come un test di acquisizione. Per altre informazioni, vedere la sezione successiva, [Corrispondenza condizionale in base a un gruppo acquisito valido](#conditional-matching-based-on-a-valid-captured-group). In altre parole, il motore delle espressioni regolari non tenta di trovare la corrispondenza con la sottostringa acquisita, ma verifica invece la presenza o l'assenza del gruppo.
 

L'esempio seguente è una variante dell'esempio visualizzato nella sezione precedente. L'esempio usa la corrispondenza condizionale per determinare se i primi tre caratteri dopo un confine di parola sono due cifre seguite da un trattino. In caso affermativo, viene effettuato un tentativo di trovare una corrispondenza con un identificativo del datore di lavoro (EIN) degli Stati Uniti. In caso contrario, viene effettuato un tentativo di trovare una corrispondenza con un numero di previdenza sociale (SSN) degli Stati Uniti.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

Il criterio di ricerca di espressioni regolari `\b(?(\d{2}-)\d{2}-\d{7}|\d{3}-\d{2}-\d{4})\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`(?(\d{2}-)` | Determina se i tre caratteri successivi sono costituiti da due cifre seguite da un trattino.
`\d{2}-\d{7}` | Se il criterio precedente viene soddisfatto, trova la corrispondenza con due cifre seguite da un trattino seguito da sette cifre.
`\d{3}-\d{2}-\d{4}` | Se il criterio precedente non viene soddisfatto, trova la corrispondenza con tre cifre decimali, un trattino, due cifre decimali, un altro trattino e quattro cifre decimali. 
`\b` | Trova la corrispondenza di un confine di parola.
 
## <a name="conditional-matching-based-on-a-valid-captured-group"></a>Corrispondenza condizionale in base a un gruppo acquisito valido

Tramite questo elemento di linguaggio viene effettuato un tentativo di corrispondenza con uno dei due modelli, a seconda dell'effettiva corrispondenza con un gruppo di acquisizione specificato. La sintassi è la seguente:

**(?(**_nome_**)**_yes_**|**_no_**)**

o

**(?(**_numero_**)**_yes_**|**_no_**)**

dove *nome* è il nome e *numero* è il numero di un gruppo di acquisizione, *yes* è l'espressione di cui trovare la corrispondenza se per il nome o il numero è disponibile una corrispondenza e *no* è l'espressione facoltativa di cui trovare la corrispondenza in caso contrario.

Se *nome* non corrisponde al nome di un gruppo di acquisizione usato nel criterio di espressione regolare, il costrutto di alternanza viene interpretato come un test di espressione, come illustrato nella sezione precedente. In genere ciò significa che l'espressione restituisce `false`. Se `number` non corrisponde a un gruppo di acquisizione numerato usato nel criterio di espressione regolare, il motore delle espressioni regolari genera un'eccezione [ArgumentException](xref:System.ArgumentException).

L'esempio seguente è una variante dell'esempio visualizzato nella sezione precedente. L'esempio usa un gruppo di acquisizione denominato `n2` costituito da due cifre seguite da un trattino. Il costrutto di alternanza verifica se per questo gruppo di acquisizione è presente una corrispondenza nella stringa di input. In caso affermativo, il costrutto di alternanza tenta di trovare la corrispondenza con le ultime sette cifre delle nove cifre di un identificativo del datore di lavoro (EIN) degli Stati Uniti. In caso contrario, tenta di trovare la corrispondenza con le nove cifre di un numero di previdenza sociale (SSN) degli Stati Uniti.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example displays the following output:
//       Matches for \b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
```

Il criterio di ricerca di espressioni regolari `\b(?<n2>\d{2}-)*(?(n2)\d{7}|\d{3}-\d{2}-\d{4})\b` è interpretato nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`(?<n2>\d{2}-)*` | Corrisponde a zero o una occorrenza di due cifre seguite da un trattino. Il nome di questo gruppo di acquisizione è `n2`.
`(?(n2)` | Verificare se per `n2` è stata individuata una corrispondenza nella stringa di input. 
`)\d{7}` | Se per `n2` è stata individuata una corrispondenza, far corrispondere sette cifre decimali.
`|;\d{3}-\d{2}-\d{4}` | Se per `n2` non è stata trovata alcuna corrispondenza, far corrispondere tre cifre decimali, un trattino, due cifre decimali, un altro trattino e quattro cifre decimali. 
`\b` | Trova la corrispondenza di un confine di parola.
 
Nell'esempio seguente è illustrata una variante di questo esempio che usa un gruppo numerato anziché un gruppo denominato. Il criterio di espressione regolare è `\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b`.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b";
      string input = "01-9999999 020-333333 777-88-9999";
      Console.WriteLine("Matches for {0}:", pattern);
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index);
   }
}
// The example display the following output:
//       Matches for \b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b:
//          01-9999999 at position 0
//          777-88-9999 at position 22
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b"
      Dim input As String = "01-9999999 020-333333 777-88-9999"
      Console.WriteLine("Matches for {0}:", pattern)
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("   {0} at position {1}", match.Value, match.Index)
      Next   
   End Sub
End Module
' The example displays the following output:
'       Matches for \b(\d{2}-)*(?(1)\d{7}|\d{3}-\d{2}-\d{4})\b:
'          01-9999999 at position 0
'          777-88-9999 at position 22
```

Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)


