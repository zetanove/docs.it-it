---
title: Espressioni regolari in .NET
description: Espressioni regolari in .NET
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: d1a640cf-09ca-48f7-800c-a627a6d549c9
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 1fc1edd64c330fe579f389750432665ed982976e

---

# <a name="regular-expressions-in-net"></a>Espressioni regolari in .NET

Le espressioni regolari ("regular expression") garantiscono un metodo efficace e flessibile per elaborare del testo. L'ampia notazione per la formulazione dei criteri di ricerca fornita dalle espressioni regolari consente di analizzare rapidamente grandi quantità di testo per trovare combinazioni di caratteri specifiche, per convalidare il testo verificandone la corrispondenza con un modello predefinito, ad esempio un indirizzo di posta elettronica, per estrarre, modificare, sostituire o eliminare sottostringhe di testo e per aggiungere le stringhe estratte a una raccolta per generare un rapporto. Per numerose applicazioni che gestiscono stringhe o che analizzano grandi blocchi di testo, le espressioni regolari rappresentano uno strumento indispensabile.

## <a name="how-regular-expressions-work"></a>Funzionamento delle espressioni regolari

L'elemento centrale dell'elaborazione del testo con le espressioni regolari è il motore delle espressioni regolari, rappresentato dall'oggetto [System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex) in .NET. L'elaborazione di testo tramite espressioni regolari richiede che al motore delle espressioni regolari vengano fornite almeno le due informazioni seguenti:

* Criterio di espressione regolare da identificare nel testo. 
  
  In .NET i criteri di espressione regolare vengono definiti a un linguaggio o una sintassi speciale, compatibile con le espressioni regolari Perl 5, che offre funzionalità aggiuntive come la corrispondenza da destra verso sinistra. Per altre informazioni, vedere [Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md).
  
* Testo da analizzare per il criterio di espressione regolare.

I metodi della classe [Regex](xref:System.Text.RegularExpressions.Regex) consentono di eseguire le operazioni seguenti:

* Determinare se il criterio di espressione regolare è presente nel testo di input chiamando il metodo [Regex.IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)). Per un esempio di uso del metodo [IsMatch](xref:System.Text.RegularExpressions.Regex.IsMatch(System.String)) per la convalida del testo, vedere [Procedura: Verificare che le stringhe siano in formato di posta elettronica valido](verify-format.md).

* Recuperare una o tutte le occorrenze del testo che corrisponde al criterio di espressione regolare chiamando il metodo [Regex.Match](xref:System.Text.RegularExpressions.Regex.Match(System.String)) o [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)). Il primo metodo restituisce un oggetto [System.Text.RegularExpressions.Match](xref:System.Text.RegularExpressions.Match) che visualizza informazioni sul testo corrispondente. I secondo metodo restituisce un oggetto [MatchCollection](xref:System.Text.RegularExpressions.MatchCollection) che contiene un oggetto [System.Text.RegularExpressions.Match](xref:System.Text.RegularExpressions.Match) per ogni corrispondenza trovata nel testo analizzato. 

* Sostituire il testo che corrisponde al criterio di espressione regolare chiamando il metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)). Per esempi di uso del metodo [Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) per modificare i formati di data e rimuovere i caratteri non validi da una stringa, vedere [Procedura: Rimuovere caratteri non validi da una stringa](strip-characters.md) e [Procedura: Modificare i formati di data](changing-formats.md).

Per una panoramica del modello a oggetti delle espressioni regolari, vedere [Modello a oggetti delle espressioni regolari](object-model.md).

Per altre informazioni sul linguaggio delle espressioni regolari, vedere [Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md).

## <a name="regular-expression-examples"></a>Esempi di espressioni regolari

La classe [String](xref:System.String) include alcuni metodi di ricerca e sostituzione di stringhe che è possibile usare quando si vogliono individuare stringhe letterali in una stringa più grande. Le espressioni regolari sono utili per lo più quando si vuole individuare una di diverse sottostringhe in una stringa più grande o quando si vogliono identificare dei modelli in una stringa, come illustrato negli esempi seguenti. 

### <a name="example-1-replacing-substrings"></a>Esempio 1: sostituzione di sottostringhe

Si presupponga che una lista di distribuzione contenga nomi che talvolta includono un titolo (Mr., Mrs., Miss o Ms.) oltre al nome e al cognome. Se non si vogliono includere i titoli quando si generano etichette per le buste dall'elenco, è possibile usare un'espressione regolare per rimuovere i titoli, come illustrato nell'esempio seguente.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string pattern = "(Mr\\.? |Mrs\\.? |Miss |Ms\\.? )";
      string[] names = { "Mr. Henry Hunt", "Ms. Sara Samuels", 
                         "Abraham Adams", "Ms. Nicole Norris" };
      foreach (string name in names)
         Console.WriteLine(Regex.Replace(name, pattern, String.Empty));
   }
}
// The example displays the following output:
//    Henry Hunt
//    Sara Samuels
//    Abraham Adams
//    Nicole Norris
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim pattern As String = "(Mr\.? |Mrs\.? |Miss |Ms\.? )"
      Dim names() As String = { "Mr. Henry Hunt", "Ms. Sara Samuels", _
                                "Abraham Adams", "Ms. Nicole Norris" }
      For Each name As String In names
         Console.WriteLine(Regex.Replace(name, pattern, String.Empty))
      Next                                
   End Sub
End Module
' The example displays the following output:
'    Henry Hunt
'    Sara Samuels
'    Abraham Adams
'    Nicole Norris
```

Il criterio di espressione regolare `(Mr\.? |Mrs\.? |Miss |Ms\.? )` trova una corrispondenza di tutte le occorrenze di "Mr", "Mr.", "Mrs", "Mrs.", "Miss", "Ms" o "Ms.". La chiamata al metodo [Regex.Replace](xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String)) sostituisce la stringa corrispondente con [String.Empty](xref:System.String.Empty), ovvero la rimuove dalla stringa originale.

### <a name="example-2-identifying-duplicated-words"></a>Esempio 2: identificazione di parole duplicate

La duplicazione accidentale delle parole è un errore comune commesso dagli autori. È possibile usare un'espressione regolare per identificare le parole duplicate, come illustrato nell'esempio seguente.

```csharp
using System;
using System.Text.RegularExpressions;

public class Class1
{
   public static void Main()
   {
      string pattern = @"\b(\w+?)\s\1\b";
      string input = "This this is a nice day. What about this? This tastes good. I saw a a dog.";
      foreach (Match match in Regex.Matches(input, pattern, RegexOptions.IgnoreCase))
         Console.WriteLine("{0} (duplicates '{1}') at position {2}", 
                           match.Value, match.Groups[1].Value, match.Index);
   }
}
// The example displays the following output:
//       This this (duplicates 'This)' at position 0
//       a a (duplicates 'a)' at position 66
```

```vb
Imports System.Text.RegularExpressions

Module modMain
   Public Sub Main()
      Dim pattern As String = "\b(\w+?)\s\1\b"
      Dim input As String = "This this is a nice day. What about this? This tastes good. I saw a a dog."
      For Each match As Match In Regex.Matches(input, pattern, RegexOptions.IgnoreCase)
         Console.WriteLine("{0} (duplicates '{1}') at position {2}", _
                           match.Value, match.Groups(1).Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       This this (duplicates 'This)' at position 0
'       a a (duplicates 'a)' at position 66
```

Il criterio di espressione regolare `\b(\w+?)\s\1\b` può essere interpretato nel modo seguente:

Sintassi | Significato
------ | -------
`\b` | Inizia dal confine di una parola.
`(\w+?)` | Corrisponde a uno o più caratteri alfanumerici, ma il minor numero di caratteri possibile. I caratteri insieme formano un gruppo a cui è possibile fare riferimento come `\1`.
`\s` | Trova la corrispondenza con uno spazio vuoto.
`\1` | Trova la corrispondenza della sottostringa equivalente al gruppo denominato `\1`.
`\b` | Trova la corrispondenza di un confine di parola.

Il metodo [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con le opzioni di espressioni regolari impostate su [RegexOptions.IgnoreCase](xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase). Per l'operazione di corrispondenza non viene quindi fatta distinzione tra maiuscole e minuscole e nell'esempio la sottostringa "This this" viene identificata come duplicato.

Si noti che la stringa di input include la sottostringa "this? This". Dato che tuttavia tra le due parole è presente un segno di punteggiatura, le parole non vengono identificate come duplicati.

### <a name="example-3-dynamically-building-a-culture-sensitive-regular-expression"></a>Esempio 3: compilazione dinamica di un'espressione regolare dipendente dalle impostazioni cultura

L'esempio seguente illustra le potenzialità delle espressioni regolari combinate alla flessibilità offerta dalle funzionalità di globalizzazione di .NET. Viene usato l'oggetto [NumberFormatInfo](xref:System.Globalization.NumberFormatInfo) per determinare il formato dei valori di valuta nelle impostazioni cultura correnti del sistema. Queste informazioni vengono quindi usate per costruire in modo dinamico un'espressione regolare per l'estrazione dei valori di valuta dal testo. Per ogni corrispondenza, il sottogruppo che contiene solo la stringa numerica viene estratto e convertito in un valore [Decimal](xref:System.Decimal), quindi viene calcolato un totale parziale. 

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      // Define text to be parsed.
      string input = "Office expenses on 2/13/2008:\n" + 
                     "Paper (500 sheets)                      $3.95\n" + 
                     "Pencils (box of 10)                     $1.00\n" + 
                     "Pens (box of 10)                        $4.49\n" + 
                     "Erasers                                 $2.19\n" + 
                     "Ink jet printer                        $69.95\n\n" + 
                     "Total Expenses                        $ 81.58\n"; 

      // Get current culture's NumberFormatInfo object.
      NumberFormatInfo nfi = CultureInfo.CurrentCulture.NumberFormat;
      // Assign needed property values to variables.
      string currencySymbol = nfi.CurrencySymbol;
      bool symbolPrecedesIfPositive = nfi.CurrencyPositivePattern % 2 == 0;
      string groupSeparator = nfi.CurrencyGroupSeparator;
      string decimalSeparator = nfi.CurrencyDecimalSeparator;

      // Form regular expression pattern.
      string pattern = Regex.Escape( symbolPrecedesIfPositive ? currencySymbol : "") + 
                       @"\s*[-+]?" + "([0-9]{0,3}(" + groupSeparator + "[0-9]{3})*(" + 
                       Regex.Escape(decimalSeparator) + "[0-9]+)?)" + 
                       (! symbolPrecedesIfPositive ? currencySymbol : ""); 
      Console.WriteLine( "The regular expression pattern is:");
      Console.WriteLine("   " + pattern);      

      // Get text that matches regular expression pattern.
      MatchCollection matches = Regex.Matches(input, pattern, 
                                              RegexOptions.IgnorePatternWhitespace);               
      Console.WriteLine("Found {0} matches.", matches.Count); 

      // Get numeric string, convert it to a value, and add it to List object.
      List<decimal> expenses = new List<Decimal>();

      foreach (Match match in matches)
         expenses.Add(Decimal.Parse(match.Groups[1].Value));      

      // Determine whether total is present and if present, whether it is correct.
      decimal total = 0;
      foreach (decimal value in expenses)
         total += value;

      if (total / 2 == expenses[expenses.Count - 1]) 
         Console.WriteLine("The expenses total {0:C2}.", expenses[expenses.Count - 1]);
      else
         Console.WriteLine("The expenses total {0:C2}.", total);
   }  
}
// The example displays the following output:
//       The regular expression pattern is:
//          \$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)
//       Found 6 matches.
//       The expenses total $81.58.
```

```vb
Imports System.Collections.Generic
Imports System.Globalization
Imports System.Text.RegularExpressions

Public Module Example
   Public Sub Main()
      ' Define text to be parsed.
      Dim input As String = "Office expenses on 2/13/2008:" + vbCrLf + _
                            "Paper (500 sheets)                      $3.95" + vbCrLf + _
                            "Pencils (box of 10)                     $1.00" + vbCrLf + _
                            "Pens (box of 10)                        $4.49" + vbCrLf + _
                            "Erasers                                 $2.19" + vbCrLf + _
                            "Ink jet printer                        $69.95" + vbCrLf + vbCrLf + _
                            "Total Expenses                        $ 81.58" + vbCrLf
      ' Get current culture's NumberFormatInfo object.
      Dim nfi As NumberFormatInfo = CultureInfo.CurrentCulture.NumberFormat
      ' Assign needed property values to variables.
      Dim currencySymbol As String = nfi.CurrencySymbol
      Dim symbolPrecedesIfPositive As Boolean = CBool(nfi.CurrencyPositivePattern Mod 2 = 0)
      Dim groupSeparator As String = nfi.CurrencyGroupSeparator
      Dim decimalSeparator As String = nfi.CurrencyDecimalSeparator

      ' Form regular expression pattern.
      Dim pattern As String = Regex.Escape(CStr(IIf(symbolPrecedesIfPositive, currencySymbol, ""))) + _
                              "\s*[-+]?" + "([0-9]{0,3}(" + groupSeparator + "[0-9]{3})*(" + _
                              Regex.Escape(decimalSeparator) + "[0-9]+)?)" + _
                              CStr(IIf(Not symbolPrecedesIfPositive, currencySymbol, "")) 
      Console.WriteLine("The regular expression pattern is: ")
      Console.WriteLine("   " + pattern)      

      ' Get text that matches regular expression pattern.
      Dim matches As MatchCollection = Regex.Matches(input, pattern, RegexOptions.IgnorePatternWhitespace)               
      Console.WriteLine("Found {0} matches. ", matches.Count)

      ' Get numeric string, convert it to a value, and add it to List object.
      Dim expenses As New List(Of Decimal)

      For Each match As Match In matches
         expenses.Add(Decimal.Parse(match.Groups.Item(1).Value))      
      Next

      ' Determine whether total is present and if present, whether it is correct.
      Dim total As Decimal
      For Each value As Decimal In expenses
         total += value
      Next

      If total / 2 = expenses(expenses.Count - 1) Then
         Console.WriteLine("The expenses total {0:C2}.", expenses(expenses.Count - 1))
      Else
         Console.WriteLine("The expenses total {0:C2}.", total)
      End If   
   End Sub
End Module
' The example displays the following output:
'       The regular expression pattern is:
'          \$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)
'       Found 6 matches.
'       The expenses total $81.58.
```

In un computer le cui impostazioni cultura correnti sono Inglese - Stati Uniti (en-US), l'esempio compila l'espressione regolare `\$\s*[-+]?([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)` dinamicamente. Questo criterio di espressione regolare può essere interpretato nel modo seguente:

Sintassi | Significato
------ | -------
`\$` | Cerca una singola occorrenza del simbolo di dollaro ($) nella stringa di input. La stringa del criterio di espressione regolare include una barra rovesciata per indicare che il simbolo di dollaro deve essere interpretato letteralmente e non come un ancoraggio dell'espressione regolare. Il simbolo $ da solo indica che il motore delle espressioni regolari deve cercare di iniziare la ricerca della corrispondenza alla fine di una stringa. Per verificare che il simbolo di valuta delle impostazioni cultura correnti non venga interpretato erroneamente come simbolo dell'espressione regolare, l'esempio chiama il metodo [Escape](xref:System.Text.RegularExpressions.Regex.Escape(System.String)) per usare caratteri di escape per il carattere.
`\s*` | Cerca zero o più occorrenze di uno spazio vuoto.
`[-+]?` | Cerca zero o una occorrenza di un segno positivo o negativo.
`([0-9]{0,3}(,[0-9]{3})*(\.[0-9]+)?)` | Le parentesi esterne che delimitano questa espressione la definiscono come gruppo di acquisizione o come sottoespressione. Se viene trovata una corrispondenza, è possibile recuperare informazioni relative a questa parte della stringa corrispondente dal secondo oggetto [Group](xref:System.Text.RegularExpressions.Group) nell'oggetto [GroupCollection](xref:System.Text.RegularExpressions.GroupCollection) restituito dalla proprietà [Match.Groups](xref:System.Text.RegularExpressions.Match.Groups). Il primo elemento della raccolta rappresenta la corrispondenza completa.
`[0-9]{0,3}` | Cerca da zero a tre occorrenze delle cifre decimali comprese tra 0 e 9.
`(,[0-9]{3})*` | Cerca zero o più occorrenze di un separatore di gruppi seguito da tre cifre decimali.
`\.` | Cerca una singola occorrenza del separatore decimale.
`[0-9]+` | Cerca una o più cifre decimali.
`(\.[0-9]+)?` | Cerca zero o una occorrenza del separatore decimale seguito da almeno una cifra decimale.

## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | -----------
[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md) | Fornisce informazioni sul set di caratteri, di operatori e di costrutti che è possibile usare per definire le espressioni regolari.
[Modello a oggetti delle espressioni regolari](object-model.md) | Fornisce esempi di codice e informazioni che illustrano l'uso delle classi di espressioni regolari.
[Dettagli sul comportamento delle espressioni regolari](regex-behavior.md) | Offre informazioni sulle funzionalità e il funzionamento delle espressioni regolari di .NET.
[Esempi di espressioni regolari](regex-examples.md) | Fornisce esempi di codice che illustrano gli usi tipici delle espressioni regolari.


## <a name="reference"></a>Riferimento

[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[System.Text.RegularExpressions.Regex](xref:System.Text.RegularExpressions.Regex)




<!--HONumber=Nov16_HO3-->


