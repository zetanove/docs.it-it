---
title: Stringhe di formato TimeSpan standard
description: Stringhe di formato TimeSpan standard
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 4e0f02f1-4abd-47b5-8995-5c3ff45b0ce1
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: a31f0da1f5b502d8b983f4d496c4b9a520b0309c

---

# <a name="standard-timespan-format-strings"></a>Stringhe di formato TimeSpan standard

Una stringa di formato [TimeSpan](xref:System.TimeSpan) standard usa un singolo identificatore di formato per definire la rappresentazione di testo di un valore [TimeSpan](xref:System.TimeSpan) che risulta da un'operazione di formattazione. Le stringhe di formato contenenti più caratteri alfabetici, inclusi gli spazi vuoti, vengono interpretate come stringhe di formato [TimeSpan](xref:System.TimeSpan) personalizzato. Per altre informazioni, vedere [Stringhe di formato TimeSpan personalizzate](custom-timespan.md).

Le rappresentazione di stringa dei valori [TimeSpan](xref:System.TimeSpan) vengono prodotte da chiamate agli overload del metodo [TimeSpan.ToString](xref:System.TimeSpan.ToString), nonché dai metodi che supportano la formattazione composita, come [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). Per altre informazioni, vedere [Formattazione di tipi](formatting-types.md) e [Formattazione composita](composite-format.md). Nell'esempio seguente viene illustrato l'uso di stringhe di formato standard nelle operazioni di formattazione

```csharp
using System;

public class Example
{
   public static void Main()
   {
      TimeSpan duration = new TimeSpan(1, 12, 23, 62);
      string output = "Time of Travel: " + duration.ToString("c");
      Console.WriteLine(output);

      Console.WriteLine("Time of Travel: {0:c}", duration); 
   }
}
// The example displays the following output:
//       Time of Travel: 1.12:24:02
//       Time of Travel: 1.12:24:02
```

```vb
Module Example
   Public Sub Main()
      Dim duration As New TimeSpan(1, 12, 23, 62)
      Dim output As String = "Time of Travel: " + duration.ToString("c")
      Console.WriteLine(output)

      Console.WriteLine("Time of Travel: {0:c}", duration) 
   End Sub
End Module
' The example displays the following output:
'       Time of Travel: 1.12:24:02
'       Time of Travel: 1.12:24:02
```

Le stringhe di formato [TimeSpan](xref:System.TimeSpan) standard sono usate anche dai metodi [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) e [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) per definire il formato richiesto delle stringhe di input per le operazioni di analisi. (l'analisi converte la rappresentazione di stringa di un valore in tale valore). Nell'esempio seguente viene illustrato l'utilizzo di stringhe di formato standard nelle operazioni di analisi.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string value = "1.03:14:56.1667";
      TimeSpan interval;
      try {
         interval = TimeSpan.ParseExact(value, "c", null);
         Console.WriteLine("Converted '{0}' to {1}", value, interval);
      }   
      catch (FormatException) {
         Console.WriteLine("{0}: Bad Format", value);
      }   
      catch (OverflowException) {
         Console.WriteLine("{0}: Out of Range", value);
      }

      if (TimeSpan.TryParseExact(value, "c", null, out interval))
         Console.WriteLine("Converted '{0}' to {1}", value, interval);
      else
         Console.WriteLine("Unable to convert {0} to a time interval.", 
                           value);
   }
}
// The example displays the following output:
//       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
//       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
```

```vb
Module Example
   Public Sub Main()
      Dim value As String = "1.03:14:56.1667"
      Dim interval As TimeSpan
      Try
         interval = TimeSpan.ParseExact(value, "c", Nothing)
         Console.WriteLine("Converted '{0}' to {1}", value, interval)
      Catch e As FormatException
         Console.WriteLine("{0}: Bad Format", value)
      Catch e As OverflowException
         Console.WriteLine("{0}: Out of Range", value)
      End Try

      If TimeSpan.TryParseExact(value, "c", Nothing, interval) Then
         Console.WriteLine("Converted '{0}' to {1}", value, interval)
      Else
         Console.WriteLine("Unable to convert {0} to a time interval.", 
                           value)
      End If                
   End Sub
End Module
' The example displays the following output:
'       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
'       Converted '1.03:14:56.1667' to 1.03:14:56.1667000
```

Nella tabella seguente sono elencati gli identificatori di formato di intervallo di tempo standard.

Identificatore di formato | Nome | Descrizione | Esempi
---------------- | ---- | ----------- | --------
"c" | Formato di costante (invariante) | Questo identificatore non è dipendente dalle impostazioni cultura. Assume il formato [-] [d'. '] hh': 'mm':'ss ['. ' fffffff]. (le stringhe di formato "t" e "T" producono gli stessi risultati). | `TimeSpan.Zero -> 00:00:00`; `New TimeSpan(0, 0, 30, 0) -> 00:30:00`; `New TimeSpan(3, 17, 25, 30, 500) -> 3.17:25:30.5000000`
"g" | Formato breve generale | Questo identificatore restituisce informazioni strettamente necessarie. È basato sulle impostazioni cultura e assume il formato [-][d':']h':'mm':'ss[.FFFFFFF]. | `New TimeSpan(1, 3, 16, 50, 500) -> 1:3:16:50.5 (en-US)`; `New TimeSpan(1, 3, 16, 50, 500) -> 1:3:16:50,5 (fr-FR)`; `New TimeSpan(1, 3, 16, 50, 599) -> 1:3:16:50.599 (en-US)`; `New TimeSpan(1, 3, 16, 50, 599) -> 1:3:16:50,599 (fr-FR)`
"G" | Formato esteso generale | Questo identificatore restituisce sempre giorni e sette cifre frazionarie. È basato sulle impostazioni cultura e assume il formato [-]d':'hh':'mm':'ss.fffffff. | `New TimeSpan(18, 30, 0) -> 0:18:30:00.0000000 (en-US)`; `New TimeSpan(18, 30, 0) -> 0:18:30:00,0000000 (fr-FR)` 

## <a name="the-constant-c-format-specifier"></a>Identificatore di formato di costante ("C").

L'identificatore di formato "c" restituisce la rappresentazione di stringa di un valore [TimeSpan](xref:System.TimeSpan) nel formato seguente:

[-][_d_.]_hh_:_mm_:_ss_[._fffffff_]

Gli elementi tra parentesi quadre ([e]) sono facoltativi. Il punto (.) e i due punti (:) sono simboli letterali. La tabella seguente descrive gli elementi rimanenti. 

Elemento | Descrizione
------- | -----------
- | Un segno negativo facoltativo, che indica un intervallo di tempo negativo.
*d* | Numero di giorni facoltativo, senza zeri iniziali.
*hh* | Numero di ore, nell'intervallo compreso tra "00" e "23".
*mm* | Numero di minuti, nell'intervallo compreso tra "00" e "59".
*ss* | Numero di secondi, nell'intervallo compreso tra "0" e "59".
*fffffff* | La parte frazionaria facoltativa di un secondo. Il valore può variare da "0000001" (un tick oppure un decimilionesimo di secondo) e "9999999" (9.999.999 decimilionesimi di secondo, o un secondo meno di un tick). 

A differenza degli identificatori di formato "g" e "G", l'identificatore di formato "c" non è dipendente dalle impostazioni cultura. Produce la rappresentazione di stringa di un valore [TimeSpan](xref:System.TimeSpan) invariabile e comune a tutte le versioni precedenti di.NET Framework prima di .NET Framework 4. "c" è la stringa di formato [TimeSpan](xref:System.TimeSpan) predefinita; il metodo [TimeSpan.ToString](xref:System.TimeSpan.ToString) formatta un valore di intervallo di tempo usando la stringa di formato "c".

> [!NOTE]
> [TimeSpan](xref:System.TimeSpan) supporta anche le stringhe di formato standard "t" e "T", che hanno un comportamento identico alla stringa di formato standard "c".

Nell'esempio seguente viene creata un'istanza di due oggetti [TimeSpan](xref:System.TimeSpan), usati per eseguire operazioni aritmetiche e viene visualizzato il risultato. In ogni caso, viene usata la formattazione composita per visualizzare il valore [TimeSpan](xref:System.TimeSpan) con l'identificatore di formato "c".

```csharp
using System;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:c} - {1:c} = {2:c}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2);

      interval1 = new TimeSpan(0, 0, 1, 14, 365);
      interval2 = TimeSpan.FromTicks(2143756);  
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       07:45:16 - 18:12:38 = -10:27:22
//       07:45:16 + 18:12:38 = 1.01:57:54
//       00:01:14.3650000 + 00:00:00.2143756 = 00:01:14.5793756
```

```vb
Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:c} - {1:c} = {2:c}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2)

      interval1 = New TimeSpan(0, 0, 1, 14, 365)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:c} + {1:c} = {2:c}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       07:45:16 - 18:12:38 = -10:27:22
'       07:45:16 + 18:12:38 = 1.01:57:54
'       00:01:14.3650000 + 00:00:00.2143756 = 00:01:14.5793756
```

## <a name="the-general-short-g-format-specifier"></a>Identificatore di formato generale ("g")

L'identificatore di formato [TimeSpan](xref:System.TimeSpan) "g" restituisce la rappresentazione di stringa di un valore [TimeSpan](xref:System.TimeSpan) in un formato compresso includendo solo gli elementi necessari. Ha il formato seguente:

[-][_d_:]_h_:_mm_:_ss_[._FFFFFFF_]

Gli elementi tra parentesi quadre ([e]) sono facoltativi. I due punti (:) sono un simbolo letterale. La tabella seguente descrive gli elementi rimanenti.

Elemento | Descrizione
------- | -----------
- | Un segno negativo facoltativo, che indica un intervallo di tempo negativo.
*d* | Numero di giorni facoltativo, senza zeri iniziali.
*hh* | Numero di ore, compreso tra "0" e "23", senza zeri iniziali. 
*mm* | Numero di minuti, nell'intervallo compreso tra "00" e "59".
*ss* | Numero di secondi, nell'intervallo compreso tra "0" e "59".
. | Il separatore dei secondi frazionari.
*FFFFFFF* | Frazioni di secondo. Viene visualizzato il minor numero di cifre possibile.

Come l'identificatore di formato "G", l'identificatore di formato "g" viene localizzato. Il separatore dei secondi frazionari è basato sulle impostazioni cultura correnti.

Nell'esempio seguente viene creata un'istanza di due oggetti [TimeSpan](xref:System.TimeSpan), usati per eseguire operazioni aritmetiche e viene visualizzato il risultato. In ogni caso, viene usata la formattazione composita per visualizzare il valore [TimeSpan](xref:System.TimeSpan) con l'identificatore di formato "g". Il valore [TimeSpan](xref:System.TimeSpan) viene anche formattato usando le convenzioni di formattazione dell'impostazione cultura corrente del sistema (ovvero, in questo caso, Inglese - Stati Uniti o en-US) e il Francese - Francia (fr-FR).

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:g} - {1:g} = {2:g}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), 
                        "{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2));

      interval1 = new TimeSpan(0, 0, 1, 14, 36);
      interval2 = TimeSpan.FromTicks(2143756);      
      Console.WriteLine("{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       7:45:16 - 18:12:38 = -10:27:22
//       7:45:16 + 18:12:38 = 1:1:57:54
//       0:01:14.036 + 0:00:00.2143756 = 0:01:14.2503756
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:g} - {1:g} = {2:g}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), 
                        "{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2))

      interval1 = New TimeSpan(0, 0, 1, 14, 36)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:g} + {1:g} = {2:g}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       7:45:16 - 18:12:38 = -10:27:22
'       7:45:16 + 18:12:38 = 1:1:57:54
'       0:01:14.036 + 0:00:00.2143756 = 0:01:14.2503756
```

## <a name="the-general-long-g-format-specifier"></a>Identificatore di formato esteso generale ("G")

L'identificatore di formato [TimeSpan](xref:System.TimeSpan) "G" restituisce la rappresentazione di stringa di un valore [TimeSpan](xref:System.TimeSpan) in un formato esteso che include sempre sia i giorni che le frazioni di secondo. La stringa risultante dall'identificatore di formato standard "G" ha il seguente formato:

[-]*d*:*hh*:*mm*:*ss*.*fffffff*

Gli elementi tra parentesi quadre ([e]) sono facoltativi. I due punti (:) sono un simbolo letterale. La tabella seguente descrive gli elementi rimanenti.

Elemento | Descrizione
------- | -----------
- | Un segno negativo facoltativo, che indica un intervallo di tempo negativo.
*d* | Numero di giorni facoltativo, senza zeri iniziali.
*hh* | Numero di ore, nell'intervallo compreso tra "0" e "23". 
*mm* | Numero di minuti, nell'intervallo compreso tra "00" e "59".
*ss* | Numero di secondi, nell'intervallo compreso tra "0" e "59".
. | Il separatore dei secondi frazionari.
*fffffff* | Frazioni di secondo.

Come l'identificatore di formato "G", l'identificatore di formato "g" viene localizzato. Il separatore dei secondi frazionari è basato sulle impostazioni cultura correnti.

Nell'esempio seguente viene creata un'istanza di due oggetti [TimeSpan](xref:System.TimeSpan), usati per eseguire operazioni aritmetiche e viene visualizzato il risultato. In ogni caso, viene usata la formattazione composita per visualizzare il valore [TimeSpan](xref:System.TimeSpan) con l'identificatore di formato "G". Il valore [TimeSpan](xref:System.TimeSpan) viene anche formattato usando le convenzioni di formattazione dell'impostazione cultura corrente del sistema (ovvero, in questo caso, Inglese - Stati Uniti o en-US) e il Francese - Francia (fr-FR). 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      TimeSpan interval1, interval2;
      interval1 = new TimeSpan(7, 45, 16);
      interval2 = new TimeSpan(18, 12, 38);

      Console.WriteLine("{0:G} - {1:G} = {2:G}", interval1, 
                        interval2, interval1 - interval2);
      Console.WriteLine(String.Format(new CultureInfo("fr-FR"), 
                        "{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2));

      interval1 = new TimeSpan(0, 0, 1, 14, 36);
      interval2 = TimeSpan.FromTicks(2143756);      
      Console.WriteLine("{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2);
   }
}
// The example displays the following output:
//       0:07:45:16.0000000 - 0:18:12:38.0000000 = -0:10:27:22.0000000
//       0:07:45:16,0000000 + 0:18:12:38,0000000 = 1:01:57:54,0000000
//       0:00:01:14.0360000 + 0:00:00:00.2143756 = 0:00:01:14.2503756
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim interval1, interval2 As TimeSpan
      interval1 = New TimeSpan(7, 45, 16)
      interval2 = New TimeSpan(18, 12, 38)

      Console.WriteLine("{0:G} - {1:G} = {2:G}", interval1, 
                        interval2, interval1 - interval2)
      Console.WriteLine(String.Format(New CultureInfo("fr-FR"), 
                        "{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2))

      interval1 = New TimeSpan(0, 0, 1, 14, 36)
      interval2 = TimeSpan.FromTicks(2143756)      
      Console.WriteLine("{0:G} + {1:G} = {2:G}", interval1, 
                        interval2, interval1 + interval2)
   End Sub
End Module
' The example displays the following output:
'       0:07:45:16.0000000 - 0:18:12:38.0000000 = -0:10:27:22.0000000
'       0:07:45:16,0000000 + 0:18:12:38,0000000 = 1:01:57:54,0000000
'       0:00:01:14.0360000 + 0:00:00:00.2143756 = 0:00:01:14.2503756
```

## <a name="see-also"></a>Vedere anche

[Formattazione di tipi](formatting-types.md)

[Formattazione composita](composite-format.md)

[Analisi di stringhe](parsing-strings.md)




<!--HONumber=Nov16_HO1-->


