---
title: Ancoraggi in espressioni regolari
description: Ancoraggi in espressioni regolari
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 96dff1be-3005-4ba5-af1b-323182a26085
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: ef2a63115f1efbe2418c348a3379fe7dd2face86

---

# <a name="anchors-in-regular-expressions"></a>Ancoraggi in espressioni regolari

Gli ancoraggi, o asserzioni atomiche di larghezza zero, specificano una posizione della stringa in cui deve verificarsi una corrispondenza. Quando si usa un ancoraggio nell'espressione di ricerca, il motore delle espressioni regolari non avanza nella stringa né utilizza caratteri, ma cerca una corrispondenza solo nella posizione specificata. Ad esempio, **^** specifica che la corrispondenza deve iniziare all'inizio di una riga o stringa. Di conseguenza, l'espressione regolare `^http:` considera la corrispondenza "http:" solo quando si verifica all'inizio di una riga. La tabella seguente contiene gli ancoraggi supportati dalle espressioni regolari in .NET. 

Ancoraggio | Descrizione
------ | ----------- 
**^** | La corrispondenza deve iniziare all'inizio della stringa o della riga.
**$** | La corrispondenza deve verificarsi alla fine della stringa o della riga oppure prima di \n alla fine della stringa o della riga.
**\A** | La corrispondenza deve verificarsi solo all'inizio della stringa (nessun supporto per più righe)
**\Z** | La corrispondenza deve verificarsi alla fine della stringa o prima di \n alla fine della stringa.
**\z** | La corrispondenza deve verificarsi solo alla fine della stringa. 
**\G** | La corrispondenza deve iniziare nella posizione in cui è terminata la corrispondenza precedente.
**\b** | La corrispondenza deve verificarsi in un confine di parola.
**\B** | La corrispondenza non deve verificarsi in un confine di parola.
 
## <a name="start-of-string-or-line-"></a>Inizio di stringa o riga: ^

L'ancoraggio **^** specifica che il criterio seguente deve iniziare in corrispondenza della posizione del primo carattere della stringa. Se si usa **^** con l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) (vedere [Opzioni di espressioni regolari](options.md)), la corrispondenza deve verificarsi all'inizio di ogni riga.

L'esempio seguente usa l'ancoraggio **^** in un'espressione regolare che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. L'esempio chiama due overload del metodo `Regex.Matches` 

* La chiamata all'overload [Matches(String, String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String)) trova solo la prima sottostringa nella stringa di input corrispondente al criterio di espressione regolare. 

* La chiamata all'overload [Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) con il parametro options impostato su [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline) trova tutte le cinque sottostringhe.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957\n" +
                     "Chicago Cubs, National League, 1903-present\n" + 
                     "Detroit Tigers, American League, 1901-present\n" + 
                     "New York Giants, National League, 1885-1957\n" +  
                     "Washington Senators, American League, 1901-1960\n";   
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      Match match;

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      

      startPos = 0
      endPos = 70
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      


'       For Each match As Match in Regex.Matches(input, pattern, RegexOptions.Multiline)
'          Console.Write("The {0} played in the {1} in", _
'                            match.Groups(1).Value, match.Groups(4).Value)
'          For Each capture As Capture In match.Groups(5).Captures
'             Console.Write(capture.Value)
'          Next
'          Console.WriteLine(".")
'       Next
   End Sub
End Module
' The example displays the following output:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
```

Il criterio di ricerca di espressioni regolari `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+` è definito nel modo illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`^` | La corrispondenza deve iniziare all'inizio della stringa di input (o all'inizio della riga se il metodo viene chiamato con l'opzione `RegexOptions.Multiline`).
`((\w+(\s?)){2,}` | Trova uno o più caratteri alfanumerici seguiti da nessuno o uno spazio esattamente due volte. Equivale al primo gruppo di acquisizione. Questa espressione definisce anche un secondo e un terzo gruppo di acquisizione: il secondo è costituito dalla parola acquisita, il terzo dagli spazi acquisiti. 
`,\s` | Trova una virgola seguita da uno spazio vuoto.
`(\w+\s\w+)` | Trova uno o più caratteri alfanumerici seguiti da uno spazio, seguito da uno o più caratteri alfanumerici. Questo è il quarto gruppo di acquisizione.
`,` | Trova la corrispondenza con una virgola.
`\s\d{4}` | Trova uno spazio seguito da quattro cifre decimali.
`(-(\d{4}`&#124;`present))?` |  Trova nessuna o una occorrenza di un trattino seguita da quattro cifre decimali o dalla stringa "present". Equivale al sesto gruppo di acquisizione. Include anche un settimo gruppo di acquisizione. 
`,?` | Trova nessuna o una occorrenza di una virgola.
`(\s\d{4}(-(\d{4}`&#124;`present))?,?)+` | Trova una o più occorrenze di: uno spazio, quattro cifre decimali, nessuna o una occorrenza di un trattino seguita da quattro cifre decimali oppure la stringa "present" e nessuna o una virgola. Equivale al quinto gruppo di acquisizione.
 
## <a name="end-of-string-or-line-"></a>Fine di stringa o riga: ^

L'ancoraggio **$** specifica che il criterio precedente deve verificarsi alla fine della stringa di input oppure prima di \n alla fine della stringa di input. 

Se si usa **$** con l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline), la corrispondenza può verificarsi anche alla fine di una riga. Notare che **$** corrisponde a **\n**, ma non a **\r\n** (combinazione di ritorno a capo e caratteri di nuova riga o CR/LF). Per trovare la combinazione di caratteri CR/LF, includere **\r?$** nel criterio di espressione regolare.

L'esempio seguente aggiunge l'ancoraggio **$** al criterio di espressione regolare usato nell'esempio della sezione "Inizio di stringa o riga". Se usato con la stringa di input originale, che include cinque righe di testo, il metodo [Regex.Matches(String, String)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String)) non è in grado di trovare una corrispondenza, perché la fine della prima riga non corrisponde al criterio **$**. Quando la stringa di input originale viene suddivisa in una matrice di stringhe, il metodo `Regex.Matches(String, String)` riesce a trovare la corrispondenza in ognuna delle cinque righe. Quando il metodo [Regex.Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) viene chiamato con il parametro *options* impostato su `RegexOptions.Multiline`, non viene trovata alcuna corrispondenza perché il criterio di espressione regolare non tiene conto dell'elemento di ritorno a capo (\u+000D). Tuttavia, quando il criterio di espressione regolare viene modificato sostituendo **$** con **\r?$**, la chiamata del metodo `Regex.Matches(String, String, RegexOptions)` con il parametro *options* impostato su `RegexOptions.Multiline` trova di nuovo cinque corrispondenze.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string cr = Environment.NewLine;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + cr +
                     "Chicago Cubs, National League, 1903-present" + cr + 
                     "Detroit Tigers, American League, 1901-present" + cr + 
                     "New York Giants, National League, 1885-1957" + cr +  
                     "Washington Senators, American League, 1901-1960" + cr;   
      Match match;

      string basePattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      string pattern = basePattern + "$";
      Console.WriteLine("Attempting to match the entire input string:");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      string[] teams = input.Split(new String[] { cr }, StringSplitOptions.RemoveEmptyEntries);
      Console.WriteLine("Attempting to match each element in a string array:");
      foreach (string team in teams)
      {
         if (team.Length > 70) continue;

         match = Regex.Match(team, pattern);
         if (match.Success)
         {
            Console.Write("The {0} played in the {1} in", 
                          match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);
            Console.WriteLine(".");
         }
      }
      Console.WriteLine();

      startPos = 0;
      endPos = 70;
      Console.WriteLine("Attempting to match each line of an input string with '$':");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }

      startPos = 0;
      endPos = 70;
      pattern = basePattern + "\r?$"; 
      Console.WriteLine(@"Attempting to match each line of an input string with '\r?$':");
      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    Attempting to match the entire input string:
//    
//    Attempting to match each element in a string array:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
//    
//    Attempting to match each line of an input string with '$':
//    
//    Attempting to match each line of an input string with '\r+$':
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
//    The Chicago Cubs played in the National League in 1903-present.
//    The Detroit Tigers played in the American League in 1901-present.
//    The New York Giants played in the National League in 1885-1957.
//    The Washington Senators played in the American League in 1901-1960.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim basePattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      Dim pattern As String = basePattern + "$"
      Console.WriteLine("Attempting to match the entire input string:")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      

      Dim teams() As String = input.Split(New String() { vbCrLf }, StringSplitOptions.RemoveEmptyEntries)
      Console.WriteLine("Attempting to match each element in a string array:")
      For Each team As String In teams
         If team.Length > 70 Then Continue For
         match = Regex.Match(team, pattern)
         If match.Success Then
            Console.Write("The {0} played in the {1} in", _
                           match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
         End If
      Next
      Console.WriteLine()

      startPos = 0
      endPos = 70
      Console.WriteLine("Attempting to match each line of an input string with '$':")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      


      startPos = 0
      endPos = 70
      pattern = basePattern + "\r?$" 
      Console.WriteLine("Attempting to match each line of an input string with '\r?$':")
      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      
   End Sub
End Module
' The example displays the following output:
'    Attempting to match the entire input string:
'    
'    Attempting to match each element in a string array:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
'    
'    Attempting to match each line of an input string with '$':
'    
'    Attempting to match each line of an input string with '\r+$':
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
'    The Chicago Cubs played in the National League in 1903-present.
'    The Detroit Tigers played in the American League in 1901-present.
'    The New York Giants played in the National League in 1885-1957.
'    The Washington Senators played in the American League in 1901-1960.
```

## <a name="start-of-string-only-a"></a>Solo inizio di stringa: \A

L'ancoraggio **\A** specifica che la corrispondenza deve verificarsi all'inizio della stringa di input. È identico all'ancoraggio **^**, ad eccezione del fatto che **\A** ignora l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline). Di conseguenza, può trovare solo l'inizio della prima riga in una stringa di input con più righe.

L'esempio seguente è simile agli esempi per gli ancoraggi **^** e **$**. Viene usato l'ancoraggio **\A** in un'espressione regolare che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. La stringa di input include cinque righe. La chiamata al metodo [Regex.Matches(String, String, RegexOptions)](xref:System.Text.RegularExpressions.Regex.Matches(System.String,System.String,System.Text.RegularExpressions.RegexOptions)) trova solo la prima sottostringa nella stringa di input corrispondente al criterio di espressione regolare. Come mostrato nell'esempio, l'opzione `Multiline` non ha alcun effetto.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      int startPos = 0, endPos = 70;
      string input = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957\n" +
                     "Chicago Cubs, National League, 1903-present\n" + 
                     "Detroit Tigers, American League, 1901-present\n" + 
                     "New York Giants, National League, 1885-1957\n" +  
                     "Washington Senators, American League, 1901-1960\n";   

      string pattern = @"\A((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+";
      Match match;

      if (input.Substring(startPos, endPos).Contains(",")) {
         match = Regex.Match(input, pattern, RegexOptions.Multiline);
         while (match.Success) {
            Console.Write("The {0} played in the {1} in", 
                              match.Groups[1].Value, match.Groups[4].Value);
            foreach (Capture capture in match.Groups[5].Captures)
               Console.Write(capture.Value);

            Console.WriteLine(".");
            startPos = match.Index + match.Length;
            endPos = startPos + 70 <= input.Length ? 70 : input.Length - startPos;
            if (! input.Substring(startPos, endPos).Contains(",")) break;
            match = match.NextMatch();
         }
         Console.WriteLine();
      }
   }
}
// The example displays the following output:
//    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim startPos As Integer = 0
      Dim endPos As Integer = 70
      Dim input As String = "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957" + vbCrLf + _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf + _
                            "Detroit Tigers, American League, 1901-present" + vbCrLf + _
                            "New York Giants, National League, 1885-1957" + vbCrLf + _
                            "Washington Senators, American League, 1901-1960" + vbCrLf  

      Dim pattern As String = "\A((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+"
      Dim match As Match

      ' Provide minimal validation in the event the input is invalid.
      If input.Substring(startPos, endPos).Contains(",") Then
         match = Regex.Match(input, pattern, RegexOptions.Multiline)
         Do While match.Success
            Console.Write("The {0} played in the {1} in", _
                              match.Groups(1).Value, match.Groups(4).Value)
            For Each capture As Capture In match.Groups(5).Captures
               Console.Write(capture.Value)
            Next
            Console.WriteLine(".")
            startPos = match.Index + match.Length 
            endPos = CInt(IIf(startPos + 70 <= input.Length, 70, input.Length - startPos))
            If Not input.Substring(startPos, endPos).Contains(",") Then Exit Do
            match = match.NextMatch()            
         Loop
         Console.WriteLine()                               
      End If      
   End Sub   
End Module
' The example displays the following output:
'    The Brooklyn Dodgers played in the National League in 1911, 1912, 1932-1957.
```

## <a name="end-of-string-or-before-ending-newline-z"></a>Fine di stringa o prima di terminare una nuova riga: \Z

L'ancoraggio **\Z** specifica che la corrispondenza deve verificarsi alla fine della stringa di input oppure prima di **\n** alla fine della stringa di input. È identico all'ancoraggio **$**, ad eccezione del fatto che **\Z** ignora l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline). Di conseguenza, in una stringa con più righe può trovare solo la fine dell'ultima riga oppure l'ultima riga prima di **\n**.

Notare che **\Z** corrisponde a **\n**, ma non a **\r\n** (combinazione di caratteri CR/LF). Per trovare la combinazione di caratteri CR/LF, includere **\r?\Z** nel criterio di espressione regolare.

L'esempio seguente usa l'ancoraggio **\Z** in un'espressione regolare simile all'esempio della sezione "Inizio di stringa o riga", che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. La sottoespressione `\r?\Z` nell'espressione regolare `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z` trova la fine di una stringa e anche una stringa che termina con **\n** o **\r\n**. Di conseguenza, ogni elemento nella matrice corrisponde al criterio di espressione regolare.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  
                          "Chicago Cubs, National League, 1903-present" + Environment.NewLine, 
                          "Detroit Tigers, American League, 1901-present" + Regex.Unescape(@"\n"), 
                          "New York Giants, National League, 1885-1957", 
                          "Washington Senators, American League, 1901-1960" + Environment.NewLine}; 
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z";

      foreach (string input in inputs)
      {
         if (input.Length > 70 || ! input.Contains(",")) continue;

         Console.WriteLine(Regex.Escape(input));
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("   Match succeeded.");
         else
            Console.WriteLine("   Match failed.");
      }   
   }
}
// The example displays the following output:
//    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
//       Match succeeded.
//    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
//       Match succeeded.
//    Detroit\ Tigers,\ American\ League,\ 1901-present\n
//       Match succeeded.
//    New\ York\ Giants,\ National\ League,\ 1885-1957
//       Match succeeded.
//    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
//       Match succeeded.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf, _
                            "Detroit Tigers, American League, 1901-present" + vbLf, _
                            "New York Giants, National League, 1885-1957", _
                            "Washington Senators, American League, 1901-1960" + vbCrLf }  
      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z"

      For Each input As String In inputs
         If input.Length > 70 Or Not input.Contains(",") Then Continue For

         Console.WriteLine(Regex.Escape(input))
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("   Match succeeded.")
         Else
            Console.WriteLine("   Match failed.")
         End If
      Next   
   End Sub
End Module
' The example displays the following output:
'    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
'       Match succeeded.
'    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
'       Match succeeded.
'    Detroit\ Tigers,\ American\ League,\ 1901-present\n
'       Match succeeded.
'    New\ York\ Giants,\ National\ League,\ 1885-1957
'       Match succeeded.
'    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
'       Match succeeded.
```

## <a name="end-of-string-only-z"></a>Solo fine di stringa: \z

L'ancoraggio **\z** specifica che la corrispondenza deve verificarsi alla fine della stringa di input. Come l'elemento language **$**, **\z** ignora l'opzione [RegexOptions.Multiline](xref:System.Text.RegularExpressions.RegexOptions.Multiline). A differenza dell'elemento language **\Z**, **\z** non trova un carattere **\n** alla fine di una stringa. Di conseguenza, può trovare solo l'ultima riga della stringa di input.

L'esempio seguente usa l'ancoraggio **\z** in un'espressione regolare che è altrimenti identica all'esempio della sezione precedente, che estrae informazioni sugli anni durante i quali sono esistite alcune squadre di baseball professionale. L'esempio prova a trovare ognuno dei cinque elementi in una matrice di stringhe con il criterio di espressione regolare `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z`. Due delle stringhe terminano con caratteri di ritorno a capo e di avanzamento riga, mentre le altre due no. Come mostrato dall'output, solo le stringhe senza carattere di ritorno a capo o avanzamento riga corrispondono al criterio. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string[] inputs = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957", 
                          "Chicago Cubs, National League, 1903-present" + Environment.NewLine,
                          "Detroit Tigers, American League, 1901-present\\r",
                          "New York Giants, National League, 1885-1957",
                          "Washington Senators, American League, 1901-1960" + Environment.NewLine };  
      string pattern = @"^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z";

      foreach (string input in inputs)
      {
         if (input.Length > 70 || ! input.Contains(",")) continue;

         Console.WriteLine(Regex.Escape(input));
         Match match = Regex.Match(input, pattern);
         if (match.Success)
            Console.WriteLine("   Match succeeded.");
         else
            Console.WriteLine("   Match failed.");
      }   
   }
}
// The example displays the following output:
//    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
//       Match succeeded.
//    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
//       Match failed.
//    Detroit\ Tigers,\ American\ League,\ 1901-present\n
//       Match failed.
//    New\ York\ Giants,\ National\ League,\ 1885-1957
//       Match succeeded.
//    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
//       Match failed.
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim inputs() As String = { "Brooklyn Dodgers, National League, 1911, 1912, 1932-1957",  _
                            "Chicago Cubs, National League, 1903-present" + vbCrLf, _
                            "Detroit Tigers, American League, 1901-present" + vbLf, _
                            "New York Giants, National League, 1885-1957", _
                            "Washington Senators, American League, 1901-1960" + vbCrLf }  
      Dim pattern As String = "^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z"

      For Each input As String In inputs
         If input.Length > 70 Or Not input.Contains(",") Then Continue For

         Console.WriteLine(Regex.Escape(input))
         Dim match As Match = Regex.Match(input, pattern)
         If match.Success Then
            Console.WriteLine("   Match succeeded.")
         Else
            Console.WriteLine("   Match failed.")
         End If
      Next   
   End Sub
End Module
' The example displays the following output:
'    Brooklyn\ Dodgers,\ National\ League,\ 1911,\ 1912,\ 1932-1957
'       Match succeeded.
'    Chicago\ Cubs,\ National\ League,\ 1903-present\r\n
'       Match failed.
'    Detroit\ Tigers,\ American\ League,\ 1901-present\n
'       Match failed.
'    New\ York\ Giants,\ National\ League,\ 1885-1957
'       Match succeeded.
'    Washington\ Senators,\ American\ League,\ 1901-1960\r\n
'       Match failed.
```

## <a name="contiguous-matches-g"></a>Corrispondenze contigue: \G

L'ancoraggio **\G** specifica che la corrispondenza deve verificarsi nel punto in cui è terminata la corrispondenza precedente. Se usato con il metodo [Regex.Matches](xref:System.Text.RegularExpressions.Regex.Matches(System.String)) o [Match.NextMatch](xref:System.Text.RegularExpressions.Match.NextMatch), questo ancoraggio garantisce che tutte le corrispondenze siano contigue. 

L'esempio seguente usa un'espressione regolare per estrarre i nomi delle specie di roditori da una stringa con valori delimitati da virgole. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "capybara,squirrel,chipmunk,porcupine,gopher," + 
                     "beaver,groundhog,hamster,guinea pig,gerbil," + 
                     "chinchilla,prairie dog,mouse,rat";
      string pattern = @"\G(\w+\s?\w*),?";
      Match match = Regex.Match(input, pattern);
      while (match.Success) 
      {
         Console.WriteLine(match.Groups[1].Value);
         match = match.NextMatch();
      } 
   }
}
// The example displays the following output:
//       capybara
//       squirrel
//       chipmunk
//       porcupine
//       gopher
//       beaver
//       groundhog
//       hamster
//       guinea pig
//       gerbil
//       chinchilla
//       prairie dog
//       mouse
//       rat
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "capybara,squirrel,chipmunk,porcupine,gopher," + _
                            "beaver,groundhog,hamster,guinea pig,gerbil," + _
                            "chinchilla,prairie dog,mouse,rat"
      Dim pattern As String = "\G(\w+\s?\w*),?"
      Dim match As Match = Regex.Match(input, pattern)
      Do While match.Success
         Console.WriteLine(match.Groups(1).Value)
         match = match.NextMatch()
      Loop 
   End Sub
End Module
' The example displays the following output:
'       capybara
'       squirrel
'       chipmunk
'       porcupine
'       gopher
'       beaver
'       groundhog
'       hamster
'       guinea pig
'       gerbil
'       chinchilla
'       prairie dog
'       mouse
'       rat
```

L'espressione regolare `\G(\w+\s?\w*),?` viene interpretata come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\G` | La corrispondenza deve iniziare nel punto in cui termina l'ultima corrispondenza.
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
`\s?` | Trova nessuno o uno spazio.
`\w*` | Trova la corrispondenza di zero o più caratteri alfanumerici.
`(\w+\s?\w*)` | Trova uno o più caratteri alfanumerici seguiti da nessuno o uno spazio, seguito da nessuno o più caratteri alfanumerici. Equivale al primo gruppo di acquisizione.
`,?` | Trova nessuna o una occorrenza di un carattere virgola letterale.
 
## <a name="word-boundary-b"></a>Confine di parola: \b

L'ancoraggio **\b** specifica che la corrispondenza deve verificarsi in un confine tra un carattere alfanumerico (elemento language **\w**) e uno non alfanumerico (elemento language **\W**). I caratteri alfanumerici sono costituiti da lettere, cifre e caratteri di sottolineatura. Un carattere non alfanumerico è qualsiasi carattere diverso da lettere, cifre e carattere di sottolineatura. Per altre informazioni, vedere [Classi di caratteri nelle espressioni regolari](classes.md). La corrispondenza può verificarsi anche in un confine di parola all'inizio o alla fine della stringa.

L'ancoraggio **\b** viene usato di frequente per garantire che una sottoespressione corrisponda a un'intera parola anziché solo all'inizio o alla fine di una parola. L'espressione regolare `\bare\w*\b` nell'esempio seguente mostra questo utilizzo. L'espressione trova qualsiasi parola che inizia con la sottostringa "are". L'output dell'esempio indica anche che **\b** trova sia l'inizio sia la fine della stringa di input. 

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "area bare arena mare";
      string pattern = @"\bare\w*\b";
      Console.WriteLine("Words that begin with 'are':");
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("'{0}' found at position {1}",
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       Words that begin with 'are':
//       'area' found at position 0
//       'arena' found at position 10
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "area bare arena mare"
      Dim pattern As String = "\bare\w*\b"
      Console.WriteLine("Words that begin with 'are':")
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       Words that begin with 'are':
'       'area' found at position 0
'       'arena' found at position 10
```

Il criterio di ricerca di espressioni regolari viene interpretato come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\b` | Inizia la corrispondenza sul confine di parola.
`are` | Trova la sottostringa "are".
`\w*` | Trova la corrispondenza di zero o più caratteri alfanumerici.
`\b` | Termina la corrispondenza sul confine di parola.
 
## <a name="non-word-boundary-b"></a>Carattere che non costituisce un confine di parola: \B

L'ancoraggio **\B** specifica che la corrispondenza non deve verificarsi in un confine di parola. Si tratta dell'effetto contrario rispetto all'ancoraggio **\b**.

L'esempio seguente usa l'ancoraggio **\B** per individuare le occorrenze della sottostringa "qu" in una parola. Il criterio di espressione regolare `\Bqu\w+` trova una sottostringa che inizia con "qu" che non si trova all'inizio di una parola e che continua fino alla fine della parola.

```csharp
using System;
using System.Text.RegularExpressions;

public class Example
{
   public static void Main()
   {
      string input = "equity queen equip acquaint quiet";
      string pattern = @"\Bqu\w+";
      foreach (Match match in Regex.Matches(input, pattern))
         Console.WriteLine("'{0}' found at position {1}", 
                           match.Value, match.Index);
   }
}
// The example displays the following output:
//       'quity' found at position 1
//       'quip' found at position 14
//       'quaint' found at position 21
```

```vb
Imports System.Text.RegularExpressions

Module Example
   Public Sub Main()
      Dim input As String = "equity queen equip acquaint quiet"
      Dim pattern As String = "\Bqu\w+"
      For Each match As Match In Regex.Matches(input, pattern)
         Console.WriteLine("'{0}' found at position {1}", _
                           match.Value, match.Index)
      Next
   End Sub
End Module
' The example displays the following output:
'       'quity' found at position 1
'       'quip' found at position 14
'       'quaint' found at position 21
```

Il criterio di ricerca di espressioni regolari viene interpretato come illustrato nella tabella seguente.

Criterio | Descrizione
------- | ----------- 
`\B` | La corrispondenza non deve iniziare nel confine di parola.
`qu` | Trova la sottostringa "qu".
`\w+` | Trova la corrispondenza di uno o più caratteri alfanumerici.
 
## <a name="see-also"></a>Vedere anche

[Linguaggio di espressioni regolari - Riferimento rapido](quick-ref.md)

[Opzioni di espressioni regolari](options.md)
 



<!--HONumber=Nov16_HO3-->


