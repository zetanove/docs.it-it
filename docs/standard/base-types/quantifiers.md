---
title: Quantificatori in espressioni regolari
description: Quantificatori in espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/29/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 8e5124c4-20b5-4c57-ab68-301d1d7311c4
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: cd47cc351fb926bcf444bdcbd12f3cd61d9fb327
ms.lasthandoff: 03/02/2017

---

# <a name="quantifiers-in-regular-expressions"></a>Quantificatori in espressioni regolari

I quantificatori specificano il numero di istanze di un carattere, un gruppo o una classe di caratteri che deve essere presente nell'input affinché venga trovata una corrispondenza. Nella tabella seguente vengono elencati i quantificatori supportati da .NET.

Quantificatore greedy | Quantificatore lazy | Descrizione
----------------- | --------------- | ----------- 
**\*** | **\*?** | Trova la corrispondenza zero o più volte.
**+** | **+?** | Trova la corrispondenza una o più volte.
**?** | **??** | Trova la corrispondenza zero o una volta.
**{**_n_**}** | **{**_n_**}?** | Trova la corrispondenza esatta n volte.
**{**_n_**,}** | **{**_n_**,}?** | Trova la corrispondenza almeno n volte.
**{**_n_**,**_m_**}** | **{**_n_**,**_m_**}?** | Trova la corrispondenza da n a m volte.
 
Le quantità *n* e *m* sono costanti integer. In genere, i quantificatori sono greedy: il motore delle espressioni regolari trova la corrispondenza con il maggior numero possibile di determinati criteri. L'aggiunta del carattere `?` rende un quantificatore lazy: il motore delle espressioni regolari trova la corrispondenza con il minor numero possibile di occorrenze. Per una descrizione completa della differenza tra quantificatori greedy e lazy, vedere la sezione [Quantificatori greedy e lazy](#greedy-and-lazy-quantifiers) più avanti in questo argomento.

> [!IMPORTANT]
> Annidare i quantificatori, come nel caso del criterio di espressione regolare `(a*)*`, può aumentare il numero dei confronti che deve eseguire il motore delle espressioni regolari, come una funzione esponenziale del numero di caratteri nella stringa di input. Per altre informazioni su questo comportamento e sulle relative soluzioni alternative, vedere [Backtracking nelle espressioni regolari](backtracking.md).

## <a name="regular-expression-quantifiers"></a>Quantificatori delle espressioni regolari

Nelle sezioni seguenti sono riportati i quantificatori supportati dalle espressioni regolari in .NET. 

> [!NOTE]
> Se vengono rilevati i caratteri \*, +,?, { e} in un criterio di espressione regolare, il motore delle espressioni regolari li interpreta come quantificatori o parte di costrutti di quantificatori a meno che non siano inclusi in una [classe di caratteri](classes.md). Per interpretarli come caratteri letterali all'esterno di una classe di caratteri, è necessaria una sequenza di escape con i caratteri preceduti da una barra rovesciata. Ad esempio, la stringa `\*` in un'espressione regolare viene interpretata come carattere letterale asterisco ("*").

### <a name="match-zero-or-more-times-"></a>Trova la corrispondenza zero o più volte: \*

Il quantificatore \* trova la corrispondenza con l'elemento precedente zero o più volte. È equivalente al quantificatore **{0,}**. **\*** è un quantificatore greedy il cui equivalente lazy è **\*?**.

L'esempio seguente illustra questa espressione regolare. Delle nove cifre nella stringa di input, cinque corrispondono al criterio e quattro (`95`, `929`, `9129` e `9919`) no.

```csharp
string pattern = @"\b91*9*\b";   
string input = "99 95 919 929 9119 9219 999 9919 91119";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//       '99' found at position 0.
//       '919' found at position 6.
//       '9119' found at position 14.
//       '999' found at position 24.
//       '91119' found at position 33.
```

```vb
Dim pattern As String = "\b91*9*\b"   
Dim input As String = "99 95 919 929 9119 9219 999 9919 91119"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:   
'       '99' found at position 0.
'       '919' found at position 6.
'       '9119' found at position 14.
'       '999' found at position 24.
'       '91119' found at position 33.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`91*` | Trova un "9" seguito da zero o più caratteri "1".
`9*` | Trova la corrispondenza con zero o più caratteri "9".
`\b` | Terminare al confine di una parola.
 
### <a name="match-one-or-more-times-"></a>Trova la corrispondenza una o più volte: +

Il quantificatore **+** trova la corrispondenza con l'elemento precedente una o più volte. Equivale a **{1,}**. **+** è un quantificatore greedy il cui equivalente lazy è **+?**.

Ad esempio, l'espressione regolare `\ban+\w*?\b` tenta di trovare la corrispondenza con intere parole che iniziano con la lettera `a` seguita da una o più istanze della lettera `n`. L'esempio seguente illustra questa espressione regolare. L'espressione regolare trova le parole `an`, `annual`, `announcement`, `antique` e, correttamente, non riesce a trovare `autumn` e `all`.

```csharp
string pattern = @"\ban+\w*?\b";

string input = "Autumn is a great time for an annual announcement to all antique collectors.";
foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//       'an' found at position 27.
//       'annual' found at position 30.
//       'announcement' found at position 37.
//       'antique' found at position 57.      
```

```vb
Dim pattern As String = "\ban+\w*?\b"

Dim input As String = "Autumn is a great time for an annual announcement to all antique collectors."
For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next   
' The example displays the following output:   
'       'an' found at position 27.
'       'annual' found at position 30.
'       'announcement' found at position 37.
'       'antique' found at position 57. 
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`an+` | Trova una "a" seguita da uno o più caratteri "n". 
`\w*?` | Trova la corrispondenza con un carattere alfanumerico o più volte, ma il minor numero di volte possibile.
`\b` | Terminare al confine di una parola.
 
### <a name="match-zero-or-one-time-"></a>Trova la corrispondenza zero o una volta: ?

Il quantificatore **?** trova la corrispondenza con l'elemento precedente zero o una volta. Equivale a **{0,1}**. **?** è un quantificatore greedy il cui equivalente lazy è **??**.

Ad esempio, l'espressione regolare `\ban?\b` tenta di trovare la corrispondenza con intere parole che iniziano con la lettera `a` seguita da zero o una istanza della lettera `n`. In altre parole, tenta di trovare la corrispondenza con le parole `a` e `an`. L'esempio seguente illustra questa espressione regolare.

```csharp
string pattern = @"\ban?\b";
string input = "An amiable animal with a large snount and an animated nose.";
foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

// The example displays the following output:   
//        'An' found at position 0.
//        'a' found at position 23.
//        'an' found at position 42.
```

```vb
Dim pattern As String = "\ban?\b"
Dim input As String = "An amiable animal with a large snount and an animated nose."
For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next  
' The example displays the following output:   
'       'An' found at position 0.
'       'a' found at position 23.
'       'an' found at position 42.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`an?` | Trova una "a" seguita da zero o un carattere "n". 
`\b` | Terminare al confine di una parola.
 
### <a name="match-exactly-n-times-n"></a>Trova la corrispondenza esatta n volte: {n}

Il quantificatore **{**_n_**}** trova la corrispondenza con l'elemento precedente esattamente *n* volte, dove *n* è qualsiasi numero intero. **{**_n_**}**è un quantificatore greedy il cui equivalente lazy è **{**_n_**}?**.

Ad esempio, l'espressione regolare `\b\d+\,\d{3}\b` tenta di trovare la corrispondenza con il confine di una parola seguito da una o più cifre decimali seguite da tre cifre decimali seguite dal confine di una parola. L'esempio seguente illustra questa espressione regolare. 

```csharp
string pattern = @"\b\d+\,\d{3}\b";
string input = "Sales totaled 103,524 million in January, " + 
                      "106,971 million in February, but only " + 
                      "943 million in March.";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:   
//        '103,524' found at position 14.
//        '106,971' found at position 45.
```

```vb
Dim pattern As String = "\b\d+\,\d{3}\b"
Dim input As String = "Sales totaled 103,524 million in January, " + _
                      "106,971 million in February, but only " + _
                      "943 million in March."
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:   
'       '103,524' found at position 14.
'       '106,971' found at position 45.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`\d+` | Trova la corrispondenza con una o più cifre decimali. 
`\,` | Trova la corrispondenza con un carattere virgola.
`\d{3}` | Trova la corrispondenza con tre cifre decimali.
`\b` | Terminare al confine di una parola.
 
### <a name="match-at-least-n-times-n"></a>Trova la corrispondenza almeno n volte: {n,}

Il quantificatore **{**_n_**,}** trova la corrispondenza con l'elemento precedente almeno *n* volte, dove *n* è qualsiasi numero intero. **{**_n_**,}**è un quantificatore greedy il cui equivalente lazy è **{**_n_**}?**.

Ad esempio, l'espressione regolare `\b\d{2,}\b\D+` tenta di trovare la corrispondenza con il confine di una parola seguito da almeno due cifre seguite dal confine di una parola e un carattere non numerico. L'esempio seguente illustra questa espressione regolare. L'espressione regolare non riesce a trovare la frase "7 days" perché contiene solo una cifra decimale, ma trova la corrispondenza con le frasi "10 weeks e 300 years".

```csharp
string pattern = @"\b\d{2,}\b\D+";   
string input = "7 days, 10 weeks, 300 years";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        '10 weeks, ' found at position 8.
// 
``` 

```vb
Dim pattern As String = "\b\d{2,}\b\D+"  
 Dim input As String = "7 days, 10 weeks, 300 years"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       '10 weeks, ' found at position 8.
'       '300 years' found at position 18.
      '300 years' found at position 18.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`\d{2,}` | Trova la corrispondenza con almeno due cifre decimali. 
`\b` | Trova la corrispondenza di un confine di parola.
`\D+` | Trova la corrispondenza con almeno una cifra non decimale.
 
### <a name="match-between-n-and-m-times-nm"></a>Trova la corrispondenza tra n e m volte: {n,m}

Il quantificatore **{**_n_**,**_m_**}** trova la corrispondenza con l'elemento precedente almeno *n* volte, ma non più di *m* volte, dove *n* e *m* sono numeri interi. **{**_n_**,**_m_**}** è un quantificatore greedy il cui equivalente lazy è **{**_n_**,**_m_**}?**.

Nell'esempio seguente, l'espressione regolare `(00\s){2,4}` tenta di trovare una corrispondenza tra due e quattro occorrenze di due cifre zero seguite da uno spazio. Si noti che la parte finale della stringa di input include questo criterio cinque volte anziché il numero massimo di quattro. Tuttavia, solo la parte iniziale della sottostringa (fino allo spazio e alla quinta coppia di zeri) corrisponde al criterio dell'espressione regolare.

```csharp
string pattern = @"(00\s){2,4}";
string input = "0x00 FF 00 00 18 17 FF 00 00 00 21 00 00 00 00 00";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        '00 00 ' found at position 8.
//        '00 00 00 ' found at position 23.
//        '00 00 00 00 ' found at position 35.
```

```vb
Dim pattern As String = "(00\s){2,4}"
Dim input As String = "0x00 FF 00 00 18 17 FF 00 00 00 21 00 00 00 00 00"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       '00 00 ' found at position 8.
'       '00 00 00 ' found at position 23.
'       '00 00 00 00 ' found at position 35.
```

### <a name="match-zero-or-more-times-lazy-match-"></a>Trova la corrispondenza zero o più volte (corrispondenza lazy): \*?

Il quantificatore **\*?** trova la corrispondenza con l'elemento precedente zero o più volte, ma il minor numero di volte possibile. Si tratta della controparte lazy del quantificatore greedy **\***.

Nell'esempio seguente l'espressione regolare `\b\w*?oo\w*?\b` corrisponde a tutte le parole contenenti la stringa `oo`. 

```csharp
 string pattern = @"\b\w*?oo\w*?\b";
 string input = "woof root root rob oof woo woe";
 foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
    Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

 //  The example displays the following output:
//        'woof' found at position 0.
//        'root' found at position 5.
//        'root' found at position 10.
//        'oof' found at position 19.
//        'woo' found at position 23.
```

```vb
Dim pattern As String = "\b\w*?oo\w*?\b"
 Dim input As String = "woof root root rob oof woo woe"
 For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
    Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
 Next 
 ' The example displays the following output:
'       'woof' found at position 0.
'       'root' found at position 5.
'       'root' found at position 10.
'       'oof' found at position 19.
'       'woo' found at position 23.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia dal confine di una parola.
`\w*?` | Trova la corrispondenza con zero o più caratteri alfanumerici, ma il minor numero di caratteri possibile. 
`oo` | Trova la corrispondenza con la stringa "oo".
`\w*?` | Trova la corrispondenza con zero o più caratteri alfanumerici, ma il minor numero di caratteri possibile.
`\b` | Termina al confine di una parola.
 
### <a name="match-one-or-more-times-lazy-match-"></a>Trova la corrispondenza una o più volte (corrispondenza lazy): +?

Il quantificatore **+?** trova la corrispondenza con l'elemento precedente una o più volte, ma il minor numero di volte possibile. Si tratta della controparte lazy del quantificatore greedy **+**.

Ad esempio, l'espressione regolare `\b\w+?\b` trova la corrispondenza con uno o più caratteri separati confini di parole. L'esempio seguente illustra questa espressione regolare.

```csharp
string pattern = @"\b\w+?\b";
string input = "Aa Bb Cc Dd Ee Ff";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'Aa' found at position 0.
//        'Bb' found at position 3.
//        'Cc' found at position 6.
//        'Dd' found at position 9.
//        'Ee' found at position 12.
//        'Ff' found at position 15.
```

```vb
Dim pattern As String = "\b\w+?\b"
 Dim input As String = "Aa Bb Cc Dd Ee Ff"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'Aa' found at position 0.
'       'Bb' found at position 3.
'       'Cc' found at position 6.
'       'Dd' found at position 9.
'       'Ee' found at position 12.
'       'Ff' found at position 15.
```

### <a name="match-zero-or-one-time-lazy-match-"></a>Trova la corrispondenza zero o una volta (corrispondenza lazy): ??

Il quantificatore **??** trova la corrispondenza con l'elemento precedente zero o una volta, ma il minor numero di volte possibile. Si tratta della controparte lazy del quantificatore greedy **?**.

Ad esempio, l'espressione regolare `^\s*(System.)??Console.Write(Line)??\(??` tenta di trovare la corrispondenza con le stringhe "Console.Write" o "Console.WriteLine". La stringa può anche includere "System." prima di "Console" e può essere seguita da una parentesi di apertura. La stringa deve essere all'inizio di una riga, anche se può essere preceduta da uno spazio vuoto. L'esempio seguente illustra questa espressione regolare.

```csharp
string pattern = @"^\s*(System.)??Console.Write(Line)??\(??";
string input = "System.Console.WriteLine(\"Hello!\")\n" + 
                      "Console.Write(\"Hello!\")\n" + 
                      "Console.WriteLine(\"Hello!\")\n" + 
                      "Console.ReadLine()\n" + 
                      "   Console.WriteLine";
foreach (Match match in Regex.Matches(input, pattern, 
                                      RegexOptions.IgnorePatternWhitespace | 
                                      RegexOptions.IgnoreCase | 
                                      RegexOptions.Multiline))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'System.Console.Write' found at position 0.
//        'Console.Write' found at position 36.
//        'Console.Write' found at position 61.
//        '   Console.Write' found at position 110.
```

```vb
Dim pattern As String = "^\s*(System.)??Console.Write(Line)??\(??"
Dim input As String = "System.Console.WriteLine(""Hello!"")" + vbCrLf + _
                      "Console.Write(""Hello!"")" + vbCrLf + _
                      "Console.WriteLine(""Hello!"")" + vbCrLf + _
                      "Console.ReadLine()" + vbCrLf + _
                      "   Console.WriteLine"
For Each match As Match In Regex.Matches(input, pattern, _
                                         RegexOptions.IgnorePatternWhitespace Or RegexOptions.IgnoreCase Or RegexOptions.MultiLine)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'System.Console.Write' found at position 0.
'       'Console.Write' found at position 36.
'       'Console.Write' found at position 61.
'       '   Console.Write' found at position 110.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | Trova la corrispondenza con l'inizio del flusso di input.
`\s*` | Trovare la corrispondenza di zero o più spazi vuoti.
`(System.)??` | Trova la corrispondenza con zero o una occorrenza della stringa "System.".
`Console.Write` | Trova la corrispondenza con la stringa "Console.Write".
`(Line)??` | Trova la corrispondenza con zero o una occorrenza della stringa "Line".
`\(??` | Trova la corrispondenza con zero o una occorrenza della parentesi di apertura.
 
### <a name="match-exactly-n-times-lazy-match-n"></a>Trova la corrispondenza esatta n volte (corrispondenza lazy): {n}?

Il quantificatore **{**_n_**}?** trova la corrispondenza con l'elemento precedente esattamente *n* volte, dove *n* è qualsiasi numero intero. Si tratta della controparte lazy del quantificatore greedy **{**_n_**}+**.

Nell'esempio seguente viene usata l'espressione regolare `\b(\w{3,}?\.){2}?\w{3,}?\b` per identificare un indirizzo di sito Web. Si noti che corrisponde a "www.microsoft.com" e "msdn.microsoft.com", ma non a "mywebsite" o "mycompany.com".

```csharp
string pattern = @"\b(\w{3,}?\.){2}?\w{3,}?\b";
string input = "www.microsoft.com msdn.microsoft.com mywebsite mycompany.com";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'www.microsoft.com' found at position 0.
//        'msdn.microsoft.com' found at position 18.
```

```vb
Dim pattern As String = "\b(\w{3,}?\.){2}?\w{3,}?\b"
 Dim input As String = "www.microsoft.com msdn.microsoft.com mywebsite mycompany.com"
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next     
' The example displays the following output:
'       'www.microsoft.com' found at position 0.
'       'msdn.microsoft.com' found at position 18.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`(\w{3,}?\.)` | Trova la corrispondenza con almeno 3 caratteri alfanumerici, ma il minor numero di caratteri possibile, seguiti da un carattere punto. Equivale al primo gruppo di acquisizione.
`(\w{3,}?\.){2}?` | Corrisponde al criterio nel primo gruppo due volte, ma il minor numero di volte possibile.
`\b` | Termina la corrispondenza sul confine di parola.
 
### <a name="match-at-least-n-times-lazy-match-n"></a>Trova la corrispondenza almeno n volte (corrispondenza lazy): {n,}?

Il quantificatore **{**_n_**,}?** trova la corrispondenza con l'elemento precedente almeno *n* volte, dove *n* è qualsiasi numero intero, ma il minor numero di volte possibile. Si tratta della controparte lazy del quantificatore greedy **{**_n_**,}**.

Vedere l'esempio per il quantificatore **{**_n_**}?** nella sezione precedente per un'illustrazione. L'espressione regolare in tale esempio usa il quantificatore **{**_n_**,}** per trovare la corrispondenza con una stringa che contenga almeno tre caratteri seguiti da un punto.

### <a name="match-between-n-and-m-times-lazy-match-nm"></a>Trova la corrispondenza tra n e m volte (corrispondenza lazy): {n,m}?

Il quantificatore **{**_n_**,**_m_**}?** trova la corrispondenza con l'elemento precedente tra *n* e *m* volte, dove *n* e *m* sono numeri interi, ma il minor numero di volte possibile. Si tratta della controparte lazy del quantificatore greedy **{**_n_**,**_m_**}**.

Nell'esempio seguente l'espressione regolare `\b[A-Z](\w*\s+){1,10}?[.!?]` corrisponde alle frasi che contengono da una a dieci parole. Trova la corrispondenza con tutte le frasi nella stringa di input, ad eccezione di una frase che contiene 18 parole.

```csharp
string pattern = @"\b[A-Z](\w*?\s*?){1,10}[.!?]";
string input = "Hi. I am writing a short note. Its purpose is " + 
                      "to test a regular expression that attempts to find " + 
                      "sentences with ten or fewer words. Most sentences " + 
                      "in this note are short.";
foreach (Match match in Regex.Matches(input, pattern))
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index);

//  The example displays the following output:
//        'Hi.' found at position 0.
//        'I am writing a short note.' found at position 4.
//        'Most sentences in this note are short.' found at position 132.
```

```vb
Dim pattern As String = "\b[A-Z](\w*\s?){1,10}?[.!?]"
Dim input As String = "Hi. I am writing a short note. Its purpose is " + _
                      "to test a regular expression that attempts to find " + _
                      "sentences with ten or fewer words. Most sentences " + _
                      "in this note are short."
For Each match As Match In Regex.Matches(input, pattern)
   Console.WriteLine("'{0}' found at position {1}.", match.Value, match.Index)
Next 
' The example displays the following output:
'       'Hi.' found at position 0.
'       'I am writing a short note.' found at position 4.
'       'Most sentences in this note are short.' found at position 132.
```

Il criterio di ricerca di espressioni regolari è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | -----------
`\b` | Inizia dal confine di una parola.
`[A-Z]` | Trova la corrispondenza con un carattere maiuscolo da A a Z.
`(\w*\s+)` | Trova la corrispondenza con uno o più caratteri alfanumerici seguiti da uno o più caratteri spazio vuoto. Equivale al primo gruppo di acquisizione.
`{1,10}?` | Trova la corrispondenza con il criterio precedente da 1 a 10 volte, ma il minor numero di volte possibile.
`[.!?]` | Trova la corrispondenza con uno dei caratteri di punteggiatura ".", "!" o "?".
 
## <a name="greedy-and-lazy-quantifiers"></a>Quantificatori greedy e lazy

Alcuni quantificatori hanno due versioni: 

* Una versione greedy. 

  Un quantificatore greedy tenta di trovare la corrispondenza con un elemento il maggior numero di volte possibile. 


* •Una versione non greedy (o lazy). 

 Un quantificatore non greedy tenta di trovare la corrispondenza con un elemento il minor numero di volte possibile. È possibile trasformare un quantificatore greedy in un quantificatore lazy aggiungendo semplicemente un **?**.

Si consideri un'espressione regolare semplice progettata per estrarre le ultime quattro cifre da una stringa di numeri, ad esempio un numero di carta di credito. La versione dell'espressione regolare che usa il quantificatore greedy **\*** è `\b.*([0-9]{4})\b`. Se tuttavia una stringa contiene due numeri, come illustrato nell'esempio seguente, l'espressione regolare trova la corrispondenza solo con le ultime quattro cifre secondo numero.

```csharp
string greedyPattern = @"\b.*([0-9]{4})\b";
string input1 = "1112223333 3992991999";
foreach (Match match in Regex.Matches(input1, greedyPattern))
   Console.WriteLine("Account ending in ******{0}.", match.Groups[1].Value);

// The example displays the following output:
//       Account ending in ******1999.
```

```vb
Dim greedyPattern As String = "\b.*([0-9]{4})\b"
Dim input1 As String = "1112223333 3992991999"
For Each match As Match In Regex.Matches(input1, greedypattern)
   Console.WriteLine("Account ending in ******{0}.", match.Groups(1).Value)
Next
' The example displays the following output:
'       Account ending in ******1999.
```

L'espressione regolare non è in grado di trovare il primo numero perché il quantificatore **\*** tenta di trovare la corrispondenza con l'elemento precedente il maggior numero di volte possibile nell'intera stringa, quindi trova la corrispondenza alla fine della stringa.

Questo non è il comportamento desiderato. In alternativa, è possibile usare il quantificatore lazy **\*?** per estrarre cifre da entrambi i numeri, come illustra l'esempio seguente.

```csharp
string lazyPattern = @"\b.*?([0-9]{4})\b";
string input2 = "1112223333 3992991999";
foreach (Match match in Regex.Matches(input2, lazyPattern))
   Console.WriteLine("Account ending in ******{0}.", match.Groups[1].Value);

// The example displays the following output:
//       Account ending in ******3333.
//       Account ending in ******1999.
```

```vb
Dim lazyPattern As String = "\b.*?([0-9]{4})\b"
Dim input2 As String = "1112223333 3992991999"
For Each match As Match In Regex.Matches(input2, lazypattern)
   Console.WriteLine("Account ending in ******{0}.", match.Groups(1).Value)
Next     
' The example displays the following output:
'       Account ending in ******3333.
'       Account ending in ******1999.
```

Nella maggior parte dei casi le espressioni regolari con quantificatori greedy e lazy restituiscono le stesse corrispondenze. In genere restituiscono risultati diversi quando vengono usate con il metacarattere jolly (**.**), che corrisponde a qualsiasi carattere. 

## <a name="quantifiers-and-empty-matches"></a>Quantificatori e corrispondenze vuote

I quantificatori **\***, **+** e **{**_n_**,**_m_**}** e le relative controparti lazy non si ripetono mai dopo una corrispondenza vuota quando è stato trovato il numero minimo di acquisizioni. Questa regola impedisce ai quantificatori di avviare cicli infiniti su corrispondenze di sottoespressioni vuote quando il numero massimo di acquisizioni possibili per il gruppo possibili è infinito o quasi infinito.

Ad esempio, il codice seguente presenta il risultato di una chiamata al metodo [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) con il criterio di espressione regolare `(a?)*,` che trova la corrispondenza con uno o nessun carattere "a" zero o più volte. Si noti che il singolo gruppo di acquisizione acquisisce ogni "a" nonché [String.Empty](xref:System.String.Empty), ma che non esiste una seconda corrispondenza vuota, perché la prima corrispondenza vuota induce il quantificatore a interrompere la ripetizione.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "(a?)*";
      string input = "aaabbb";
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}' at index {1}", 
                        match.Value, match.Index);
      if (match.Groups.Count > 1) {
         GroupCollection groups = match.Groups;
         for (int grpCtr = 1; grpCtr <= groups.Count - 1; grpCtr++) {
            Console.WriteLine("   Group {0}: '{1}' at index {2}", 
                              grpCtr, 
                              groups[grpCtr].Value,
                              groups[grpCtr].Index);
            int captureCtr = 0;
            foreach (Capture capture in groups[grpCtr].Captures) {
               captureCtr++;
               Console.WriteLine("      Capture {0}: '{1}' at index {2}", 
                                 captureCtr, capture.Value, capture.Index);
            }
         } 
      }   
   }
}
// The example displays the following output:
//       Match: 'aaa' at index 0
//          Group 1: '' at index 3
//             Capture 1: 'a' at index 0
//             Capture 2: 'a' at index 1
//             Capture 3: 'a' at index 2
//             Capture 4: '' at index 3
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(a?)*"
      Dim input As String = "aaabbb"
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}' at index {1}", 
                        match.Value, match.Index)
      If match.Groups.Count > 1 Then
         Dim groups As GroupCollection = match.Groups
         For grpCtr As Integer = 1 To groups.Count - 1
            Console.WriteLine("   Group {0}: '{1}' at index {2}", 
                              grpCtr, 
                              groups(grpCtr).Value,
                              groups(grpCtr).Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In groups(grpCtr).Captures
               captureCtr += 1
               Console.WriteLine("      Capture {0}: '{1}' at index {2}", 
                                 captureCtr, capture.Value, capture.Index)
            Next
         Next 
      End If   
   End Sub
End Module
' The example displays the following output:
'       Match: 'aaa' at index 0
'          Group 1: '' at index 3
'             Capture 1: 'a' at index 0
'             Capture 2: 'a' at index 1
'             Capture 3: 'a' at index 2
'             Capture 4: '' at index 3
```

Per vedere in pratica la differenza tra un gruppo di acquisizione che definisce un numero minimo e massimo di acquisizioni e uno che definisce un numero fisso di acquisizioni, considerare i criteri di espressione regolare `(a\1|(?(1)\1)){0,2}` e `(a\1|(?(1)\1)){2}`. Entrambe le espressioni regolari sono costituite da un singolo gruppo di acquisizione, definito come illustrato nella tabella seguente. 

Criterio | Descrizione
------- | -----------
`(a\1` | Trova la corrispondenza con "a" insieme al valore del primo gruppo acquisito...
`&#124;(?(1)` | … o verifica se è stato definito il primo gruppo acquisito. Si noti che il costrutto **(?(1)** non definisce un gruppo di acquisizione.
`\1))` | Se il primo gruppo acquisito esiste, trovare la corrispondenza con il relativo valore. Se non esiste, il gruppo corrisponderà a [String.Empty](xref:System.String.Empty). 
 
La prima espressione regolare tenta di trovare la corrispondenza con questo criterio da zero a due volte, la seconda esattamente due volte. Poiché il primo criterio raggiunge il numero minimo di acquisizioni con la prima acquisizione di [String.Empty](xref:System.String.Empty), non ripete mai il tentativo di trovare una corrispondenza con `a\1;` e il quantificatore `{0,2}` consente solo corrispondenze vuote nell'ultima iterazione. Al contrario, la seconda espressione regolare trova la corrispondenza con "a" perché restituisce `a\1` una seconda volta. Il numero minimo di iterazioni, 2, impone al motore la ripetizione dopo una corrispondenza vuota.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern, input;

      pattern = @"(a\1|(?(1)\1)){0,2}";
      input = "aaabbb"; 

      Console.WriteLine("Regex pattern: {0}", pattern);
      Match match = Regex.Match(input, pattern);
      Console.WriteLine("Match: '{0}' at position {1}.", 
                        match.Value, match.Index);
      if (match.Groups.Count > 1) {
         for (int groupCtr = 1; groupCtr <= match.Groups.Count - 1; groupCtr++)
         {
            Group group = match.Groups[groupCtr];         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index);
            int captureCtr = 0;
            foreach (Capture capture in group.Captures) {
               captureCtr++;
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index);
            }   
         }
      }
      Console.WriteLine();

      pattern = @"(a\1|(?(1)\1)){2}";
      Console.WriteLine("Regex pattern: {0}", pattern);
      match = Regex.Match(input, pattern);
         Console.WriteLine("Matched '{0}' at position {1}.", 
                           match.Value, match.Index);
      if (match.Groups.Count > 1) {
         for (int groupCtr = 1; groupCtr <= match.Groups.Count - 1; groupCtr++)
         {
            Group group = match.Groups[groupCtr];         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index);
            int captureCtr = 0;
            foreach (Capture capture in group.Captures) {
               captureCtr++;
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index);
            }   
         }
      }
   }
}
// The example displays the following output:
//       Regex pattern: (a\1|(?(1)\1)){0,2}
//       Match: '' at position 0.
//          Group: 1: '' at position 0.
//             Capture: 1: '' at position 0.
//       
//       Regex pattern: (a\1|(?(1)\1)){2}
//       Matched 'a' at position 0.
//          Group: 1: 'a' at position 0.
//             Capture: 1: '' at position 0.
//             Capture: 2: 'a' at position 0.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern, input As String

      pattern = "(a\1|(?(1)\1)){0,2}"
      input = "aaabbb" 

      Console.WriteLine("Regex pattern: {0}", pattern)
      Dim match As Match = Regex.Match(input, pattern)
      Console.WriteLine("Match: '{0}' at position {1}.", 
                        match.Value, match.Index)
      If match.Groups.Count > 1 Then
         For groupCtr As Integer = 1 To match.Groups.Count - 1
            Dim group As Group = match.Groups(groupCtr)         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               captureCtr += 1
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index)
            Next   
         Next
      End If
      Console.WriteLine()

      pattern = "(a\1|(?(1)\1)){2}"
      Console.WriteLine("Regex pattern: {0}", pattern)
      match = Regex.Match(input, pattern)
         Console.WriteLine("Matched '{0}' at position {1}.", 
                           match.Value, match.Index)
      If match.Groups.Count > 1 Then
         For groupCtr As Integer = 1 To match.Groups.Count - 1
            Dim group As Group = match.Groups(groupCtr)         
            Console.WriteLine("   Group: {0}: '{1}' at position {2}.", 
                              groupCtr, group.Value, group.Index)
            Dim captureCtr As Integer = 0
            For Each capture As Capture In group.Captures
               captureCtr += 1
               Console.WriteLine("      Capture: {0}: '{1}' at position {2}.", 
                                 captureCtr, capture.Value, capture.Index)
            Next   
         Next
      End If
   End Sub
End Module
' The example displays the following output:
'       Regex pattern: (a\1|(?(1)\1)){0,2}
'       Match: '' at position 0.
'          Group: 1: '' at position 0.
'             Capture: 1: '' at position 0.
'       
'       Regex pattern: (a\1|(?(1)\1)){2}
'       Matched 'a' at position 0.
'          Group: 1: 'a' at position 0.
'             Capture: 1: '' at position 0.
'             Capture: 2: 'a' at position 0.
```

## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)

[Backtracking nelle espressioni regolari](backtracking.md)


