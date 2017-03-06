---
title: Classi di caratteri nelle espressioni regolari
description: Classi di caratteri nelle espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c7a9305f-7144-4fe8-80e8-a727bf7d223f
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: ae677af2590636fd144d8978a3500c37f9d33615
ms.lasthandoff: 03/03/2017

---

# <a name="character-classes-in-regular-expressions"></a>Classi di caratteri nelle espressioni regolari

Una classe di caratteri definisce un set di caratteri, di cui uno qualsiasi può verificarsi in una stringa di input per trovare una corrispondenza. Il linguaggio delle espressioni regolari di .NET supporta le classi di caratteri seguenti:

* Gruppi di caratteri positivi. Un carattere nella stringa di input deve corrispondere a un set di caratteri specificato. Per altre informazioni, vedere [Gruppo di caratteri positivi](#positive-character-group--).

* Gruppi di caratteri negativi. Un carattere nella stringa di input non deve corrispondere a un set di caratteri specificato. Per altre informazioni, vedere [Gruppo di caratteri negativi](#negative-character-group-).

* Qualsiasi carattere. Il file con estensione  Il carattere . (punto) in un'espressione regolare è un carattere jolly che corrisponde a qualsiasi carattere, eccetto **\n**. Per altre informazioni, vedere [Qualsiasi carattere](#any-character-). 

* Categoria generale Unicode o blocco denominato. Per trovare una corrispondenza, un carattere nella stringa di input deve appartenere a una particolare categoria Unicode o essere compreso in un intervallo contiguo di caratteri Unicode. Per altre informazioni, vedere [Categoria Unicode o blocco Unicode](#unicode-category-or-unicode-block-p).

* Categoria Unicode generale o blocco denominato. Per trovare una corrispondenza, un carattere nella stringa di input non deve appartenere a una particolare categoria Unicode o non deve essere compreso in un intervallo contiguo di caratteri Unicode. Per altre informazioni, vedere [Categoria Unicode negativa o blocco Unicode negativo](#negative-unicode-category-or-unicode-block-p).

* Carattere alfanumerico. Un carattere nella stringa di input può appartenere a qualsiasi categoria Unicode appropriata per i caratteri alfanumerico. Per altre informazioni, vedere [Carattere alfanumerico](#word-character-w).

* Carattere non alfanumerico. Un carattere nella stringa di input può appartenere a qualsiasi categoria Unicode che non sia un carattere alfanumerico. Per altre informazioni, vedere [Carattere non alfanumerico](#non-word-character-w).

* Spazio vuoto. Un carattere nella stringa di input può essere qualsiasi carattere separatore Unicode, nonché un numero qualsiasi di caratteri di controllo. Per altre informazioni, vedere [Spazio vuoto](#white-space-character-s).

* Carattere diverso da uno spazio vuoto. Un carattere nella stringa di input può essere qualsiasi carattere diverso da uno spazio vuoto. Per altre informazioni, vedere [Carattere diverso da uno spazio vuoto](#non-white-space-character-s).

* Cifra decimale. Un carattere nella stringa di input può essere qualsiasi numero di caratteri classificati come cifre decimali Unicode. Per altre informazioni, vedere [Carattere cifra decimale](#decimal-digit-character-d).

* Cifra non decimale. Un carattere nella stringa di input può essere qualsiasi carattere tranne una cifra decimale Unicode. Per altre informazioni, vedere [Carattere cifra non decimale](#non-digit-character-d).


.NET supporta espressioni di sottrazione di classi di caratteri che consentono di definire un set di caratteri come risultato dell'esclusione di una classe di caratteri da un'altra classe di caratteri. Per altre informazioni, vedere [Sottrazione di classi di caratteri](#character-class-subtraction).

## <a name="positive-character-group--"></a>Gruppo di caratteri positivi: [ ]

Un gruppo di caratteri positivi specifica un elenco di caratteri che possono essere presenti in una stringa di input per trovare una corrispondenza. È possibile specificare l'elenco di caratteri singolarmente, come intervallo o entrambi. 

Di seguito viene indicata la sintassi per specificare un elenco di singoli caratteri: 

[*character*_*group*]

dove *character_group* è un elenco dei singoli caratteri che possono essere inclusi nella stringa di input affinché una corrispondenza riesca. *character*_*group* può contenere qualsiasi combinazione di uno o più caratteri letterali, [caratteri di escape](escapes.md) o classi di caratteri. 

Di seguito viene indicata la sintassi per specificare un intervallo di caratteri:

```
[firstCharacter-lastCharacter]
```

dove *firstCharacter* è il carattere all'inizio dell'intervallo e *lastCharacter* è il carattere alla fine dell'intervallo. Un intervallo di caratteri è una serie contigua di caratteri definita specificando il primo carattere della serie, un trattino (-), quindi l'ultimo carattere della serie. Due caratteri sono contigui se hanno punti di codice Unicode adiacenti.

Nella tabella seguente sono elencati alcuni criteri di espressione regolare comuni contenenti classi di caratteri positivi.

Criterio | Descrizione
------- | ----------- 
`[aeiou]` | Corrisponde a tutte le vocali.
`[\p{P}\d]` | Corrisponde a tutti i caratteri di punteggiatura e tutte le cifre decimali.
`[\s\p{P}]` | Corrisponde a tutti gli spazi vuoti e ai caratteri di punteggiatura.
 
Nell'esempio seguente viene definito un gruppo di caratteri positivi contenente i caratteri "a" ed "e" in modo che la stringa di input contenga obbligatoriamente le parole "grey" o "gray" seguite da un'altra parola perché si verifichi una corrispondenza.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"gr[ae]y\s\S+?[\s\p{P}]";
      string input = "The gray wolf jumped over the grey wall.";
      MatchCollection matches = Regex.Matches(input, pattern);
      foreach (Match match in matches)
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       gray wolf
//       grey wall.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "gr[ae]y\s\S+?[\s\p{P}]"
      Dim input As String = "The gray wolf jumped over the grey wall."
      Dim matches As MatchCollection = Regex.Matches(input, pattern)
      For Each match As Match In matches
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       gray wolf
'       grey wall.
```

L'espressione regolare `gr[ae]y\s\S+?[\s|\p{P}]` viene definita come segue:

Criterio | Descrizione
------- | ----------- 
`gr` | Corrisponde ai caratteri letterali "gr".
`[ae]` | Corrisponde a una "a" o una "e".
`y\s` | Corrisponde al carattere letterale "y" seguito da uno spazio vuoto.
`\S+?` | Corrisponde a uno o più spazi vuoti, ma al minor numero possibile.
`[\s\p{P}]` | Corrisponde a uno spazio vuoto o a un segno di punteggiatura.
 
Le corrispondenze dell'esempio seguente sono relative a parole che iniziano con una lettera maiuscola qualsiasi. Viene usata la sottoespressione `[A-Z]` per rappresentare l'intervallo di lettere maiuscole da A a Z. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b[A-Z]\w*\b";
      string input = "A city Albany Zulu maritime Marseilles";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       A
//       Albany
//       Zulu
//       Marseilles
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b[A-Z]\w*\b"
      Dim input As String = "A city Albany Zulu maritime Marseilles"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
```

L'espressione regolare `\b[A-Z]\w*\b` viene definita come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`[A-Z]` | Corrisponde a qualsiasi carattere maiuscolo da A a Z.
`\w*` | Trova la corrispondenza di zero o più caratteri alfanumerici.
`\b` | Trova la corrispondenza di un confine di parola.

## <a name="negative-character-group-"></a>Gruppo di caratteri negativi: [^]

Un gruppo di caratteri negativi specifica un elenco di caratteri che non devono essere presenti in una stringa di input per trovare una corrispondenza. È possibile specificare l'elenco di caratteri singolarmente, come intervallo o entrambi. 

Di seguito viene indicata la sintassi per specificare un elenco di singoli caratteri:

[^*character*_*group*]

dove *character_group* è un elenco dei singoli caratteri che non possono essere inclusi nella stringa di input affinché una corrispondenza riesca. *character*_*group* può contenere qualsiasi combinazione di uno o più caratteri letterali, [caratteri di escape](escapes.md) o classi di caratteri. 

Di seguito viene indicata la sintassi per specificare un intervallo di caratteri:

[^*firstCharacter-lastCharacter*]

dove *firstCharacter* è il carattere all'inizio dell'intervallo e *lastCharacter* è il carattere alla fine dell'intervallo. Un intervallo di caratteri è una serie contigua di caratteri definita specificando il primo carattere della serie, un trattino (-), quindi l'ultimo carattere della serie. Due caratteri sono contigui se hanno punti di codice Unicode adiacenti.

Due o più intervalli di caratteri possono essere concatenati. Ad esempio, per specificare l'intervallo di cifre decimali comprese tra "0" e "9", l'intervallo di lettere minuscole comprese tra "a" e "f" e l'intervallo di lettere maiuscole comprese tra "A" e "F", usare `[0-9a-fA-F]`.

L'accento circonflesso iniziale (^) in un gruppo di caratteri negativi è obbligatorio e indica che tale gruppo è un gruppo di caratteri negativi anziché un gruppo di caratteri positivi.

> [!IMPORTANT]
> Un gruppo di caratteri negativi in un criterio di ricerca di espressioni regolari più grande non è un'asserzione di larghezza zero. Ovvero, dopo avere valutato il gruppo di caratteri negativi, il motore delle espressioni regolari avanza di un carattere nella stringa di input.

Nella tabella seguente sono elencati alcuni criteri di espressione regolare comuni contenenti gruppi di caratteri negativi.

Criterio | Descrizione
------- | ----------- 
`[^aeiou]` | Corrisponde a tutti i caratteri eccetto le vocali.
`[^\p{P}\d]` | Corrisponde a tutti i caratteri eccetto caratteri di punteggiatura e cifre decimali.
 
Le corrispondenze dell'esempio seguente sono relative a tutte le parole che iniziano con i caratteri "th" e non sono seguite dalla lettera "o". 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\bth[^o]\w+\b";
      string input = "thought thing though them through thus thorough this";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       thing
//       them
//       through
//       thus
//       this
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\bth[^o]\w+\b"
      Dim input As String = "thought thing though them through thus " + _
                            "thorough this"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       thing
'       them
'       through
'       thus
'       this
```

L'espressione regolare `\bth[^o]\w+\b` viene definita come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`th` | Corrisponde ai caratteri letterali "th".
`[^o]` | Corrisponde a tutti i caratteri diversi da "o".
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`\b` | Terminare al confine di una parola.

## <a name="any-character-"></a>Qualsiasi carattere: .

Il carattere punto (.) corrisponde a qualsiasi carattere ad eccezione di **\n** (il carattere di nuova riga, **\u000A**), con le due qualificazioni seguenti:

* Se un modello di espressione regolare viene modificato dall'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) o se la parte del modello contenente la classe di caratteri . viene modificata dall'opzione **s**, viene trovata la corrispondenza di qualsiasi carattere. Per altre informazioni, vedere [Opzioni di espressioni regolari](options.md).

  Nell'esempio seguente vengono illustrate le differenze di comportamento della classe di caratteri . se si usa l'impostazione predefinita o l'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline). L'espressione regolare `^.+` parte dall'inizio della stringa e individua una corrispondenza per ogni carattere. Per impostazione predefinita, la corrispondenza termina alla fine della prima riga. Il modello di espressione regolare trova il carattere di ritorno a capo **\r** o **\u000D**, ma non **\n**. Poiché l'opzione [RegexOptions.Singleline](xref:System.Text.RegularExpressions.RegexOptions.Singleline) interpreta l'intera stringa di input come riga singola, ottiene una corrispondenza per ogni carattere nella stringa di input, incluso **\n**.

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

  > [!NOTE]
  > Poiché trova corrispondenza con ogni carattere ad eccezione di **\n**, la classe di caratteri trova anche **\r**, ossia il carattere di ritorno a capo, **\u000D**.
 
* In un gruppo di caratteri positivi o negativi un punto viene interpretato come carattere punto letterale e non come classe di caratteri. Per altre informazioni, vedere [Gruppo di caratteri positivi](#positive-character-group--) o [Gruppo di caratteri negativi](#negative-character-group-) descritti in precedenza in questo argomento. L'esempio seguente illustra la definizione di un'espressione regolare che include il carattere punto (**.**) sia come classe di caratteri che come membro di un gruppo di caratteri positivi. L'espressione regolare `\b.*[.?!;:](\s|\z)` inizia in corrispondenza di confine di parola, corrisponde a qualsiasi carattere fino a quando non incontra uno dei quattro segni di punteggiatura, incluso un punto, quindi individua la corrispondenza con uno spazio vuoto o con la fine della stringa.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b.*[.?!;:](\s|\z)";
      string input = "this. what: is? go, thing.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       this. what: is? go, thing.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As STring = "\b.*[.?!;:](\s|\z)"
      Dim input As String = "this. what: is? go, thing."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
      Next   
   End Sub
End Module
' The example displays the following output:
'       this. what: is? go, thing.
```

  > [!NOTE]
  > Poiché trova corrispondenza con ogni carattere, l'elemento di linguaggio viene spesso usato con un quantificatore lazy se un modello di espressione regolare tenta di trovare più volte corrispondenza con ogni carattere. Per altre informazioni, vedere [Quantificatori nelle espressioni regolari](quantifiers.md). 
 
## <a name="unicode-category-or-unicode-block-p"></a>Categoria Unicode o blocco Unicode: \p{}

Lo standard Unicode assegna una categoria generale a ogni carattere. Un carattere particolare può ad esempio essere una lettera maiuscola, rappresentata dalla categoria **Lu**, una cifra decimale, rappresentata dalla categoria **Nd**, un simbolo matematico, rappresentato dalla categoria **Sm** o un separatore di paragrafo, rappresentato dalla categoria **Zl**. Anche set di caratteri specifici nello standard Unicode occupano un intervallo specifico o un blocco di punti di codice consecutivi. Il set di caratteri latini è ad esempio compreso tra **\u0000** e **\u007F**, mentre il set di caratteri arabi tra **\u0600** e **\u06FF**. 

Costrutto dell'espressione regolare

**\p{**_name_**}**

trova corrispondenza con qualsiasi carattere appartenente a una categoria generale Unicode o a un blocco denominato, dove name è l'abbreviazione della categoria o il nome del blocco denominato. Per un elenco di abbreviazioni della categoria, vedere la sezione [Categorie generali Unicode supportate](#supported-unicode-general-categories) più avanti in questo argomento. Per un elenco dei blocchi denominati, vedere la sezione [Blocchi denominati supportati](#supported-named-blocks) più avanti in questo argomento. 

Nell'esempio seguente viene usato il costrutto **\p{**_name_**}** per individuare una corrispondenza per una categoria generale Unicode, in questo caso la categoria **Pd** (punteggiature o trattino) e un blocco denominato, vale a dire **IsGreek** e **IsBasicLatin**.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+";
      string input = "?ata ?a??a??? - The Gospel of Matthew";

      Console.WriteLine(Regex.IsMatch(input, pattern));        // Displays True.
   }
}
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+"
      Dim input As String = "Κατα Μαθθαίον - The Gospel of Matthew"

      Console.WriteLine(Regex.IsMatch(input, pattern))         ' Displays True.
   End Sub
End Module
```

L'espressione regolare `\b(\p{IsGreek}+(\s)?)+\p{Pd}\s(\p{IsBasicLatin}+(\s)?)+` viene definita come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`\p{IsGreek}+` | Corrisponde a uno o più caratteri greci.
`(\s)?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`(\p{IsGreek}+(\s)?)+` | Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri greci seguiti da zero o da uno spazio vuoto. 
`\p{Pd}` | Corrisponde a un carattere "Pd" (Punctuation, Dash).
`\s` | Trova la corrispondenza con uno spazio vuoto.
`\p{IsBasicLatin}+` | Corrisponde a uno o più caratteri latini di base.
`(\s)?` | Trova la corrispondenza di uno o nessuno spazio vuoto.
`(\p{IsBasicLatin}+(\s)?)+` | Ottiene una o più volte la corrispondenza con il modello di uno o più caratteri latini di base seguiti da zero o da uno spazio vuoto.

## <a name="negative-unicode-category-or-unicode-block-p"></a>Categoria Unicode negativa o blocco Unicode negativo: \P {}

Lo standard Unicode assegna una categoria generale a ogni carattere. Un carattere particolare può ad esempio essere una lettera maiuscola, rappresentata dalla categoria **Lu**, una cifra decimale, rappresentata dalla categoria **Nd**, un simbolo matematico, rappresentato dalla categoria **Sm** o un separatore di paragrafo, rappresentato dalla categoria **Zl**. Anche set di caratteri specifici nello standard Unicode occupano un intervallo specifico o un blocco di punti di codice consecutivi. Il set di caratteri latini è ad esempio compreso tra **\u0000** e **\u007F**, mentre il set di caratteri arabi tra **\u0600** e **\u06FF**. 

Costrutto dell'espressione regolare

**\P{**_name_**}**

trova corrispondenza con qualsiasi carattere appartenente a una categoria generale Unicode o a un blocco denominato, dove name è l'abbreviazione della categoria o il nome del blocco denominato. Per un elenco di abbreviazioni della categoria, vedere la sezione [Categorie generali Unicode supportate](#supported-unicode-general-categories) più avanti in questo argomento. Per un elenco dei blocchi denominati, vedere la sezione [Blocchi denominati supportati](#supported-named-blocks) più avanti in questo argomento.

L'esempio seguente usa il costrutto **\P{**_name_**}** per rimuovere qualsiasi simbolo di valuta, in questo caso la categoria **Sc** (simbolo o valuta) dalle stringhe numeriche.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\P{Sc})+";

      string[] values = { "$164,091.78", "£1,073,142.68", "73¢", "€120" };
      foreach (string value in values)
         Console.WriteLine(Regex.Match(value, pattern).Value);
   }
}
// The example displays the following output:
//       164,091.78
//       1,073,142.68
//       73
//       120
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\P{Sc})+"

      Dim values() As String = { "$164,091.78", "£1,073,142.68", "73¢", "€120"}
      For Each value As String In values
         Console.WriteLine(Regex.Match(value, pattern).Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       164,091.78
'       1,073,142.68
'       73
'       120
```

Il criterio di ricerca di espressioni regolari `(\P{Sc})+` corrisponde a uno o più caratteri che non siano simboli di valuta e rimuove efficacemente qualsiasi simbolo di valuta dalla stringa del risultato.

## <a name="word-character-w"></a>Carattere alfanumerico: \w

**\w** trova corrispondenza con qualsiasi carattere alfanumerico. Un carattere alfanumerico è un membro di una delle categorie Unicode elencate nella seguente tabella. 

Categoria | Descrizione
-------- | ----------- 
Ll | Letter, Lowercase
Lu | Letter, Uppercase
Lt | Letter, Titlecase
Lo | Letter, Other
Lm | Letter, Modifier
Mn | Mark, Nonspacing
Nd | Number, Decimal Digit
Pc | Punctuation, Connector. Questa categoria include dieci caratteri, tra cui quello più comunemente usato è (_) LOWLINE, u+005F.
 
Se viene specificato il comportamento conforme a ECMAScript, **\w** equivale a `[a-zA-Z_0-9]`. Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md). 

> [!NOTE]
> Poiché trova corrispondenza con qualsiasi carattere alfanumerico, l'elemento di linguaggio \w viene spesso usato con un quantificatore lazy se un modello di espressione regolare tenta di ottenere più volte una corrispondenza con ogni carattere alfanumerico, seguito da un carattere alfanumerico specifico. Per altre informazioni, vedere [Quantificatori nelle espressioni regolari](quantifiers.md).

Nell'esempio seguente viene usato l'elemento di linguaggio **\w** per trovare corrispondenza con i caratteri duplicati in una parola. L'esempio definisce un modello di espressione regolare, **(\w )\1**, che può essere interpretato nel modo seguente.

Elemento | Descrizione
------- | -----------
(\w) | Corrisponde a un carattere alfanumerico. Equivale al primo gruppo di acquisizione.
\1 | Corrisponde al valore della prima acquisizione. 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"(\w)\1";
      string[] words = { "trellis", "seer", "latter", "summer", 
                         "hoarse", "lesser", "aardvark", "stunned" };
      foreach (string word in words)
      {
         Match match = Regex.Match(word, pattern);
         if (match.Success)
            Console.WriteLine("'{0}' found in '{1}' at position {2}.", 
                              match.Value, word, match.Index);
         else
            Console.WriteLine("No double characters in '{0}'.", word);
      }                                                  
   }
}
// The example displays the following output:
//       'll' found in 'trellis' at position 3.
//       'ee' found in 'seer' at position 1.
//       'tt' found in 'latter' at position 2.
//       'mm' found in 'summer' at position 2.
//       No double characters in 'hoarse'.
//       'ss' found in 'lesser' at position 2.
//       'aa' found in 'aardvark' at position 0.
//       'nn' found in 'stunned' at position 3.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(\w)\1"
      Dim words() As String = { "trellis", "seer", "latter", "summer", _
                                "hoarse", "lesser", "aardvark", "stunned" }
      For Each word As String In words
         Dim match As Match = Regex.Match(word, pattern)
         If match.Success Then
            Console.WriteLine("'{0}' found in '{1}' at position {2}.", _
                              match.Value, word, match.Index)
         Else
            Console.WriteLine("No double characters in '{0}'.", word)
         End If
      Next                                                  
   End Sub
End Module
' The example displays the following output:
'       'll' found in 'trellis' at position 3.
'       'ee' found in 'seer' at position 1.
'       'tt' found in 'latter' at position 2.
'       'mm' found in 'summer' at position 2.
'       No double characters in 'hoarse'.
'       'ss' found in 'lesser' at position 2.
'       'aa' found in 'aardvark' at position 0.
'       'nn' found in 'stunned' at position 3.
```

## <a name="non-word-character-w"></a>Carattere non alfanumerico: \W

**\W** trova corrispondenza con qualsiasi carattere non alfanumerico. L'elemento di linguaggio **\W** equivale alla classe di caratteri seguente:

```
[^\p{Ll}\p{Lu}\p{Lt}\p{Lo}\p{Nd}\p{Pc}\p{Lm}]
```

In altre parole, trova corrispondenza con tutti i caratteri, ad eccezione di quelli nelle categorie Unicode elencati nella tabella seguente.

Categoria | Descrizione
-------- | -----------
Ll | Letter, Lowercase
Lu | Letter, Uppercase
Lt | Letter, Titlecase
Lo | Letter, Other
Lm | Letter, Modifier
Mn | Mark, Nonspacing
Nd | Number, Decimal Digit
Pc | Punctuation, Connector. Questa categoria include dieci caratteri, tra cui quello più comunemente usato è (_) LOWLINE, u+005F.
 
Se viene specificato il comportamento conforme a ECMAScript, **\W** equivale a `[^a-zA-Z_0-9]`. Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md). 

> [!NOTE]
> Poiché trova corrispondenza con qualsiasi carattere alfanumerico, l'elemento di linguaggio \w viene spesso usato con un quantificatore lazy se un modello di espressione regolare tenta di ottenere più volte una corrispondenza con ogni carattere alfanumerico, seguito da un carattere alfanumerico specifico. Per altre informazioni, vedere [Quantificatori nelle espressioni regolari](quantifiers.md). 

Nell'esempio seguente viene illustrata la classe di caratteri **\W**. Definisce un criterio di ricerca di espressioni regolari, `\b(\w+)(\W){1,2}`, che corrisponde a una parola seguita da uno o due caratteri non alfanumerici, ad esempio uno spazio vuoto o un segno di punteggiatura. L'espressione regolare viene interpretata come illustrato nella tabella seguente.

Elemento | Descrizione
------- | ----------- 
\b | Inizia la corrispondenza sul confine di parola.
(\w+) | Trova la corrispondenza di uno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
(\W){1,2} | Ottiene una o due volte una corrispondenza con un carattere non alfanumerico. Equivale al secondo gruppo di acquisizione.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\w+)(\W){1,2}";
      string input = "The old, grey mare slowly walked across the narrow, green pasture.";
      foreach (Match match in Regex.Matches(input, pattern))
      {
         Console.WriteLine(match.Value);
         Console.Write("   Non-word character(s):");
         CaptureCollection captures = match.Groups[2].Captures;
         for (int ctr = 0; ctr < captures.Count; ctr++)
             Console.Write(@"'{0}' (\u{1}){2}", captures[ctr].Value, 
                           Convert.ToUInt16(captures[ctr].Value[0]).ToString("X4"), 
                           ctr < captures.Count - 1 ? ", " : "");
         Console.WriteLine();
      }   
   }
}
// The example displays the following output:
//       The
//          Non-word character(s):' ' (\u0020)
//       old,
//          Non-word character(s):',' (\u002C), ' ' (\u0020)
//       grey
//          Non-word character(s):' ' (\u0020)
//       mare
//          Non-word character(s):' ' (\u0020)
//       slowly
//          Non-word character(s):' ' (\u0020)
//       walked
//          Non-word character(s):' ' (\u0020)
//       across
//          Non-word character(s):' ' (\u0020)
//       the
//          Non-word character(s):' ' (\u0020)
//       narrow,
//          Non-word character(s):',' (\u002C), ' ' (\u0020)
//       green
//          Non-word character(s):' ' (\u0020)
//       pasture.
//          Non-word character(s):'.' (\u002E)
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\w+)(\W){1,2}"
      Dim input As String = "The old, grey mare slowly walked across the narrow, green pasture."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)
         Console.Write("   Non-word character(s):")
         Dim captures As CaptureCollection = match.Groups(2).Captures
         For ctr As Integer = 0 To captures.Count - 1
             Console.Write("'{0}' (\u{1}){2}", captures(ctr).Value, _
                           Convert.ToUInt16(captures(ctr).Value.Chars(0)).ToString("X4"), _
                           If(ctr < captures.Count - 1, ", ", ""))
         Next
         Console.WriteLine()
      Next
   End Sub
End Module
' The example displays the following output:
'       The
'          Non-word character(s):' ' (\u0020)
'       old,
'          Non-word character(s):',' (\u002C), ' ' (\u0020)
'       grey
'          Non-word character(s):' ' (\u0020)
'       mare
'          Non-word character(s):' ' (\u0020)
'       slowly
'          Non-word character(s):' ' (\u0020)
'       walked
'          Non-word character(s):' ' (\u0020)
'       across
'          Non-word character(s):' ' (\u0020)
'       the
'          Non-word character(s):' ' (\u0020)
'       narrow,
'          Non-word character(s):',' (\u002C), ' ' (\u0020)
'       green
'          Non-word character(s):' ' (\u0020)
'       pasture.
'          Non-word character(s):'.' (\u002E)
```

Poiché l'oggetto `Group` per il secondo gruppo di acquisizione contiene un solo carattere non alfanumerico acquisito, nell'esempio vengono recuperati tutti i caratteri non alfanumerici acquisiti dall'oggetto `CaptureCollection` restituito dalla proprietà `Group.Captures`.

## <a name="white-space-character-s"></a>Spazio vuoto: \s

**\s** trova corrispondenza con qualsiasi spazio vuoto. È equivalente alle sequenze di escape e alle categorie Unicode elencate nella tabella seguente. 

Categoria | Descrizione
-------- | ----------- 
**\f** | Carattere di avanzamento modulo, \u000C.
**\n** | Carattere di nuova riga, \u000A.
**\r** | Carattere di ritorno a capo, \u000D.
**\t** | Carattere di tabulazione, \u0009.
**\v** | Carattere di tabulazione verticale, \u000B.
**\x85** | Puntini di sospensione o carattere NEXT LINE (NEL) (...), \u0085.
**\p{Z}** | Corrisponde a qualsiasi carattere separatore.
 

Se viene specificato il comportamento conforme a ECMAScript, **\s** equivale a `[ \f\n\r\t\v]`.  Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md). 

L'esempio seguente illustra la classe di caratteri \s. Definisce un criterio di ricerca di espressioni regolari, `\b\w+(e)?s(\s|$)`, che corrisponde a una parola che termina in "s" o "es" seguita da uno spazio vuoto o dalla fine della stringa di input. L'espressione regolare viene interpretata come illustrato nella tabella seguente.

Elemento | Descrizione
------- | -----------
\b | Inizia la corrispondenza sul confine di parola.
\w+ | Trova la corrispondenza di uno o più caratteri alfanumerici. 
(e)? | Ottiene zero o una volta la corrispondenza con una "e".
s | Corrisponde a una "s".
(\s&#124;$) | Corrisponde a uno spazio vuoto o alla fine della stringa di input.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b\w+(e)?s(\s|$)";
      string input = "matches stores stops leave leaves";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Value);
   }
}
// The example displays the following output:
//       matches
//       stores
//       stops
//       leaves
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b\w+(e)?s(\s|$)"
      Dim input As String = "matches stores stops leave leaves"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Value)      
      Next
   End Sub
End Module
' The example displays the following output:
'       matches
'       stores
'       stops
'       leaves
```

## <a name="non-white-space-character-s"></a>Carattere diverso da uno spazio vuoto: \S

**\S** trova corrispondenza con qualsiasi carattere diverso da uno spazio vuoto. Equivale al modello di espressione regolare `[^\f\n\r\t\v\x85\p{Z}]` o è il contrario del modello di espressione regolare equivalente a **\s**, che trova corrispondenza con gli spazi vuoti. Per altre informazioni, vedere la sezione precedente "Spazio vuoto: \s".

Se viene specificato il comportamento conforme a ECMAScript, **\S** equivale a `[^ \f\n\r\t\v]`. Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md).

Nell'esempio seguente viene illustrato l'elemento di linguaggio **\S**. Il modello di espressione regolare \b(\S+)\s? trova corrispondenza con stringhe delimitate da spazi vuoti. Il secondo elemento nell'oggetto di corrispondenza GroupCollection contiene la stringa corrispondente. L'espressione regolare può essere interpretata come indicato nella tabella seguente.

Elemento | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`(\S+)` | Trova la corrispondenza con uno o più caratteri diversi dallo spazio vuoto. Equivale al primo gruppo di acquisizione.
`\s?` | Trova la corrispondenza di uno o nessuno spazio vuoto. 
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"\b(\S+)\s?";
      string input = "This is the first sentence of the first paragraph. " + 
                            "This is the second sentence.\n" + 
                            "This is the only sentence of the second paragraph.";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine(match.Groups[1]);
   }
}
// The example displays the following output:
//    This
//    is
//    the
//    first
//    sentence
//    of
//    the
//    first
//    paragraph.
//    This
//    is
//    the
//    second
//    sentence.
//    This
//    is
//    the
//    only
//    sentence
//    of
//    the
//    second
//    paragraph.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "\b(\S+)\s?"
      Dim input As String = "This is the first sentence of the first paragraph. " + _
                            "This is the second sentence." + vbCrLf + _
                            "This is the only sentence of the second paragraph."
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine(match.Groups(1))
      Next
   End Sub
End Module
' The example displays the following output:
'    This
'    is
'    the
'    first
'    sentence
'    of
'    the
'    first
'    paragraph.
'    This
'    is
'    the
'    second
'    sentence.
'    This
'    is
'    the
'    only
'    sentence
'    of
'    the
'    second
'    paragraph.
```

## <a name="decimal-digit-character-d"></a>Carattere cifra decimale: \d

**\d** trova corrispondenza con qualsiasi cifra decimale. È equivalente al criterio di ricerca di espressioni regolari `\\p{Nd}` che include le cifre decimali standard da 0 a 9 e le cifre decimali di diversi altri set di caratteri.

Se viene specificato il comportamento conforme a ECMAScript, **\d** equivale a `[0-9]`. Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md).

Nell'esempio seguente viene illustrato l'elemento di linguaggio **\d**. Viene verificato se una stringa di input rappresenta un numero di telefono valido negli Stati Uniti e in Canada. Il criterio di ricerca di espressioni regolari `^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$` è definito nel modo illustrato nella tabella seguente.

Elemento | Descrizione
------- | ----------- 
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`\(?` | Corrisponde a zero o a un carattere letterale "(". 
`\d{3}` | Trova la corrispondenza con tre cifre decimali. 
`\)?` | Corrisponde a zero o a un carattere letterale ")".
`[\s-]` | Corrisponde a un trattino o a uno spazio vuoto.
`(\(?\d{3}\)?[\s-])?` | Trova la corrispondenza zero o una volta con una parentesi di apertura facoltativa seguita da tre cifre decimali, una parentesi di chiusura facoltativa e uno spazio vuoto o un trattino. Equivale al primo gruppo di acquisizione.
`\d{3}-\d{4}` | Corrisponde a tre cifre decimali seguite da un trattino e da altre quattro cifre decimali.
`$` | Trova la corrispondenza con la fine della stringa di input.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$";
      string[] inputs = { "111 111-1111", "222-2222", "222 333-444", 
                          "(212) 111-1111", "111-AB1-1111", 
                          "212-111-1111", "01 999-9999" };

      foreach (string input in inputs)
      {
         if (Regex.IsMatch(input, pattern)) 
            Console.WriteLine(input + ": matched");
         else
            Console.WriteLine(input + ": match failed");
      }
   }
}
// The example displays the following output:
//       111 111-1111: matched
//       222-2222: matched
//       222 333-444: match failed
//       (212) 111-1111: matched
//       111-AB1-1111: match failed
//       212-111-1111: matched
//       01 999-9999: match failed
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^(\(?\d{3}\)?[\s-])?\d{3}-\d{4}$"
      Dim inputs() As String = { "111 111-1111", "222-2222", "222 333-444", _
                                 "(212) 111-1111", "111-AB1-1111", _
                                 "212-111-1111", "01 999-9999" }

      For Each input As String In inputs
         If Regex.IsMatch(input, pattern) Then 
            Console.WriteLine(input + ": matched")
         Else
            Console.WriteLine(input + ": match failed")
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
'       111 111-1111: matched
'       222-2222: matched
'       222 333-444: match failed
'       (212) 111-1111: matched
'       111-AB1-1111: match failed
'       212-111-1111: matched
'       01 999-9999: match failed
```

## <a name="non-digit-character-d"></a>Carattere non numerico: \D

**\D** trova corrispondenza con qualsiasi carattere non numerico. È equivalente al criterio di ricerca di espressioni regolari `\P{Nd}`.

Se viene specificato il comportamento conforme a ECMAScript, **\D** equivale a `[^0-9]`. Per informazioni sulle espressioni regolari ECMAScript, vedere la sezione [Comportamento di corrispondenza ECMAScript](options.md#ecmascript-matching-behavior) in [Opzioni di espressioni regolari](options.md).

Nell'esempio seguente viene illustrato l'elemento di linguaggio **\D**. Verifica se una stringa, ad esempio un numero parte, è formata dalla combinazione corretta di caratteri decimali e non decimali. Il criterio di ricerca di espressioni regolari `^\D\d{1,5}\D*$` è definito nel modo illustrato nella tabella seguente.

Elemento | Descrizione
------- | ----------- 
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`\D` | Corrisponde a un carattere non numerico. 
`\d{1,5}` | Corrisponde a una fino a cinque cifre decimali. 
`\D*` | Corrisponde a zero, uno o più caratteri non decimali. 
`$` | Trova la corrispondenza con la fine della stringa di input.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = @"^\D\d{1,5}\D*$"; 
      string[] inputs = { "A1039C", "AA0001", "C18A", "Y938518" }; 

      foreach (string input in inputs)
      {
         if (Regex.IsMatch(input, pattern))
            Console.WriteLine(input + ": matched");
         else
            Console.WriteLine(input + ": match failed");
      }
   }
}
// The example displays the following output:
//       A1039C: matched
//       AA0001: match failed
//       C18A: matched
//       Y938518: match failed
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "^\D\d{1,5}\D*$" 
      Dim inputs() As String = { "A1039C", "AA0001", "C18A", "Y938518" } 

      For Each input As String In inputs
         If Regex.IsMatch(input, pattern) Then
            Console.WriteLine(input + ": matched")
         Else
            Console.WriteLine(input + ": match failed")
         End If   
      Next
   End Sub
End Module
' The example displays the following output:
```

## <a name="supported-unicode-general-categories"></a>Categorie generali Unicode supportate

In Unicode sono definite le categorie generali elencate nella tabella riportata di seguito. Per altre informazioni, vedere gli argomenti correlati "UCD File Format" (Formato di file UCD) e "General Category Values" (Valori di categoria generale) in [Unicode Character Database](http://www.unicode.org/reports/tr44/) (Database di caratteri Unicode).

Categoria | Descrizione
-------- | -----------
**Lu** | Letter, Uppercase
**Ll** | Letter, Lowercase
**Lt** | Letter, Titlecase
**Lm** | Letter, Modifier
**Lo** | Letter, Other
**L** | Tutti i caratteri alfanumerici. Sono inclusi i caratteri **Lu**, **Ll**, **Lt**, **Lm** e **Lo**.
**Mn** | Mark, Nonspacing
**Mc** | Mark, Spacing Combining
**Me** | Mark, Enclosing
**M** | Tutti i contrassegni diacritici. Sono incluse le categorie **Mn**, **Mc** e **Me**.
**Nd** | Number, Decimal Digit
**Nl** | Number, Letter
**No** | Number, Other
**N** | Tutti i numeri. Sono incluse le categorie **Nd**, **Nl** e **No**.
**Pc** | Punctuation, Connector
**Pd** | Punctuation, Dash
**Ps** | Punctuation, Open
**Pe** | Punctuation, Close
**Pi** | Punctuation, Initial quote (può comportarsi come Ps o Pe a seconda dell'utilizzo)
**Pf** | Punctuation, Final quote (può comportarsi come Ps o Pe a seconda dell'utilizzo)
**Po** | Punctuation, Other
**P** | Tutti i caratteri di punteggiatura. Sono incluse le categorie **Pc**, **Pd**, **Ps**, **Pe**, **Pi**, **Pf** e **Po**.
**Sm** | Symbol, Math
**Sc** | Symbol, Currency
**Sk** | Symbol, Modifier
**So** | Symbol, Other
**S** | Tutti i simboli. Sono incluse le categorie **Sm**, **Sc**, **Sk**, e **So**.
**Zs** | Separator, Space
**Zl** | Separator, Line
**Zp** | Separator, Paragraph
**Z** | Tutti i caratteri separatori. Sono incluse le categorie **Zs**, **Zl** e **Zp**.
**Cc** | Other, Control
**Cf** | Other, Format
**Cs** | Other, Surrogate
**Co** | Other, Private Use
**Cn** | Other, Not Assigned (nessun carattere ha questa proprietà)
**C** | Tutti i caratteri di controllo. Sono incluse le categorie **Cc**, **Cf**, **Cs**, **Co** e **Cn**.
 
##<a name="supported-named-blocks"></a>Blocchi denominati supportati

In .NET sono supportati i blocchi denominati elencati nella tabella seguente. Il set di blocchi denominati supportati è basato su Unicode 4.0 e Perl 5.6.

Intervallo di punti di codice | Nome del blocco
---------------- | ---------- 
0000 - 007F | **IsBasicLatin**
0080 - 00FF | **IsLatin-1Supplement**
0100 - 017F | **IsLatinExtended-A**
0180 - 024F | **IsLatinExtended-B**
0250 - 02AF | **IsIPAExtensions**
02B0 - 02FF | **IsSpacingModifierLetters**
0300 - 036F | **IsCombiningDiacriticalMarks**
0370 - 03FF | **IsGreek** o **IsGreekandCoptic**
0400 - 04FF | **IsCyrillic**
0500 - 052F | **IsCyrillicSupplement**
0530 - 058F | **IsArmenian**
0590 - 05FF | **IsHebrew**
0600 - 06FF | **IsArabic**
0700 - 074F | **IsSyriac**
0780 - 07BF | **IsThaana**
0900 - 097F | **IsDevanagari**
0980 - 09FF | **IsBengali**
0A00 - 0A7F | **IsGurmukhi**
0A80 - 0AFF | **IsGujarati**
0B00 - 0B7F | **IsOriya**
0B80 - 0BFF | **IsTamil**
0C00 - 0C7F | **IsTelugu**
0C80 - 0CFF | **IsKannada**
0D00 - 0D7F | **IsMalayalam**
0D80 - 0DFF | **IsSinhala**
0E00 - 0E7F | **IsThai**
0E80 - 0EFF | **IsLao**
0F00 - 0FFF | **IsTibetan**
1000 - 109F | **IsMyanmar**
10A0 - 10FF | **IsGeorgian**
1100 - 11FF | **IsHangulJamo**
1200 - 137F | **IsEthiopic**
13A0 - 13FF | **IsCherokee**
1400 - 167F | **IsUnifiedCanadianAboriginalSyllabics**
1680 - 169F | **IsOgham**
16A0 - 16FF | **IsRunic**
1700 - 171F | **IsTagalog**
1720 - 173F | **IsHanunoo**
1740 - 175F | **IsBuhid**
1760 - 177F | **IsTagbanwa**
1780 - 17FF | **IsKhmer**
1800 - 18AF | **IsMongolian**
1900 - 194F | **IsLimbu**
1950 - 197F | **IsTaiLe**
19E0 - 19FF | **IsKhmerSymbols**
1D00 - 1D7F | **IsPhoneticExtensions**
1E00 - 1EFF | **IsLatinExtendedAdditional**
1F00 - 1FFF | **IsGreekExtended**
2000 - 206F | **IsGeneralPunctuation**
2070 - 209F | **IsSuperscriptsandSubscripts**
20A0 - 20CF | **IsCurrencySymbols**
20D0 - 20FF | **IsCombiningDiacriticalMarksforSymbols** o **IsCombiningMarksforSymbols**
2100 - 214F | **IsLetterlikeSymbols**
2150 - 218F | **IsNumberForms**
2190 - 21FF | **IsArrows**
2200 - 22FF | **IsMathematicalOperators**
2300 - 23FF | **IsMiscellaneousTechnical**
2400 - 243F | **IsControlPictures**
2440 - 245F | **IsOpticalCharacterRecognition**
2460 - 24FF | **IsEnclosedAlphanumerics**
2500 - 257F | **IsBoxDrawing**
2580 - 259F | **IsBlockElements**
25A0 - 25FF | **IsGeometricShapes**
2600 - 26FF | **IsMiscellaneousSymbols**
2700 - 27BF | **IsDingbats**
27C0 - 27EF | **IsMiscellaneousMathematicalSymbols-A**
27F0 - 27FF | **IsSupplementalArrows-A**
2800 - 28FF | **IsBraillePatterns**
2900 - 297F | **IsSupplementalArrows-B**
2980 - 29FF | **IsMiscellaneousMathematicalSymbols-B**
2A00 - 2AFF | **IsSupplementalMathematicalOperators**
2B00 - 2BFF | **IsMiscellaneousSymbolsandArrows**
2E80 - 2EFF | **IsCJKRadicalsSupplement**
2F00 - 2FDF | **IsKangxiRadicals**
2FF0 - 2FFF | **IsIdeographicDescriptionCharacters**
3000 - 303F | **IsCJKSymbolsandPunctuation**
3040 - 309F | **IsHiragana**
30A0 - 30FF | **IsKatakana**
3100 - 312F | **IsBopomofo**
3130 - 318F | **IsHangulCompatibilityJamo**
3190 - 319F | **IsKanbun**
31A0 - 31BF | **IsBopomofoExtended**
31F0 - 31FF | **IsKatakanaPhoneticExtensions**
3200 - 32FF | **IsEnclosedCJKLettersandMonths**
3300 - 33FF | **IsCJKCompatibility**
3400 - 4DBF | **IsCJKUnifiedIdeographsExtensionA**
4DC0 - 4DFF | **IsYijingHexagramSymbols**
4E00 - 9FFF | **IsCJKUnifiedIdeographs**
A000 - A48F | **IsYiSyllables**
A490 - A4CF | **IsYiRadicals**
AC00 - D7AF | **IsHangulSyllables**
D800 - DB7F | **IsHighSurrogates**
DB80 - DBFF | **IsHighPrivateUseSurrogates**
DC00 - DFFF | **IsLowSurrogates**
E000 - F8FF | **IsPrivateUse** o **IsPrivateUseArea**
F900 - FAFF | **IsCJKCompatibilityIdeographs**
FB00 - FB4F | **IsAlphabeticPresentationForms** 
FB50 - FDFF | **IsArabicPresentationForms-A** 
FE00 - FE0F | **IsVariationSelectors** 
FE20 - FE2F | **IsCombiningHalfMarks** 
FE30 - FE4F | **IsCJKCompatibilityForms** 
FE50 - FE6F | **IsSmallFormVariants**
FE70 - FEFF | **IsArabicPresentationForms-B** 
FF00 - FFEF | **IsHalfwidthandFullwidthForms** 
FFF0 - FFFF | **IsSpecials**
 
<a name="character-class-subtraction"></a>
## <a name="character-class-subtraction-basegroup---excludedgroup"></a>Sottrazione di classi di caratteri: [base_group - excluded_group] []

Una classe di caratteri definisce un set di caratteri. La sottrazione di classi di caratteri produce un set di caratteri che è il risultato dell'esclusione dei caratteri di una classe di caratteri da un'altra classe di caratteri. 

Un'espressione di sottrazione di classi di caratteri ha il formato seguente:

__[__*base*_*group*-__[__*excluded*_*group*__]]--

Le parentesi quadre (**[]**) e il trattino (-) sono obbligatori. *base_group* è un gruppo di caratteri positivi o un gruppo di caratteri negativi. Il componente *excluded_group* è un altro gruppo di caratteri positivi o negativi o un'altra espressione di sottrazione di classi di caratteri, ovvero è possibile annidare espressioni di sottrazione di classi di caratteri. 

Si supponga ad esempio di disporre di un gruppo di base costituito dall'intervallo di caratteri compresi tra "a" e "z". Per definire il set di caratteri costituito dal gruppo di base con l'esclusione del carattere "m", usare `[a-z-[m]]`. Per definire il set di caratteri costituito dal gruppo di base con l'esclusione del set di caratteri "d", "j" e "p", usare `[a-z-[djp]]`. Per definire il set di caratteri costituito dal gruppo di base con l'esclusione dell'intervallo di caratteri compresi tra "m" e "p", usare `[a-z-[m-p]]`. 

Si consideri l'espressione di sottrazione di classi di caratteri annidata `[a-z-[d-w-[m-o]]]`. L'espressione viene valutata partendo dall'intervallo di caratteri più interno verso quello più esterno. Innanzitutto, l'intervallo di caratteri compresi tra "m" e "o" viene sottratto dall'intervallo di caratteri compresi tra "d" e "w", producendo il set di caratteri compresi tra "d" e "l" e tra "p" e "w". Tale set viene quindi sottratto dall'intervallo di caratteri compreso tra "a" e "z", producendo il set di caratteri `[abcmnoxyz]`.

È possibile usare qualsiasi classe di caratteri con sottrazione di classi di caratteri. Per definire il set di caratteri costituito da tutti i caratteri Unicode compresi tra \u0000 e \uFFFF ad eccezione degli spazi vuoti (**\s**), i caratteri nella categoria generale punteggiatura (**\p{P}**), i caratteri nel blocco denominato **IsGreek** (**\p{IsGreek}**) e il carattere di controllo NEXT LINE Unicode (\x85), usare `[\u0000-\uFFFF-[\s\p{P}\p{IsGreek}\x85]]`.

Scegliere le classi di caratteri per un'espressione di sottrazione di classi di caratteri che produrrà risultati utili. Evitare espressioni che producono set di caratteri vuoti, che non hanno corrispondenze o che equivalgono al gruppo di base originale. Ad esempio, il set vuoto è il risultato dell'espressione `[\p{IsBasicLatin}-[\x00-\x7F]]`, che sottrae tutti i caratteri compresi nell'intervallo di caratteri **IsBasicLatin** dalla categoria generale **IsBasicLatin**. Analogamente, il gruppo di base originale è il risultato dell'espressione `[a-z-[0-9]]`. Questo è dovuto al fatto che il gruppo di base, ovvero l'intervallo dei caratteri compresi tra le lettere "a" e "z", non contiene alcun carattere del gruppo escluso, ovvero dell'intervallo dei caratteri compresi tra le cifre decimali "0" e "9". 

Nell'esempio seguente viene definita un'espressione regolare, `^[0-9-[2468]]+$`, che corrisponde a zero e a cifre dispari in una stringa di input. L'espressione regolare viene interpretata come illustrato nella tabella seguente.

Elemento | Descrizione
------- | ----------- 
`^` | Inizia la corrispondenza all'inizio della stringa di input.
`[0-9-[2468]]+` | Corrisponde a una o più occorrenze di qualsiasi carattere da 0 a 9 ad eccezione di 2, 4, 6 e 8. In altre parole, corrisponde a una o più occorrenze di zero o di una cifra dispari.
`$` | Termina la ricerca della corrispondenza alla fine della stringa di input.
 
```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "123", "13579753", "3557798", "335599901" };
      string pattern = @"^[0-9-[2468]]+$";

      foreach (string input in inputs)
      {
         Match match = Regex.Match(input, pattern);
         if (match.Success) 
            Console.WriteLine(match.Value);
      }      
   }
}
// The example displays the following output:
//       13579753
//       335599901
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "123", "13579753", "3557798", "335599901" }
      Dim pattern As String = "^[0-9-[2468]]+$"

      For Each input As String In inputs
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then Console.WriteLine(match.Value)
      Next
   End Sub
End Module
' The example displays the following output:
'       13579753
'       335599901
```

## <a name="see-also"></a>Vedere anche

[Opzioni di espressioni regolari](options.md)
