---
title: Stringhe in formato TimeSpan personalizzato
description: Stringhe in formato TimeSpan personalizzato
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e79745eb-6ebd-4e62-85c4-4f2830c27285
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 168bd497891ead884413fad4542943a24de7a7f4

---

# <a name="custom-timespan-format-strings"></a>Stringhe in formato TimeSpan personalizzato

Una stringa di formato [TimeSpan](xref:System.TimeSpan) definisce la rappresentazione di stringa di un valore [TimeSpan](xref:System.TimeSpan) risultante da un'operazione di formattazione. Una stringa di formato personalizzato è costituita da uno o più identificatori di formato [TimeSpan](xref:System.TimeSpan) personalizzato con un numero qualsiasi di caratteri di tipo letterale. Qualsiasi stringa di un formato diverso da [TimeSpan standard](standard-timespan.md) viene interpretata come stringa di formato [TimeSpan](xref:System.TimeSpan) personalizzato.

> [!IMPORTANT]
> Gli identificatori del formato [TimeSpan](xref:System.TimeSpan) personalizzato non includono i simboli separatori dei segnaposto, ad esempio i simboli che separano i giorni dalle ore, le ore dai minuti o i secondi dalle frazioni di secondo. Questi simboli devono essere inclusi nella stringa di formato personalizzato come valori letterali stringa. Ad esempio, in `"dd\.hh\:mm"` il punto (.) è definito come separatore tra giorni e ore e i due punti (:) come separatore tra ore e minuti. 

> Negli identificatori di formato [TimeSpan](xref:System.TimeSpan) personalizzato, poi, non è incluso il simbolo segno, che consente di distinguere tra intervalli di tempo negativi e positivi. Per includere un simbolo di segno, è necessario creare una stringa di formato tramite la logica condizionale. Nella sezione [Altri caratteri](#other-characters) è incluso un esempio. 

Le rappresentazioni di stringa dei valori [TimeSpan](xref:System.TimeSpan) vengono prodotte da chiamate agli overload del metodo [TimeSpan](xref:System.TimeSpan) `ToString`, nonché dai metodi che supportano la formattazione composita, come [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)). Per altre informazioni, vedere [Formattazione di tipi](formatting-types.md) e [Formattazione composita](composite-format.md). Nell'esempio seguente viene illustrato l'utilizzo di stringhe di formato standard nelle operazioni di formattazione.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      TimeSpan duration = new TimeSpan(1, 12, 23, 62);

      string output = null;
      output = "Time of Travel: " + duration.ToString("%d") + " days";
      Console.WriteLine(output);
      output = "Time of Travel: " + duration.ToString(xref:"dd\.hh\:mm\:ss"); 
      Console.WriteLine(output);

      Console.WriteLine("Time of Travel: {0:%d} day(s)", duration);
      Console.WriteLine("Time of Travel: {0:dd\\.hh\\:mm\\:ss} days", duration);
   }
}
// The example displays the following output:
//       Time of Travel: 1 days
//       Time of Travel: 01.12:24:02
//       Time of Travel: 1 day(s)
//       Time of Travel: 01.12:24:02 days
```

```vb
Module Example
   Public Sub Main()
      Dim duration As New TimeSpan(1, 12, 23, 62)

      Dim output As String = Nothing
      output = "Time of Travel: " + duration.ToString("%d") + " days"
      Console.WriteLine(output)
      output = "Time of Travel: " + duration.ToString("dd\.hh\:mm\:ss") 
      Console.WriteLine(output)

      Console.WriteLine("Time of Travel: {0:%d} day(s)", duration)
      Console.WriteLine("Time of Travel: {0:dd\.hh\:mm\:ss} days", duration)
   End Sub
End Module
' The example displays the following output:
'       Time of Travel: 1 days
'       Time of Travel: 01.12:24:02
'       Time of Travel: 1 day(s)
'       Time of Travel: 01.12:24:02 days
```

Le stringhe di formato [TimeSpan](xref:System.TimeSpan) personalizzato sono usate anche dai metodi [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) e [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) per definire il formato richiesto delle stringhe di input per le operazioni di analisi. (l'analisi converte la rappresentazione di stringa di un valore in tale valore). Nell'esempio seguente viene illustrato l'utilizzo di stringhe di formato standard nelle operazioni di analisi.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      string value = null;
      TimeSpan interval;

      value = "6";
      if (TimeSpan.TryParseExact(value, "%d", null, out interval))
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"));
      else
         Console.WriteLine("Unable to parse '{0}'", value);

      value = "16:32.05";
      if (TimeSpan.TryParseExact(value, @"mm\:ss\.ff", null, out interval))
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"));
      else
         Console.WriteLine("Unable to parse '{0}'", value);

      value= "12.035";
      if (TimeSpan.TryParseExact(value, "ss\\.fff", null, out interval))
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"));
      else
         Console.WriteLine("Unable to parse '{0}'", value);
   }
}
// The example displays the following output:
//       6 --> 6.00:00:00
//       16:32.05 --> 00:16:32.0500000
//       12.035 --> 00:00:12.0350000
```

```vb
Module Example
   Public Sub Main()
      Dim value As String = Nothing
      Dim interval As TimeSpan

      value = "6"
      If TimeSpan.TryParseExact(value, "%d", Nothing, interval) Then
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"))
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If

      value = "16:32.05"
      If TimeSpan.TryParseExact(value, "mm\:ss\.ff", Nothing, interval) Then
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"))
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If

      value= "12.035"
      If TimeSpan.TryParseExact(value, "ss\.fff", Nothing, interval) Then
         Console.WriteLine("{0} --> {1}", value, interval.ToString("c"))
      Else
         Console.WriteLine("Unable to parse '{0}'", value)
      End If
   End Sub
End Module
' The example displays the following output:
'       6 --> 6.00:00:00
'       16:32.05 --> 00:16:32.0500000
'       12.035 --> 00:00:12.0350000
```

Nella tabella seguente vengono descritti gli identificatori di formato di data e ora personalizzati.

Identificatore di formato | Descrizione | Esempi
---------------- | ----------- | --------
"d", "%d" | Il numero di giorni completi nell'intervallo di tempo. | `new TimeSpan(6, 14, 32, 17, 685):` `%d --> "6"`;  `d\.hh\:mm --> "6.14:32"`
"dd", "dddddddd" | Il numero di giorni completi nell'intervallo di tempo, con il numero di zeri necessari all'inizio. | `new TimeSpan(6, 14, 32, 17, 685):` `ddd --> "006"`; `dd\.hh\:mm --> "06.14:32"`
"h", "%h" | Il numero di ore complete nell'intervallo di tempo non conteggiate come parti di giorni. Le ore a una sola cifra non hanno uno zero iniziale. | `new TimeSpan(6, 14, 32, 17, 685):` `%h --> "14"`; `hh\:mm --> "14:32"`
"hh" | Il numero di ore complete nell'intervallo di tempo non conteggiate come parti di giorni. Le ore a una sola cifra hanno uno zero iniziale. | `new TimeSpan(6, 14, 32, 17, 685):` `hh --> "14"`  `new TimeSpan(6, 8, 32, 17, 685):` `hh --> 08`
"m", "%m" | Il numero di minuti completi nell'intervallo di tempo non conteggiati come parti di ore o di giorni. I minuti a una sola cifra non hanno uno zero iniziale. | `new TimeSpan(6, 14, 8, 17, 685):` `%m --> "8"`; `h\:m --> "14:8"`
"mm" | Il numero di minuti completi nell'intervallo di tempo non conteggiati come parti di ore o di giorni. I minuti a una sola cifra hanno uno zero iniziale. | `new TimeSpan(6, 14, 8, 17, 685):` `mm --> "08"` `new TimeSpan(6, 8, 5, 17, 685):` `d\.hh\:mm\:ss --> 6.08:05:17`
"s", "%s" | Il numero di secondi completi nell'intervallo di tempo non conteggiati come parti di minuti, ore o giorni. I secondi a una sola cifra non hanno uno zero iniziale. | `TimeSpan.FromSeconds(12.965):` `%s --> 12`; `s\.fff --> 12.965`
"ss" | Il numero di secondi completi nell'intervallo di tempo non conteggiati come parti di minuti, ore o giorni. I secondi a una sola cifra hanno uno zero iniziale. | `TimeSpan.FromSeconds(6.965):` `ss --> 06`; `ss\.fff --> 06.965`
"f", "%f" | I decimi di secondo in un intervallo di tempo. | `TimeSpan.FromSeconds(6.895):` `f --> 8`; `ss\.f --> 06.8`
"ff" | I centesimi di secondo in un intervallo di tempo. | `TimeSpan.FromSeconds(6.895):` `ff --> 89`; `ss\.ff --> 06.89`
"fff" | I millisecondi in un intervallo di tempo. | `TimeSpan.FromSeconds(6.895):` `fff --> 895`; `ss\.fff --> 06.895`
"ffff" | I decimillesimi di secondo in un intervallo di tempo. | `TimeSpan.Parse("0:0:6.8954321"):` `ffff --> 8954`; `ss\.ffff --> 06.8954`
"fffff" | I centesimi di millesimo di secondo in un intervallo di tempo. | `TimeSpan.Parse("0:0:6.8954321"):` `ffff --> 89543`; `ss\.ffff --> 06.89543`
"ffffff" | I milionesimi di secondo in un intervallo di tempo. | `TimeSpan.Parse("0:0:6.8954321"):` `ffff --> 895432`; `ss\.ffff --> 06.895432`
"fffffff" | I decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo. | `TimeSpan.Parse("0:0:6.8954321"):` `ffff --> 8954321`; `ss\.ffff --> 06.8954321`
"F", "%F" | I decimi di secondo in un intervallo di tempo. Se la cifra è zero, non viene prodotta alcuna visualizzazione. | `TimeSpan.Parse("00:00:06.32"):` `%F: 3`  `TimeSpan.Parse("0:0:3.091"):` `ss\.F: 03.`
"FF" | I centesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari o doppi zeri non sono inclusi. |  `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 32`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.1`
"FFF" | I millisecondi in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi. |  `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 329`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.1`
"FFFF" | I decimillesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi. |  `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 3291`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.1`
"FFFFF" | I centesimi di millesimo di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono inclusi. | `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 32917`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.1`
"FFFFFF" | I milionesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari non sono visualizzati. | `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 329179`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.1`
"FFFFFFF" | I decimilionesimi di secondo in un intervallo di tempo. Eventuali zeri finali frazionari o gruppi di sette zeri non sono visualizzati. | `TimeSpan.Parse("00:00:06.3291791"):` `FFFFFF: 3291791`  `TimeSpan.Parse("0:0:3.1900000"):` `ss\.FFFFFF: 03.19`
'stringa' | Delimitatore di stringa letterale | `new TimeSpan(14, 32, 17):` `hh':'mm':'ss --> "14:32:17"`
\ | Carattere di escape. | `new TimeSpan(14, 32, 17):` `hh\:mm\:ss --> "14:32:17"`
Qualsiasi altro carattere | Qualsiasi altro carattere senza escape viene interpretato come identificatore di formato personalizzato. | `new TimeSpan(14, 32, 17):` `hh\:mm\:ss --> "14:32:17"`

## <a name="the-d-custom-format-specifier"></a>Identificatore di formato personalizzato "d"

L'identificatore di formato personalizzato "d" restituisce il valore della proprietà [TimeSpan.Days](xref:System.TimeSpan.Days), che rappresenta il numero di giorni completi nell'intervallo di tempo. Restituisce il numero completo di giorni di un valore [TimeSpan](xref:System.TimeSpan), anche se il valore ha più di una cifra. Se il valore della proprietà [TimeSpan.Days](xref:System.TimeSpan.Days) è zero, l'identificatore restituisce "0".

Se l'identificatore di formato personalizzato "d" viene usato da solo, specificare "%d" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.

```csharp
TimeSpan ts1 = new TimeSpan(16, 4, 3, 17, 250);
Console.WriteLine(ts1.ToString("%d"));
// Displays 16
```

```vb
Dim ts As New TimeSpan(16, 4, 3, 17, 250)
Console.WriteLine(ts.ToString("%d"))
' Displays 16 
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "d".

```csharp
TimeSpan ts2 = new TimeSpan(4, 3, 17);
Console.WriteLine(ts2.ToString(xref:"d\.hh\:mm\:ss"));

TimeSpan ts3 = new TimeSpan(3, 4, 3, 17);
Console.WriteLine(ts3.ToString(xref:"d\.hh\:mm\:ss"));
// The example displays the following output:
//       0.04:03:17
//       3.04:03:17
```

```vb
Dim ts2 As New TimeSpan(4, 3, 17)
Console.WriteLine(ts2.ToString("d\.hh\:mm\:ss"))

Dim ts3 As New TimeSpan(3, 4, 3, 17)
Console.WriteLine(ts3.ToString("d\.hh\:mm\:ss"))
' The example displays the following output:
'       0.04:03:17
'       3.04:03:17
```

## <a name="the-dddddddddd-custom-format-specifiers"></a>Identificatori di formato personalizzato "dd"-"dddddddd"

Gli identificatori di formato personalizzato "dd", "ddd", "dddd", "ddddd", "dddddd", "ddddddd" e "dddddddd" restituiscono il valore della proprietà [TimeSpan.Days](xref:System.TimeSpan.Days), che rappresenta il numero di giorni completi nell'intervallo di tempo. 

La stringa di output include un numero minimo di cifre specificato dal numero di caratteri "d" nell'identificatore di formato e il numero necessario di zeri iniziali. Se le cifre del numero di giorni superano il numero di caratteri "d"nell'identificatore di formato, l'output nella stringa risultato corrisponde al numero completo di giorni.

L'esempio seguente usa gli identificatori di formato per visualizzare la rappresentazione stringa di due valori [TimeSpan](xref:System.TimeSpan). Il valore del componente giorni del primo intervallo di tempo è zero, mentre il valore del componente dei giorni del secondo è 365.

```csharp
TimeSpan ts1 = new TimeSpan(0, 23, 17, 47);
TimeSpan ts2 = new TimeSpan(365, 21, 19, 45);

for (int ctr = 2; ctr <= 8; ctr++)
{
   string fmt = new String('d', ctr) + @"\.hh\:mm\:ss";
   Console.WriteLine("{0} --> {1:" + fmt + "}", fmt, ts1);  
   Console.WriteLine("{0} --> {1:" + fmt + "}", fmt, ts2);
   Console.WriteLine();
}  
// The example displays the following output:
//       dd\.hh\:mm\:ss --> 00.23:17:47
//       dd\.hh\:mm\:ss --> 365.21:19:45
//       
//       ddd\.hh\:mm\:ss --> 000.23:17:47
//       ddd\.hh\:mm\:ss --> 365.21:19:45
//       
//       dddd\.hh\:mm\:ss --> 0000.23:17:47
//       dddd\.hh\:mm\:ss --> 0365.21:19:45
//       
//       ddddd\.hh\:mm\:ss --> 00000.23:17:47
//       ddddd\.hh\:mm\:ss --> 00365.21:19:45
//       
//       dddddd\.hh\:mm\:ss --> 000000.23:17:47
//       dddddd\.hh\:mm\:ss --> 000365.21:19:45
//       
//       ddddddd\.hh\:mm\:ss --> 0000000.23:17:47
//       ddddddd\.hh\:mm\:ss --> 0000365.21:19:45
//       
//       dddddddd\.hh\:mm\:ss --> 00000000.23:17:47
//       dddddddd\.hh\:mm\:ss --> 00000365.21:19:45
```

```vb
Dim ts1 As New TimeSpan(0, 23, 17, 47)
Dim ts2 As New TimeSpan(365, 21, 19, 45)

For ctr As Integer = 2 To 8
   Dim fmt As String = New String("d"c, ctr) + "\.hh\:mm\:ss"
   Console.WriteLine("{0} --> {1:" + fmt + "}", fmt, ts1) 
   Console.WriteLine("{0} --> {1:" + fmt + "}", fmt, ts2)
   Console.WriteLine()
Next  
' The example displays the following output:
'       dd\.hh\:mm\:ss --> 00.23:17:47
'       dd\.hh\:mm\:ss --> 365.21:19:45
'       
'       ddd\.hh\:mm\:ss --> 000.23:17:47
'       ddd\.hh\:mm\:ss --> 365.21:19:45
'       
'       dddd\.hh\:mm\:ss --> 0000.23:17:47
'       dddd\.hh\:mm\:ss --> 0365.21:19:45
'       
'       ddddd\.hh\:mm\:ss --> 00000.23:17:47
'       ddddd\.hh\:mm\:ss --> 00365.21:19:45
'       
'       dddddd\.hh\:mm\:ss --> 000000.23:17:47
'       dddddd\.hh\:mm\:ss --> 000365.21:19:45
'       
'       ddddddd\.hh\:mm\:ss --> 0000000.23:17:47
'       ddddddd\.hh\:mm\:ss --> 0000365.21:19:45
'       
'       dddddddd\.hh\:mm\:ss --> 00000000.23:17:47
'       dddddddd\.hh\:mm\:ss --> 00000365.21:19:45
```

## <a name="the-h-custom-format-specifier"></a>Identificatore di formato personalizzato "h"

L'identificatore di formato personalizzato "h" restituisce il valore della proprietà [TimeSpan.Hours](xref:System.TimeSpan.Hours), che rappresenta il numero di ore complete nell'intervallo di tempo non conteggiate come parte del relativo componente giorno. Restituisce un valore stringa a una cifra se il valore della proprietà [TimeSpan.Hours](xref:System.TimeSpan.Hours) va da 0 a 9 e restituisce un valore stringa a due cifre se il valore della proprietà [TimeSpan.Hours](xref:System.TimeSpan.Hours) varia da 10 a 23.

Se l'identificatore di formato personalizzato "h" viene usato da solo, specificare "%h" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.

```csharp
TimeSpan ts = new TimeSpan(3, 42, 0);
Console.WriteLine("{0:%h} hours {0:%m} minutes", ts);
// The example displays the following output:
//       3 hours 42 minutes
```

```vb
Dim ts As New TimeSpan(3, 42, 0)
Console.WriteLine("{0:%h} hours {0:%m} minutes", ts)
' The example displays the following output:
'       3 hours 42 minutes
```

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%h" per interpretare la stringa numerica come numero di ore. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string value = "8";
TimeSpan interval;
if (TimeSpan.TryParseExact(value, "%h", null, out interval))
   Console.WriteLine(interval.ToString("c"));
else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value);   
// The example displays the following output:
//       08:00:00
```

```vb
Dim value As String = "8"
Dim interval As TimeSpan
If TimeSpan.TryParseExact(value, "%h", Nothing, interval) Then
   Console.WriteLine(interval.ToString("c"))
Else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value)   
End If   
' The example displays the following output:
'       08:00:00
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "h".

```csharp
TimeSpan ts1 = new TimeSpan(14, 3, 17);
Console.WriteLine(ts1.ToString(xref:"d\.h\:mm\:ss"));

TimeSpan ts2 = new TimeSpan(3, 4, 3, 17);
Console.WriteLine(ts2.ToString(xref:"d\.h\:mm\:ss"));
// The example displays the following output:
//       0.14:03:17
//       3.4:03:17
```

```vb
Dim ts1 As New TimeSpan(14, 3, 17)
Console.WriteLine(ts1.ToString("d\.h\:mm\:ss"))

Dim ts2 As New TimeSpan(3, 4, 3, 17)
Console.WriteLine(ts2.ToString("d\.h\:mm\:ss"))
' The example displays the following output:
'       0.14:03:17
'       3.4:03:17
```

## <a name="the-hh-custom-format-specifier"></a>Identificatore di formato personalizzato "hh"

L'identificatore di formato personalizzato "hh" restituisce il valore della proprietà [TimeSpan.Hours](xref:System.TimeSpan.Hours), che rappresenta il numero di ore complete nell'intervallo di tempo non conteggiate come parte del relativo componente giorno. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale. 

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "hh" per interpretare la stringa numerica come numero di ore. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string value = "08";
TimeSpan interval;
if (TimeSpan.TryParseExact(value, "hh", null, out interval))
   Console.WriteLine(interval.ToString("c"));
else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value);   
// The example displays the following output:
//       08:00:00 
```

```vb
Dim value As String = "08"
Dim interval As TimeSpan
If TimeSpan.TryParseExact(value, "hh", Nothing, interval) Then
   Console.WriteLine(interval.ToString("c"))
Else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value)   
End If   
' The example displays the following output:
'       08:00:00
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "hh".

```csharp
TimeSpan ts1 = new TimeSpan(14, 3, 17);
Console.WriteLine(ts1.ToString(xref:"d\.hh\:mm\:ss"));

TimeSpan ts2 = new TimeSpan(3, 4, 3, 17);
Console.WriteLine(ts2.ToString(xref:"d\.hh\:mm\:ss"));
// The example displays the following output:
//       0.14:03:17
//       3.04:03:17
```

```vb
Dim ts1 As New TimeSpan(14, 3, 17)
Console.WriteLine(ts1.ToString("d\.hh\:mm\:ss"))

Dim ts2 As New TimeSpan(3, 4, 3, 17)
Console.WriteLine(ts2.ToString("d\.hh\:mm\:ss"))
' The example displays the following output:
'       0.14:03:17
'       3.04:03:17
```

## <a name="the-m-custom-format-specifier"></a>Identificatore di formato personalizzato "m"

L'identificatore di formato personalizzato "m" restituisce il valore della proprietà [TimeSpan.Minutes](xref:System.TimeSpan.Minutes), che rappresenta il numero di minuti completi nell'intervallo di tempo non conteggiati come parte del relativo componente giorno. Restituisce un valore stringa a una cifra se il valore della proprietà [TimeSpan.Minutes](xref:System.TimeSpan.Minutes) va da 0 a 9 e restituisce un valore stringa a due cifre se il valore della proprietà [TimeSpan.Minutes](xref:System.TimeSpan.Minutes) varia da 10 a 59.

Se l'identificatore di formato personalizzato "m" viene usato da solo, specificare "%m" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.

```csharp
TimeSpan ts = new TimeSpan(3, 42, 0);
Console.WriteLine("{0:%h} hours {0:%m} minutes", ts);
// The example displays the following output:
//       3 hours 42 minutes
```

```vb
Dim ts As New TimeSpan(3, 42, 0)
Console.WriteLine("{0:%h} hours {0:%m} minutes", ts)
' The example displays the following output:
'       3 hours 42 minutes
```

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%m" per interpretare la stringa numerica come numero di minuti. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string value = "3";
TimeSpan interval;
if (TimeSpan.TryParseExact(value, "%m", null, out interval))
   Console.WriteLine(interval.ToString("c"));
else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value);   
// The example displays the following output:
//       00:03:00
```

```vb
Dim value As String = "3"
Dim interval As TimeSpan
If TimeSpan.TryParseExact(value, "%m", Nothing, interval) Then
   Console.WriteLine(interval.ToString("c"))
Else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value)   
End If   
' The example displays the following output:
'       00:03:00                              
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "m".

```csharp
TimeSpan ts1 = new TimeSpan(0, 6, 32);
Console.WriteLine("{0:m\\:ss} minutes", ts1);

TimeSpan ts2 = new TimeSpan(3, 4, 3, 17);
Console.WriteLine("Elapsed time: {0:m\\:ss}", ts2);
// The example displays the following output:
//       6:32 minutes
//       Elapsed time: 18:44
```

```vb
Dim ts1 As New TimeSpan(0, 6, 32)
Console.WriteLine("{0:m\:ss} minutes", ts1)

Dim ts2 As New TimeSpan(0, 18, 44)
Console.WriteLine("Elapsed time: {0:m\:ss}", ts2)
' The example displays the following output:
'       6:32 minutes
'       Elapsed time: 18:44
```

## <a name="the-mm-custom-format-specifier"></a>Identificatore di formato personalizzato "mm"

L'identificatore di formato personalizzato "mm" restituisce il valore della proprietà [TimeSpan.Minutes](xref:System.TimeSpan.Minutes), che rappresenta il numero di minuti completi nell'intervallo di tempo non inclusi come parte del relativo componente ore o giorni. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale. 

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "mm" per interpretare la stringa numerica come numero di minuti. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string value = "07";
TimeSpan interval;
if (TimeSpan.TryParseExact(value, "mm", null, out interval))
   Console.WriteLine(interval.ToString("c"));
else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value);   
// The example displays the following output:
//       00:07:00
```

```vb
Dim value As String = "05"
Dim interval As TimeSpan
If TimeSpan.TryParseExact(value, "mm", Nothing, interval) Then
   Console.WriteLine(interval.ToString("c"))
Else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value)   
End If   
' The example displays the following output:
'       00:05:00
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "mm".

```csharp
TimeSpan departTime = new TimeSpan(11, 12, 00);
TimeSpan arriveTime = new TimeSpan(16, 28, 00);
Console.WriteLine("Travel time: {0:hh\\:mm}", 
                  arriveTime - departTime);
// The example displays the following output:
//       Travel time: 05:16
```

```vb
Dim departTime As New TimeSpan(11, 12, 00)
Dim arriveTime As New TimeSpan(16, 28, 00)
Console.WriteLine("Travel time: {0:hh\:mm}", 
                  arriveTime - departTime)
' The example displays the following output:
'       Travel time: 05:16
```

## <a name="the-s-custom-format-specifier"></a>Identificatore di formato personalizzato "s"

L'identificatore di formato personalizzato "s" restituisce il valore della proprietà [TimeSpan.Seconds](xref:System.TimeSpan.Seconds), che rappresenta il numero di secondi completi nell'intervallo di tempo non inclusi come parte del relativo componente ore, giorni o minuti. Restituisce un valore stringa a una cifra se il valore della proprietà [TimeSpan.Seconds](xref:System.TimeSpan.Seconds) va da 0 a 9 e restituisce un valore stringa a due cifre se il valore della proprietà [TimeSpan.Seconds](xref:System.TimeSpan.Seconds) varia da 10 a 59. 

Se l'identificatore di formato personalizzato "s" viene usato da solo, specificare "%s" in modo che non venga interpretato erroneamente come stringa in formato standard. Nell'esempio seguente viene illustrato questo concetto.

```csharp
TimeSpan ts = TimeSpan.FromSeconds(12.465);
Console.WriteLine(ts.ToString("%s"));
// The example displays the following output:
//       12
```

```vb
Dim ts As TimeSpan = TimeSpan.FromSeconds(12.465)
Console.WriteLine(ts.ToString("%s"))
' The example displays the following output:
'       12
```

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "%s" per interpretare la stringa numerica come numero di secondi. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string value = "9";
TimeSpan interval;
if (TimeSpan.TryParseExact(value, "%s", null, out interval))
   Console.WriteLine(interval.ToString("c"));
else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value);   
// The example displays the following output:
//       00:00:09
```

```vb
Dim value As String = "9"
Dim interval As TimeSpan
If TimeSpan.TryParseExact(value, "%s", Nothing, interval) Then
   Console.WriteLine(interval.ToString("c"))
Else
   Console.WriteLine("Unable to convert '{0}' to a time interval", 
                     value)   
End If   
' The example displays the following output:
'       00:00:09
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "s".

```csharp
TimeSpan startTime = new TimeSpan(0, 12, 30, 15, 0);
TimeSpan endTime = new TimeSpan(0, 12, 30, 21, 3);
Console.WriteLine(xref:"Elapsed Time: {0:s\:fff} seconds", 
                  endTime - startTime);
// The example displays the following output:
//       Elapsed Time: 6:003 seconds      
```

```vb
Dim startTime As New TimeSpan(0, 12, 30, 15, 0)
Dim endTime As New TimeSpan(0, 12, 30, 21, 3)
Console.WriteLine("Elapsed Time: {0:s\:fff} seconds", 
                  endTime - startTime)
' The example displays the following output:
'       Elapsed Time: 6:003 seconds
```

## <a name="the-ss-custom-format-specifier"></a>Identificatore di formato personalizzato "ss"

L'identificatore di formato personalizzato "ss" restituisce il valore della proprietà [TimeSpan.Seconds](xref:System.TimeSpan.Seconds), che rappresenta il numero di secondi completi nell'intervallo di tempo non inclusi come parte del relativo componente ore, giorni o minuti. Per valori compresi tra 0 e 9, la stringa di output include uno zero iniziale. 

Normalmente in un'operazione di analisi una stringa di input che include solo un numero singolo viene interpretata come numero di giorni. Usare invece l'identificatore di formato personalizzato "ss" per interpretare la stringa numerica come numero di secondi. Nell'esempio seguente viene illustrato questo concetto.

```csharp
string[] values = { "49", "9", "06" };
TimeSpan interval;
foreach (string value in values)
{
   if (TimeSpan.TryParseExact(value, "ss", null, out interval))
      Console.WriteLine(interval.ToString("c"));
   else
      Console.WriteLine("Unable to convert '{0}' to a time interval", 
                        value);   
}
// The example displays the following output:
//       00:00:49
//       Unable to convert '9' to a time interval
//       00:00:06
```

```vb
Dim values() As String = { "49", "9", "06" }
Dim interval As TimeSpan
For Each value As String In values
   If TimeSpan.TryParseExact(value, "ss", Nothing, interval) Then
      Console.WriteLine(interval.ToString("c"))
   Else
      Console.WriteLine("Unable to convert '{0}' to a time interval", 
                        value)   
   End If   
Next   
' The example displays the following output:
'       00:00:49
'       Unable to convert '9' to a time interval
'       00:00:06
```

Nell'esempio seguente viene illustrato l'uso dell'identificatore di formato personalizzato "ss".

```csharp
TimeSpan interval1 = TimeSpan.FromSeconds(12.60);
Console.WriteLine(interval1.ToString(xref:"ss\.fff"));

TimeSpan interval2 = TimeSpan.FromSeconds(6.485);
Console.WriteLine(interval2.ToString(xref:"ss\.fff"));
// The example displays the following output:
//       12.600
//       06.485
```

```vb
Dim interval1 As TimeSpan = TimeSpan.FromSeconds(12.60)
Console.WriteLine(interval1.ToString("ss\.fff"))
Dim interval2 As TimeSpan = TimeSpan.FromSeconds(6.485)
Console.WriteLine(interval2.ToString("ss\.fff"))
' The example displays the following output:
'       12.600
'       06.485
```

## <a name="the-f-custom-format-specifier"></a>Identificatore di formato personalizzato "f"

L'identificatore di formato personalizzato "f" restituisce i decimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente una sola cifra frazionaria. 

Se l'identificatore di formato personalizzato "f" viene usato da solo, specificare "%f" in modo che non venga interpretato erroneamente come stringa in formato standard.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "f" per visualizzare i decimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). "f" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "ff"

L'identificatore di formato personalizzato "ff" restituisce i centesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente due cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "ff" per visualizzare i centesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). "ff" viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "fff"

L'identificatore di formato personalizzato "fff" (con tre caratteri "f") restituisce i millisecondi in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente tre cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "fff" per visualizzare i millisecondi in un valore [TimeSpan](xref:System.TimeSpan). "fff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffff"
L'identificatore di formato personalizzato "ffff" (con quattro caratteri "f") restituisce i decimillesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente quattro cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "ffff" per visualizzare i decimillesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). "ffff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffff"
L'identificatore di formato personalizzato "fffff" (con cinque caratteri "f") restituisce i centesimi di millesimo di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente cinque cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "fffff" per visualizzare i centesimi di millesimo di secondo in un valore [TimeSpan](xref:System.TimeSpan). "fffff" viene usato prima come unico identificatore di formato e quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432 
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "ffffff"

L'identificatore di formato personalizzato "ffffff" (con sei caratteri "f") restituisce i milionesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente sei cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "ffffff" per visualizzare i milionesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). Viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432 
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "fffffff"

L'identificatore di formato personalizzato "fffffff" (con sette caratteri "f") restituisce i decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la stringa di input deve contenere esattamente sette cifre frazionarie. 

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "fffffff" per visualizzare il numero frazionario di tick in un valore [TimeSpan](xref:System.TimeSpan). Viene usato prima come unico identificatore di formato, quindi viene usato in combinazione con l'identificatore "s" in una stringa di formato personalizzato.

```csharp
TimeSpan ts = new TimeSpan(1003498765432);
string fmt;
Console.WriteLine(ts.ToString("c"));
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   if (fmt.Length == 1) fmt = "%" + fmt;
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts);
} 
Console.WriteLine();

for (int ctr = 1; ctr <= 7; ctr++) {
   fmt = new String('f', ctr);
   Console.WriteLine("{0,10}: {1:s\\." + fmt + "}", "s\\." + fmt, ts);
}
// The example displays the following output:
//               %f: 8
//               ff: 87
//              fff: 876
//             ffff: 8765
//            fffff: 87654
//           ffffff: 876543
//          fffffff: 8765432
//       
//              s\.f: 29.8
//             s\.ff: 29.87
//            s\.fff: 29.876
//           s\.ffff: 29.8765
//          s\.fffff: 29.87654
//         s\.ffffff: 29.876543
//        s\.fffffff: 29.8765432 
```

```vb
Dim ts As New TimeSpan(1003498765432)
Dim fmt As String
Console.WriteLine(ts.ToString("c"))
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   If fmt.Length = 1 Then fmt = "%" + fmt
   Console.WriteLine("{0,10}: {1:" + fmt + "}", fmt, ts)
Next 
Console.WriteLine()

For ctr = 1 To 7
   fmt = New String("f"c, ctr)
   Console.WriteLine("{0,10}: {1:s\." + fmt + "}", "s\." + fmt, ts)
Next
' The example displays the following output:
'            %f: 8
'            ff: 87
'           fff: 876
'          ffff: 8765
'         fffff: 87654
'        ffffff: 876543
'       fffffff: 8765432
'    
'           s\.f: 29.8
'          s\.ff: 29.87
'         s\.fff: 29.876
'        s\.ffff: 29.8765
'       s\.fffff: 29.87654
'      s\.ffffff: 29.876543
'     s\.fffffff: 29.8765432
```

## <a name="the-f-custom-format-specifier"></a>Identificatore di formato personalizzato "F"

L'identificatore di formato personalizzato "F" restituisce i decimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se il valore dei decimi di secondo dell'intervallo di tempo è zero, non viene incluso nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi di secondo è facoltativa.

Se l'identificatore di formato personalizzato "F" viene usato da solo, specificare "%F" in modo che non venga interpretato erroneamente come stringa in formato standard.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "F" per visualizzare i decimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.669");
Console.WriteLine("{0} ('%F') --> {0:%F}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.091");
Console.WriteLine("{0} ('ss\\.F') --> {0:ss\\.F}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.1", "0:0:03.12" };
string fmt = @"h\:m\:ss\.F";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}                        
// The example displays the following output:
//       Formatting:
//       00:00:03.6690000 ('%F') --> 6
//       00:00:03.0910000 ('ss\.F') --> 03.
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.F') --> 00:00:03
//       0:0:03.1 ('h\:m\:ss\.F') --> 00:00:03.1000000
//       Cannot parse 0:0:03.12 with 'h\:m\:ss\.F'.
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.669")
Console.WriteLine("{0} ('%F') --> {0:%F}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.091")
Console.WriteLine("{0} ('ss\.F') --> {0:ss\.F}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.1", "0:0:03.12" }
Dim fmt As String = "h\:m\:ss\.F"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6690000 ('%F') --> 6
'       00:00:03.0910000 ('ss\.F') --> 03.
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.F') --> 00:00:03
'       0:0:03.1 ('h\:m\:ss\.F') --> 00:00:03.1000000
'       Cannot parse 0:0:03.12 with 'h\:m\:ss\.F'.
```

## <a name="the-ff-custom-format-specifier"></a>Identificatore di formato personalizzato "FF"

L'identificatore di formato personalizzato "FF" restituisce i centesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi e dei centesimi di secondo è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FF" per visualizzare i centesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.697");
Console.WriteLine("{0} ('FF') --> {0:FF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.809");
Console.WriteLine("{0} ('ss\\.FF') --> {0:ss\\.FF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.1", "0:0:03.127" };
string fmt = @"h\:m\:ss\.FF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}
// The example displays the following output:
//       Formatting:
//       00:00:03.6970000 ('FF') --> 69
//       00:00:03.8090000 ('ss\.FF') --> 03.8
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.FF') --> 00:00:03
//       0:0:03.1 ('h\:m\:ss\.FF') --> 00:00:03.1000000
//       Cannot parse 0:0:03.127 with 'h\:m\:ss\.FF'. 
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.697")
Console.WriteLine("{0} ('FF') --> {0:FF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.809")
Console.WriteLine("{0} ('ss\.FF') --> {0:ss\.FF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.1", "0:0:03.127" }
Dim fmt As String = "h\:m\:ss\.FF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6970000 ('FF') --> 69
'       00:00:03.8090000 ('ss\.FF') --> 03.8
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.FF') --> 00:00:03
'       0:0:03.1 ('h\:m\:ss\.FF') --> 00:00:03.1000000
'       Cannot parse 0:0:03.127 with 'h\:m\:ss\.FF'.
```

## <a name="the-fff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFF"

L'identificatore di formato personalizzato "FFF" (con tre caratteri "F") restituisce i millisecondi in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi, dei centesimi e dei millesimi di secondo è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FFF" per visualizzare i millesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.6974");
Console.WriteLine("{0} ('FFF') --> {0:FFF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.8009");
Console.WriteLine("{0} ('ss\\.FFF') --> {0:ss\\.FFF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.12", "0:0:03.1279" };
string fmt = @"h\:m\:ss\.FFF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}
// The example displays the following output:
//       Formatting:
//       00:00:03.6974000 ('FFF') --> 697
//       00:00:03.8009000 ('ss\.FFF') --> 03.8
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.FFF') --> 00:00:03
//       0:0:03.12 ('h\:m\:ss\.FFF') --> 00:00:03.1200000
//       Cannot parse 0:0:03.1279 with 'h\:m\:ss\.FFF'.  
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.6974")
Console.WriteLine("{0} ('FFF') --> {0:FFF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.8009")
Console.WriteLine("{0} ('ss\.FFF') --> {0:ss\.FFF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.12", "0:0:03.1279" }
Dim fmt As String = "h\:m\:ss\.FFF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6974000 ('FFF') --> 697
'       00:00:03.8009000 ('ss\.FFF') --> 03.8
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.FFF') --> 00:00:03
'       0:0:03.12 ('h\:m\:ss\.FFF') --> 00:00:03.1200000
'       Cannot parse 0:0:03.1279 with 'h\:m\:ss\.FFF'.
```

## <a name="the-ffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFF"

L'identificatore di formato personalizzato "FFFF" (con quattro caratteri "F") restituisce i decimillesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi, dei centesimi, dei millesimi e dei decimillesimi di secondo è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FFFF" per visualizzare i decimillesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). L'identificatore di formato personalizzato "FFFF" viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.69749");
Console.WriteLine("{0} ('FFFF') --> {0:FFFF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.80009");
Console.WriteLine("{0} ('ss\\.FFFF') --> {0:ss\\.FFFF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.12", "0:0:03.12795" };
string fmt = @"h\:m\:ss\.FFFF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}
// The example displays the following output:
//       Formatting:
//       00:00:03.6974900 ('FFFF') --> 6974
//       00:00:03.8000900 ('ss\.FFFF') --> 03.8
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.FFFF') --> 00:00:03
//       0:0:03.12 ('h\:m\:ss\.FFFF') --> 00:00:03.1200000
//       Cannot parse 0:0:03.12795 with 'h\:m\:ss\.FFFF'.
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.69749")
Console.WriteLine("{0} ('FFFF') --> {0:FFFF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.80009")
Console.WriteLine("{0} ('ss\.FFFF') --> {0:ss\.FFFF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.12", "0:0:03.12795" }
Dim fmt As String = "h\:m\:ss\.FFFF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6974900 ('FFFF') --> 6974
'       00:00:03.8000900 ('ss\.FFFF') --> 03.8
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.FFFF') --> 00:00:03
'       0:0:03.12 ('h\:m\:ss\.FFFF') --> 00:00:03.1200000
'       Cannot parse 0:0:03.12795 with 'h\:m\:ss\.FFFF'.
```

## <a name="the-fffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFF"

L'identificatore di formato personalizzato "FFFFF" (con cinque caratteri "F") restituisce i centesimi di millesimo di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi, dei centesimi, dei millesimi, dei decimillesimi e dei centesimi di millesimo di secondo è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FFFFF" per visualizzare i centesimi di millesimo di secondo in un valore [TimeSpan](xref:System.TimeSpan). L'identificatore di formato personalizzato "FFFFF" viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.697497");
Console.WriteLine("{0} ('FFFFF') --> {0:FFFFF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.800009");
Console.WriteLine("{0} ('ss\\.FFFFF') --> {0:ss\\.FFFFF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.12", "0:0:03.127956" };
string fmt = @"h\:m\:ss\.FFFFF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}                       
// The example displays the following output:
//       Formatting:
//       00:00:03.6974970 ('FFFFF') --> 69749
//       00:00:03.8000090 ('ss\.FFFFF') --> 03.8
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.FFFF') --> 00:00:03
//       0:0:03.12 ('h\:m\:ss\.FFFF') --> 00:00:03.1200000
//       Cannot parse 0:0:03.127956 with 'h\:m\:ss\.FFFF'. 
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.697497")
Console.WriteLine("{0} ('FFFFF') --> {0:FFFFF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.800009")
Console.WriteLine("{0} ('ss\.FFFFF') --> {0:ss\.FFFFF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.12", "0:0:03.127956" }
Dim fmt As String = "h\:m\:ss\.FFFFF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6974970 ('FFFFF') --> 69749
'       00:00:03.8000090 ('ss\.FFFFF') --> 03.8
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.FFFF') --> 00:00:03
'       0:0:03.12 ('h\:m\:ss\.FFFF') --> 00:00:03.1200000
'       Cannot parse 0:0:03.127956 with 'h\:m\:ss\.FFFF'.
```

## <a name="the-ffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFF"

L'identificatore di formato personalizzato "FFFFFF" (con sei caratteri "F") restituisce i milionesimi di secondo in un intervallo di tempo. In un'operazione di formattazione qualsiasi cifra frazionaria rimanente viene troncata. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza della cifra dei decimi, dei centesimi, dei millesimi, dei decimillesimi, dei centesimi di millesimo e dei milionesimi di secondo è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FFFFFF" per visualizzare i milionesimi di secondo in un valore [TimeSpan](xref:System.TimeSpan). Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.6974974");
Console.WriteLine("{0} ('FFFFFF') --> {0:FFFFFF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.8000009");
Console.WriteLine("{0} ('ss\\.FFFFFF') --> {0:ss\\.FFFFFF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.12", "0:0:03.1279569" };
string fmt = @"h\:m\:ss\.FFFFFF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}                       
// The example displays the following output:
//       Formatting:
//       00:00:03.6974974 ('FFFFFF') --> 697497
//       00:00:03.8000009 ('ss\.FFFFFF') --> 03.8
//       
//       Parsing:
//       0:0:03. ('h\:m\:ss\.FFFFFF') --> 00:00:03
//       0:0:03.12 ('h\:m\:ss\.FFFFFF') --> 00:00:03.1200000
//       Cannot parse 0:0:03.1279569 with 'h\:m\:ss\.FFFFFF'.
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.6974974")
Console.WriteLine("{0} ('FFFFFF') --> {0:FFFFFF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.8000009")
Console.WriteLine("{0} ('ss\.FFFFFF') --> {0:ss\.FFFFFF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.12", "0:0:03.1279569" }
Dim fmt As String = "h\:m\:ss\.FFFFFF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'       Formatting:
'       00:00:03.6974974 ('FFFFFF') --> 697497
'       00:00:03.8000009 ('ss\.FFFFFF') --> 03.8
'       
'       Parsing:
'       0:0:03. ('h\:m\:ss\.FFFFFF') --> 00:00:03
'       0:0:03.12 ('h\:m\:ss\.FFFFFF') --> 00:00:03.1200000
'       Cannot parse 0:0:03.1279569 with 'h\:m\:ss\.FFFFFF'
```

## <a name="the-fffffff-custom-format-specifier"></a>Identificatore di formato personalizzato "FFFFFFF"

L'identificatore di formato personalizzato "FFFFFFF" (con sette caratteri "F") restituisce i decimilionesimi di secondo (o il numero frazionario di tick) in un intervallo di tempo. Se sono presenti zeri frazionari finali, non vengono inclusi nella stringa del risultato. In un'operazione di analisi che chiama il metodo [TimeSpan.ParseExact](xref:System.TimeSpan.ParseExact(System.String,System.String,System.IFormatProvider)) o [TimeSpan.TryParseExact](xref:System.TimeSpan.TryParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.TimeSpanStyles,System.TimeSpan@)) la presenza delle sette cifre frazionarie nella stringa di input è facoltativa.

Nell'esempio seguente viene usato l'identificatore di formato personalizzato "FFFFFFF" per visualizzare la parte frazionaria di un secondo in un valore [TimeSpan](xref:System.TimeSpan). Questo identificatore di formato personalizzato viene usato anche in un'operazione di analisi.

```csharp
Console.WriteLine("Formatting:");
TimeSpan ts1 = TimeSpan.Parse("0:0:3.6974974");
Console.WriteLine("{0} ('FFFFFFF') --> {0:FFFFFFF}", ts1);

TimeSpan ts2 = TimeSpan.Parse("0:0:3.9500000");
Console.WriteLine("{0} ('ss\\.FFFFFFF') --> {0:ss\\.FFFFFFF}", ts2);
Console.WriteLine();

Console.WriteLine("Parsing:");
string[] inputs = { "0:0:03.", "0:0:03.12", "0:0:03.1279569" };
string fmt = @"h\:m\:ss\.FFFFFFF";
TimeSpan ts3;

foreach (string input in inputs) {
   if (TimeSpan.TryParseExact(input, fmt, null, out ts3))
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3);
   else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt);
}
// The example displays the following output:
//    Formatting:
//    00:00:03.6974974 ('FFFFFFF') --> 6974974
//    00:00:03.9500000 ('ss\.FFFFFFF') --> 03.95
//    
//    Parsing:
//    0:0:03. ('h\:m\:ss\.FFFFFFF') --> 00:00:03
//    0:0:03.12 ('h\:m\:ss\.FFFFFFF') --> 00:00:03.1200000
//    0:0:03.1279569 ('h\:m\:ss\.FFFFFFF') --> 00:00:03.1279569 
```

```vb
Console.WriteLine("Formatting:")
Dim ts1 As TimeSpan = TimeSpan.Parse("0:0:3.6974974")
Console.WriteLine("{0} ('FFFFFFF') --> {0:FFFFFFF}", ts1)

Dim ts2 As TimeSpan = TimeSpan.Parse("0:0:3.9500000")
Console.WriteLine("{0} ('ss\.FFFFFFF') --> {0:ss\.FFFFFFF}", ts2)
Console.WriteLine()

Console.WriteLine("Parsing:")
Dim inputs() As String = { "0:0:03.", "0:0:03.12", "0:0:03.1279569" }
Dim fmt As String = "h\:m\:ss\.FFFFFFF"
Dim ts3 As TimeSpan

For Each input As String In inputs
   If TimeSpan.TryParseExact(input, fmt, Nothing, ts3)
      Console.WriteLine("{0} ('{1}') --> {2}", input, fmt, ts3)
   Else
      Console.WriteLine("Cannot parse {0} with '{1}'.", 
                        input, fmt)
   End If  
Next
' The example displays the following output:
'    Formatting:
'    00:00:03.6974974 ('FFFFFFF') --> 6974974
'    00:00:03.9500000 ('ss\.FFFFFFF') --> 03.95
'    
'    Parsing:
'    0:0:03. ('h\:m\:ss\.FFFFFFF') --> 00:00:03
'    0:0:03.12 ('h\:m\:ss\.FFFFFFF') --> 00:00:03.1200000
'    0:0:03.1279569 ('h\:m\:ss\.FFFFFFF') --> 00:00:03.1279569  
```

## <a name="other-characters"></a>Altri caratteri

Qualsiasi altro carattere senza codice di escape in una stringa di formato, incluso un carattere di spazio vuoto, viene interpretato come identificatore di formato personalizzato. Nella maggior parte dei casi la presenza di qualsiasi altro carattere senza codice di escape restituisce un oggetto [FormatException](xref:System.FormatException). 

È possibile includere un carattere letterale in una stringa di formato in due modi:

* Racchiudendolo tra virgolette singole (delimitatore di stringa letterale). 

* Inserendo prima del carattere una barra rovesciata("\"), interpretata come carattere di escape. In C#, pertanto, la stringa di formato deve essere @-quoted, o il carattere letterale deve essere preceduto da una barra rovesciata aggiuntiva.

  In alcuni casi, potrebbe essere necessario utilizzare la logica condizionale per includere un valore letterale preceduto da una barra rovesciata in una stringa di formato. Nell'esempio seguente viene utilizzata la logica condizionale per includere un simbolo di segno per intervalli di tempo negativi. 
  
  ```csharp
  using System;

  public class Example
  {
     public static void Main()
     {
        TimeSpan result = new DateTime(2010, 01, 01) - DateTime.Now; 
        String fmt = (result < TimeSpan.Zero ?  "\\-" : "") + "dd\\.hh\\:mm";

        Console.WriteLine(result.ToString(fmt));
        Console.WriteLine("Interval: {0:" + fmt + "}", result);
     }
  }
  // The example displays output like the following:
  //       -1291.10:54
  //       Interval: -1291.10:54
  ```

  ```vb
  Module Example
     Public Sub Main()
        Dim result As TimeSpan = New DateTime(2010, 01, 01) - Date.Now 
        Dim fmt As String = If(result < TimeSpan.Zero, "\-", "") + "dd\.hh\:mm"

        Console.WriteLine(result.ToString(fmt))
        Console.WriteLine("Interval: {0:" + fmt + "}", result)
     End Sub
  End Module
  ' The example displays output like the following:
  '       -1291.10:54
  '       Interval: -1291.10:54
  ```
  
In .NET non viene definita una grammatica per i separatori negli intervalli di tempo. I separatori tra giorni e ore, ore e minuti, minuti e secondi e secondi e frazioni di secondo devono pertanto essere trattati come valori letterali carattere in una stringa di formato.

Nell'esempio seguente vengono usati sia il carattere di escape che la virgoletta singola per definire una stringa di formato personalizzata che include la parola "minutes" nella stringa di output. 

```csharp
TimeSpan interval = new TimeSpan(0, 32, 45);
// Escape literal characters in a format string.
string fmt = @"mm\:ss\ \m\i\n\u\t\e\s";
Console.WriteLine(interval.ToString(fmt));
// Delimit literal characters in a format string with the ' symbol.
fmt = "mm':'ss' minutes'";      
Console.WriteLine(interval.ToString(fmt));
// The example displays the following output: 
//       32:45 minutes      
//       32:45 minutes
```

```vb
Dim interval As New TimeSpan(0, 32, 45)
' Escape literal characters in a format string.
Dim fmt As String = "mm\:ss\ \m\i\n\u\t\e\s"
Console.WriteLine(interval.ToString(fmt))
' Delimit literal characters in a format string with the ' symbol.
fmt = "mm':'ss' minutes'"
Console.WriteLine(interval.ToString(fmt))
' The example displays the following output: 
'       32:45 minutes      
'       32:45 minutes
```

## <a name="see-also"></a>Vedere anche

[Formattazione di tipi](formatting-types.md)

[Stringhe di formato TimeSpan standard](standard-timespan.md)  




<!--HONumber=Nov16_HO1-->


