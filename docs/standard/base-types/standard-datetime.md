---
title: Stringhe di formato di data e ora standard
description: Stringhe di formato di data e ora standard
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/25/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: be239871-10cc-4949-b548-200bb260630a
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 1196459d74038edb1268c619dac3da69f38e7860

---

# <a name="standard-date-and-time-format-strings"></a>Stringhe di formato di data e ora standard

Una stringa di formato data e ora standard usa un singolo identificatore di formato per definire la rappresentazione di testo di un valore di data e ora. Qualsiasi stringa di formato data e ora contenente più di un carattere, inclusi gli spazi, viene interpretata come una stringa di formato data e ora personalizzata. Per altre informazioni, vedere [Stringhe di formato di data e ora personalizzato](custom-datetime.md). Una stringa di formato standard o personalizzata può essere usata in due modi:

* Per definire la stringa risultante da un'operazione di formattazione.

* Per definire la rappresentazione di testo di un valore di data e ora che può essere convertito in un valore [DateTime](xref:System.DateTime) o [DateTimeOffset](xref:System.DateTimeOffset) da un'operazione di analisi.

Le stringhe di formato data e ora standard possono essere usate con i valori [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset). 

Nella tabella seguente vengono descritti gli identificatori di formato di data e ora standard. Se non specificato diversamente, un identificatore di formato di data e ora standard specifico genera una rappresentazione di stringa identica, indipendentemente dal fatto che venga usato con un valore [DateTime](xref:System.DateTime) o con un valore [DateTimeOffset](xref:System.DateTimeOffset). Per altre informazioni sull'uso di stringhe di formato di data e ora standard, vedere la sezione [Note](#notes).

Identificatore di formato | Descrizione | Esempi
---------------- | ----------- | --------
"d" | Schema di data breve. | `2009-06-15T13:45:30 -> 6/15/2009 (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 (fr-FR)`; `2009-06-15T13:45:30 -> 2009/06/15 (ja-JP)`
"D" | Schema di data estesa. | `2009-06-15T13:45:30 -> Monday, June 15, 2009 (en-US)`; `2009-06-15T13:45:30 -> 15 июня 2009 г. (ru-RU)`; `2009-06-15T13:45:30 -> Montag, 15. Juni 2009 (de-DE)`
"f" | Schema di data/ora completa (ora breve). | `2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 13:45 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45 μμ (el-GR)`
"F" | Schema di data/ora completa (ora estesa). | `2009-06-15T13:45:30 -> Monday, June 15, 2009 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 13:45:30 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 1:45:30 μμ (el-GR)`
"g" | Schema di data/ora generale (ora breve). | `2009-06-15T13:45:30 -> 6/15/2009 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 13:45 (es-ES)`; `2009-06-15T13:45:30 -> 2009/6/15 13:45 (zh-CN)`
"G" | Schema di data/ora generale (ora estesa). | `2009-06-15T13:45:30 -> 6/15/2009 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> 15/06/2009 13:45:30 (es-ES)`; `2009-06-15T13:45:30 -> 2009/6/15 13:45:30 (zh-CN)`
"M", "m" | Schema di mese/giorno. | `2009-06-15T13:45:30 -> June 15 (en-US)`; `2009-06-15T13:45:30 -> 15. juni (da-DK)`; `2009-06-15T13:45:30 -> 15 Juni (id-ID)`
"O", "o" | Schema di data/ora di round trip. | Valori [DateTime](xref:System.DateTime): `2009-06-15T13:45:30 (DateTimeKind.Local) --> 2009-06-15T13:45:30.0000000-07:00`; `2009-06-15T13:45:30 (DateTimeKind.Utc) --> 2009-06-15T13:45:30.0000000Z`; `2009-06-15T13:45:30 (DateTimeKind.Unspecified) --> 2009-06-15T13:45:30.0000000`. Valori [DateTimeOffset](xref:System.DateTimeOffset): `2009-06-15T13:45:30-07:00 --> 2009-06-15T13:45:30.0000000-07:00`
"R", "r" | Schema RFC1123. | `2009-06-15T13:45:30 -> Mon, 15 Jun 2009 20:45:30 GMT`
"s" | Schema di data/ora ordinabile. | `2009-06-15T13:45:30 (DateTimeKind.Local) -> 2009-06-15T13:45:30`; `2009-06-15T13:45:30 (DateTimeKind.Utc) -> 2009-06-15T13:45:30`
"t" | Schema di ora breve. | `2009-06-15T13:45:30 -> 1:45 PM (en-US)`; `2009-06-15T13:45:30 -> 13:45 (hr-HR)`; `2009-06-15T13:45:30 -> 01:45 م (ar-EG)` 
"T" | Schema di ora estesa. | `2009-06-15T13:45:30 -> 1:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> 13:45:30 (hr-HR)`; `2009-06-15T13:45:30 -> 01:45:30 م (ar-EG)`
"u" | Schema di data/ora ordinabile universale. | Con un valore [DateTime](xref:System.DateTime): `2009-06-15T13:45:30 -> 2009-06-15 13:45:30Z`. Con un valore [DateTimeOffset](xref:System.DateTimeOffset): `2009-06-15T13:45:30 -> 2009-06-15 20:45:30Z`
"U" | Schema di data/ora completa universale. | `2009-06-15T13:45:30 -> Monday, June 15, 2009 8:45:30 PM (en-US)`; `2009-06-15T13:45:30 -> den 15 juni 2009 20:45:30 (sv-SE)`; `2009-06-15T13:45:30 -> Δευτέρα, 15 Ιουνίου 2009 8:45:30 μμ (el-GR)`
"Y", "y" | Schema di mese e anno. | `2009-06-15T13:45:30 -> June, 2009 (en-US)`; `2009-06-15T13:45:30 -> juni 2009 (da-DK)`; `2009-06-15T13:45:30 -> Juni 2009 (id-ID)`
Qualsiasi altro carattere singolo | Identificatore sconosciuto. | Genera un'eccezione in fase di esecuzione [FormatException](xref:System.FormatException).

## <a name="how-standard-format-strings-work"></a>Funzionamento delle stringhe di formato standard

In un'operazione di formattazione, una stringa di formato standard è semplicemente un alias per una stringa di formato personalizzata. Il vantaggio dell'uso di un alias per fare riferimento a una stringa di formato personalizzata consiste nel fatto che, sebbene l'alias sia invariante, la stringa di formato personalizzata può variare. Questo aspetto è importante perché le rappresentazioni di stringa di valori di data e ora variano in genere in base alle impostazioni cultura. La stringa di formato standard "d" indica, ad esempio, che un valore di data e ora deve essere visualizzato usando uno schema di data breve. Per le impostazioni cultura invarianti questo schema è "MM/dd/yyyy". Per le impostazioni cultura fr-FR questo schema è "dd/MM/yyyy". Per le impostazioni cultura ja-JP questo schema è "yyyy/MM/dd".

Se in un'operazione di formattazione viene eseguito il mapping di una stringa di formato standard alla stringa di formato personalizzata di impostazioni cultura particolari, nell'applicazione possono essere definite le impostazioni cultura specifiche le cui stringhe di formato personalizzate vengono usate in una di queste modalità:

* È possibile usare le impostazioni cultura predefinite, o correnti. Nell'esempio seguente viene visualizzata una data usando il formato di data breve delle impostazioni cultura correnti. In questo caso le impostazioni cultura correnti sono en-US. 

  ```csharp
  // Display using current (en-us) culture's short date format
  DateTime thisDate = new DateTime(2008, 3, 15);
  Console.WriteLine(thisDate.ToString("d"));           // Displays 3/15/2008
  ```

  ```vb
  ' Display using current (en-us) culture's short date format
  Dim thisDate As Date = #03/15/2008#
  Console.WriteLine(thisDate.ToString("d"))     ' Displays 3/15/2008
  ```
  
* È possibile passare un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta le impostazioni cultura di cui deve essere usata la formattazione a un metodo con un parametro [IFormatProvider](xref:System.IFormatProvider). Nell'esempio seguente viene visualizzata una data usando il formato di data breve delle impostazioni cultura pt-BR.
  
  ```csharp
  // Display using pt-BR culture's short date format
  DateTime thisDate = new DateTime(2008, 3, 15);
  CultureInfo culture = new CultureInfo("pt-BR");      
  Console.WriteLine(thisDate.ToString("d", culture));  // Displays 15/3/2008
  ```

  ```vb
  ' Display using pt-BR culture's short date format
  Dim thisDate As Date = #03/15/2008#
  Dim culture As New CultureInfo("pt-BR")      
  Console.WriteLine(thisDate.ToString("d", culture))   ' Displays 15/3/2008
  ```
  
* È possibile passare un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che specifica informazioni di formattazione a un metodo con un parametro [IFormatProvider](xref:System.IFormatProvider). Nell'esempio seguente viene visualizzata una data che usa il formato di data breve da un oggetto DateTimeFormatInfo per le impostazioni cultura hr-HR.  

  ```csharp
  // Display using date format information from hr-HR culture
  DateTime thisDate = new DateTime(2008, 3, 15);
  DateTimeFormatInfo fmt = (new CultureInfo("hr-HR")).DateTimeFormat;
  Console.WriteLine(thisDate.ToString("d", fmt));      // Displays 15.3.2008
  ```

  ```vb
  ' Display using date format information from hr-HR culture
  Dim thisDate As Date = #03/15/2008#
  Dim fmt As DateTimeFormatInfo = (New CultureInfo("hr-HR")).DateTimeFormat
  Console.WriteLine(thisDate.ToString("d", fmt))   ' Displays 15.3.2008
  ```
  
In alcuni casi la stringa di formato standard serve come una pratica abbreviazione per una stringa di formato personalizzata più lunga, che è invariante. In questa categoria rientrano quattro stringhe di formato standard: "O" (o "o"), "R" (o "r"), "s" e "u". Queste stringhe corrispondono a stringhe di formato personalizzate definite dalle impostazioni cultura invarianti. Producono rappresentazioni di stringa di valori di data e ora che dovranno essere identiche nelle diverse impostazioni cultura. Nella tabella seguente vengono fornite informazioni su queste quattro stringhe di formato di data e ora standard.

Stringa di formato standard | Definita dalla proprietà DateTimeFormatInfo.InvariantInfo | Stringa di formato personalizzata
---------------------- | ---------------------------------------------------- | --------------------
"O" o "o" | Nessuno | yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzz
"R" o "r" | [RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) | ddd, dd MMM yyyy HH':'mm':'ss 'GMT'
"s" | [SortableDateTime](xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern) | yyyy'-'MM'-'dd'T'HH':'mm':'ss
"u" | [UniversalSortableDateTime](xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern) | yyyy'-'MM'-'dd HH':'mm':'ss'Z'

Nelle sezioni seguenti vengono descritti gli identificatori di formato standard per i valori [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset).

## <a name="the-short-date-d-format-specifier"></a>Identificatore di formato di data breve ("d")

L'identificatore di formato standard "d" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) di una specifica impostazione cultura. La stringa di formato personalizzato restituita dalla proprietà [ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) delle impostazioni cultura per la lingua inglese è, ad esempio, "MM/dd/yyyy". 

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita.
Nell'esempio seguente viene usato l'identificatore di formato "d" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008,4, 10);
Console.WriteLine(date1.ToString("d", DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays 4/10/2008                       
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("en-NZ")));
// Displays 10/04/2008                       
Console.WriteLine(date1.ToString("d", 
                  CultureInfo.CreateSpecificCulture("de-DE")));
// Displays 10.04.2008 
```

```vb
Dim date1 As Date = #4/10/2008#
Console.WriteLine(date1.ToString("d", DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays 4/10/2008                       
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("en-NZ")))
' Displays 10/04/2008                       
Console.WriteLine(date1.ToString("d", _
                  CultureInfo.CreateSpecificCulture("de-DE")))
' Displays 10.04.2008 
```

## <a name="the-long-date-d-format-specifier"></a>Identificatore di formato di data estesa ("D")

L'identificatore di formato standard "D" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "dddd, dd MMMM yyyy".

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita.

Proprietà | Descrizione
-------- | -----------
[LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) | Definisce il formato complessivo della stringa di risultato.
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.

Nell'esempio seguente viene usato l'identificatore di formato "D" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10);
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008                        
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("pt-BR")));
// Displays quinta-feira, 10 de abril de 2008                        
Console.WriteLine(date1.ToString("D", 
                  CultureInfo.CreateSpecificCulture("es-MX")));
// Displays jueves, 10 de abril de 2008
```

```vb
Dim date1 As Date = #4/10/2008#
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008                        
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("pt-BR")))
' Displays quinta-feira, 10 de abril de 2008                        
Console.WriteLine(date1.ToString("D", _
                  CultureInfo.CreateSpecificCulture("es-MX")))
' Displays jueves, 10 de abril de 2008
```

## <a name="the-full-date-short-time-f-format-specifier"></a>Identificatore di formato di ora breve e data completa ("f")

L'identificatore di formato standard "f" rappresenta una combinazione degli schemi di data estesa ("D") e ora breve ("t"), separati da uno spazio.

La stringa risultato è influenzata dalle informazioni sulla formattazione di un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) e [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.LongDatePattern) | Definisce il formato del componente relativo alla data della stringa di risultato.
[ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | Definisce il formato del componente relativo all'ora della stringa di risultato.
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "f" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("f", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 6:30 AM                        
Console.WriteLine(date1.ToString("f", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays jeudi 10 avril 2008 06:30 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("f", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 6:30 AM                        
Console.WriteLine(date1.ToString("f", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays jeudi 10 avril 2008 06:30 
```

## <a name="the-full-date-long-time-f-format-specifier"></a>Identificatore di formato di ora estesa e data completa ("F")

L'identificatore di formato standard "F" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "dddd, dd MMMM yyyy HH:mm:ss".

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà [FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) | Definisce il formato complessivo della stringa di risultato.
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "F" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("F", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("F", 
                  CultureInfo.CreateSpecificCulture("fr-FR")));
// Displays jeudi 10 avril 2008 06:30:00 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("F", _
                  CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("F", _
                  CultureInfo.CreateSpecificCulture("fr-FR")))
' Displays jeudi 10 avril 2008 06:30:00 
```

## <a name="the-general-date-short-time-g-format-specifier"></a>Identificatore di formato di ora breve e data generale ("g")

L'identificatore di formato standard "g" rappresenta una combinazione degli schemi di data breve ("d") e ora breve ("t"), separati da uno spazio.

La stringa risultato è influenzata dalle informazioni sulla formattazione di un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà [DateTimeFormatInfo.LongDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) e [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) | Definisce il formato del componente relativo alla data della stringa di risultato.
[ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | Definisce il formato del componente relativo all'ora della stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "g" per visualizzare un valore di data e ora. 

``` csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("g", 
                  DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008 06:30                      
Console.WriteLine(date1.ToString("g", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 4/10/2008 6:30 AM                       
Console.WriteLine(date1.ToString("g", 
                  CultureInfo.CreateSpecificCulture("fr-BE")));
// Displays 10/04/2008 6:30 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("g", _
                  DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008 06:30                      
Console.WriteLine(date1.ToString("g", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 4/10/2008 6:30 AM                       
Console.WriteLine(date1.ToString("g", _
                  CultureInfo.CreateSpecificCulture("fr-BE")))
' Displays 10/04/2008 6:30  
```

## <a name="the-general-date-long-time-g-format-specifier"></a>Identificatore di formato di ora estesa e data generale ("G")

L'identificatore di formato standard "G" rappresenta una combinazione degli schemi di data breve ("d") e ora estesa ("T"), separati da uno spazio.

La stringa risultato è influenzata dalle informazioni sulla formattazione di un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà [DateTimeFormatInfo.ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) e [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[ShortDatePattern](xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern) | Definisce il formato del componente relativo alla data della stringa di risultato.
[LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) | Definisce il formato del componente relativo all'ora della stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "G" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("G", 
                  DateTimeFormatInfo.InvariantInfo));
// Displays 04/10/2008 06:30:00
Console.WriteLine(date1.ToString("G", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 4/10/2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("G", 
                  CultureInfo.CreateSpecificCulture("nl-BE")));
// Displays 10/04/2008 6:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("G", _
                  DateTimeFormatInfo.InvariantInfo))
' Displays 04/10/2008 06:30:00
Console.WriteLine(date1.ToString("G", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 4/10/2008 6:30:00 AM                        
Console.WriteLine(date1.ToString("G", _
                  CultureInfo.CreateSpecificCulture("nl-BE")))
' Displays 10/04/2008 6:30:00                       
```

## <a name="the-month-m-m-format-specifier"></a>Identificatore di formato di mese ("M", "m")

L'identificatore di formato standard "M" o "m" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.MonthDayPattern](xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern) corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "MMMM dd".

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita.

Proprietà | Descrizione
-------- | -----------
[MonthDayPattern](xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern) | Definisce il formato complessivo della stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.

Nell'esempio seguente viene usato l'identificatore di formato "m" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("m", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays April 10                        
Console.WriteLine(date1.ToString("m", 
                  CultureInfo.CreateSpecificCulture("ms-MY")));
// Displays 10 April  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("m", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays April 10                        
Console.WriteLine(date1.ToString("m", _
                  CultureInfo.CreateSpecificCulture("ms-MY")))
' Displays 10 April
```

## <a name="the-roundtrip-o-o-format-specifier"></a>Identificatore di formato di round trip ("O", "o")

L'identificatore di formato standard "O" o "o" rappresenta una stringa di formato di data e ora personalizzata con uno schema che mantiene le informazioni sul fuso orario e crea una stringa di risultato conforme allo standard ISO 8601. Per i valori [DateTime](xref:System.DateTime), questo identificatore di formato è progettato per mantenere valori di data e ora insieme alla proprietà [DateTime.Kind](xref:System.DateTime.Kind) nel testo. La stringa formattata può essere analizzata tramite il metodo [DateTime.Parse(String, IFormatProvider, DateTimeStyles)](xref:System.DateTime.Parse(System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) o [DateTime.ParseExact](xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider,System.Globalization.DateTimeStyles)) se il parametro styles è impostato su [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind). 

L'identificatore di formato standard "O" o "o" corrisponde alla stringa di formato personalizzato "yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK" per valori DateTime e alla stringa di formato personalizzato "yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffzzz" per valori [DateTimeOffset](xref:System.DateTimeOffset). In questa stringa le coppie di virgolette singole che delimitano singoli caratteri, ad esempio trattini, due punti e la lettera "T", indicano che il singolo carattere è un valore letterale che non può essere modificato. Gli apostrofi non vengono visualizzati nella stringa di output. 

L'identificatore di formato standard "O" o "o" (e la stringa di formato personalizzato "yyyy'-'MM'-'dd'T'HH':'mm':'ss'.'fffffffK") sfrutta i tre modi in cui lo standard ISO 8601 rappresenta le informazioni sul fuso orario per mantenere la proprietà [Kind](xref:System.DateTime.Kind) dei valori [DateTime](xref:System.DateTime): 

* Il componente relativo al fuso orario dei valori di data e ora [DateTimeKind.Local](xref:System.DateTimeKind.Local) è un offset rispetto all'ora UTC (ad esempio +01:00, -07:00). Anche tutti i valori DateTimeOffset sono rappresentati in questo formato. 

* Il componente relativo al fuso orario dei valori di data e ora [DateTimeKind.Utc](xref:System.DateTimeKind.Utc) usa "Z" (che sta per zero offset) per rappresentare l'ora UTC. 

* I valori di data e ora [DateTimeKind.Unspecified](xref:System.DateTimeKind.Unspecified) non offrono informazioni sul fuso orario. 

Poiché l'identificatore di formato standard O" o "o" è conforme a uno standard internazionale, l'operazione di formattazione o analisi che usa l'identificatore usa sempre le impostazioni cultura invarianti e il calendario gregoriano. 

Le stringhe passate ai metodi `Parse`, `TryParse`, `ParseExact` e `TryParseExact` di [DateTime](xref:System.DateTime) e [DateTimeOffset](xref:System.DateTimeOffset) possono essere analizzate usando l'identificatore di formato "O" o "o" se sono in uno di questi formati. Nel caso degli oggetti [DateTime](xref:System.DateTime), l'overload di analisi chiamato deve anche includere un parametro styles con un valore [DateTimeStyles.RoundtripKind](xref:System.Globalization.DateTimeStyles.RoundtripKind). Tenere presente che se si chiama un metodo di analisi con la stringa di formato personalizzata che corrisponde all'identificatore di formato "O" o "o", non si otterranno gli stessi risultati di "O" o "o". Il motivo è che i metodi di analisi che usano una stringa di formato personalizzata non possono analizzare la rappresentazione in formato stringa di valori di data e ora in cui manca un componente di fuso orario o che usano "Z" per indicare l'ora UTC. 

Nell'esempio seguente viene usato l'identificatore di formato "o" per visualizzare una serie di valori [DateTime](xref:System.DateTime) e un valore [DateTimeOffset](xref:System.DateTimeOffset) in un sistema nel fuso orario Pacifico (Stati Uniti). 

```csharp
using System;

public class Example
{
   public static void Main()
   {
       DateTime dat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                   DateTimeKind.Unspecified);
       Console.WriteLine("{0} ({1}) --> {0:O}", dat, dat.Kind); 

       DateTime uDat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                    DateTimeKind.Utc);
       Console.WriteLine("{0} ({1}) --> {0:O}", uDat, uDat.Kind);

       DateTime lDat = new DateTime(2009, 6, 15, 13, 45, 30, 
                                    DateTimeKind.Local);
       Console.WriteLine("{0} ({1}) --> {0:O}\n", lDat, lDat.Kind);

       DateTimeOffset dto = new DateTimeOffset(lDat);
       Console.WriteLine("{0} --> {0:O}", dto);
   }
}
// The example displays the following output:
//    6/15/2009 1:45:30 PM (Unspecified) --> 2009-06-15T13:45:30.0000000
//    6/15/2009 1:45:30 PM (Utc) --> 2009-06-15T13:45:30.0000000Z
//    6/15/2009 1:45:30 PM (Local) --> 2009-06-15T13:45:30.0000000-07:00
//    
//    6/15/2009 1:45:30 PM -07:00 --> 2009-06-15T13:45:30.0000000-07:00
```

```vb
Module Example
   Public Sub Main()
       Dim dat As New Date(2009, 6, 15, 13, 45, 30, 
                           DateTimeKind.Unspecified)
       Console.WriteLine("{0} ({1}) --> {0:O}", dat, dat.Kind) 

       Dim uDat As New Date(2009, 6, 15, 13, 45, 30, DateTimeKind.Utc)
       Console.WriteLine("{0} ({1}) --> {0:O}", uDat, uDat.Kind)

       Dim lDat As New Date(2009, 6, 15, 13, 45, 30, DateTimeKind.Local)
       Console.WriteLine("{0} ({1}) --> {0:O}", lDat, lDat.Kind)
       Console.WriteLine()

       Dim dto As New DateTimeOffset(lDat)
       Console.WriteLine("{0} --> {0:O}", dto)
   End Sub
End Module
' The example displays the following output:
'    6/15/2009 1:45:30 PM (Unspecified) --> 2009-06-15T13:45:30.0000000
'    6/15/2009 1:45:30 PM (Utc) --> 2009-06-15T13:45:30.0000000Z
'    6/15/2009 1:45:30 PM (Local) --> 2009-06-15T13:45:30.0000000-07:00
'    
'    6/15/2009 1:45:30 PM -07:00 --> 2009-06-15T13:45:30.0000000-07:00
```

Nell'esempio seguente viene usato l'identificatore di formato "o" per creare una stringa formattata, quindi viene ripristinato il valore di data e ora originale chiamando un metodo `Parse` di data e ora.

```csharp
// Round-trip DateTime values.
DateTime originalDate, newDate;
string dateString;
// Round-trip a local time.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 10, 6, 30, 0), DateTimeKind.Local);
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);
// Round-trip a UTC time.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 12, 9, 30, 0), DateTimeKind.Utc);                  
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);
// Round-trip time in an unspecified time zone.
originalDate = DateTime.SpecifyKind(new DateTime(2008, 4, 13, 12, 30, 0), DateTimeKind.Unspecified);                  
dateString = originalDate.ToString("o");
newDate = DateTime.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, 
                  newDate, newDate.Kind);

// Round-trip a DateTimeOffset value.
DateTimeOffset originalDTO = new DateTimeOffset(2008, 4, 12, 9, 30, 0, new TimeSpan(-8, 0, 0));
dateString = originalDTO.ToString("o");
DateTimeOffset newDTO = DateTimeOffset.Parse(dateString, null, DateTimeStyles.RoundtripKind);
Console.WriteLine("Round-tripped {0} to {1}.", originalDTO, newDTO);
// The example displays the following output:
//    Round-tripped 4/10/2008 6:30:00 AM Local to 4/10/2008 6:30:00 AM Local.
//    Round-tripped 4/12/2008 9:30:00 AM Utc to 4/12/2008 9:30:00 AM Utc.
//    Round-tripped 4/13/2008 12:30:00 PM Unspecified to 4/13/2008 12:30:00 PM Unspecified.
//    Round-tripped 4/12/2008 9:30:00 AM -08:00 to 4/12/2008 9:30:00 AM -08:00.
```

```vb
' Round-trip DateTime values.
Dim originalDate, newDate As Date
Dim dateString As String
' Round-trip a local time.
originalDate = Date.SpecifyKind(#4/10/2008 6:30AM#, DateTimeKind.Local)
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)
' Round-trip a UTC time.
originalDate = Date.SpecifyKind(#4/12/2008 9:30AM#, DateTimeKind.Utc)                  
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)
' Round-trip time in an unspecified time zone.
originalDate = Date.SpecifyKind(#4/13/2008 12:30PM#, DateTimeKind.Unspecified)                  
dateString = originalDate.ToString("o")
newDate = Date.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} {1} to {2} {3}.", originalDate, originalDate.Kind, _
                  newDate, newDate.Kind)

' Round-trip a DateTimeOffset value.
Dim originalDTO As New DateTimeOffset(#4/12/2008 9:30AM#, New TimeSpan(-8, 0, 0))
dateString = originalDTO.ToString("o")
Dim newDTO As DateTimeOffset = DateTimeOffset.Parse(dateString, Nothing, DateTimeStyles.RoundtripKind)
Console.WriteLine("Round-tripped {0} to {1}.", originalDTO, newDTO)
' The example displays the following output:
'    Round-tripped 4/10/2008 6:30:00 AM Local to 4/10/2008 6:30:00 AM Local.
'    Round-tripped 4/12/2008 9:30:00 AM Utc to 4/12/2008 9:30:00 AM Utc.
'    Round-tripped 4/13/2008 12:30:00 PM Unspecified to 4/13/2008 12:30:00 PM Unspecified.
'    Round-tripped 4/12/2008 9:30:00 AM -08:00 to 4/12/2008 9:30:00 AM -08:00.
```

## <a name="the-rfc1123-r-r-format-specifier"></a>Identificatore di formato RFC1123 ("R", "r")

L'identificatore di formato standard "R" o "r" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) corrente. Lo schema riflette uno standard definito e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "ddd, dd MMM yyyy HH':'mm':'ss 'GMT". Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti.

La stringa di risultato è influenzata dalle proprietà seguenti dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) restituito dalla proprietà [DateTimeFormatInfo.InvariantInfo](xref:System.Globalization.DateTimeFormatInfo.InvariantInfo) che rappresenta le impostazioni cultura per la lingua inglese.

Proprietà | Descrizione
-------- | -----------
[RFC1123Pattern](xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern) | Definisce il formato della stringa di risultato.
[AbbreviatedDayNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames) | Definisce i nomi dei giorni abbreviati che possono essere visualizzati nella stringa di risultato.
[AbbreviatedMonthNames](xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames) | Definisce i nomi dei mesi abbreviati che possono essere visualizzati nella stringa di risultato.

Anche se lo standard RFC 1123 esprime un'ora in formato UTC (Coordinated Universal Time), l'operazione di formattazione non comporta la modifica del valore dell'oggetto [DateTime](xref:System.DateTime) che viene formattato. È pertanto necessario convertire il valore [DateTime](xref:System.DateTime) in formato UTC chiamando il metodo [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime) prima di eseguire l'operazione di formattazione. Al contrario, i valori [DateTimeOffset](xref:System.DateTimeOffset) eseguono questa conversione automaticamente; non è necessario chiamare il metodo [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) prima dell'operazione di formattazione. 

Nell'esempio seguente viene usato l'identificatore di formato "r" per visualizzare una serie di valori [DateTime](xref:System.DateTime) e un valore [DateTimeOffset](xref:System.DateTimeOffset) in un sistema nel fuso orario Pacifico (Stati Uniti).

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
DateTimeOffset dateOffset = new DateTimeOffset(date1, 
                            TimeZoneInfo.Local.GetUtcOffset(date1));
Console.WriteLine(date1.ToUniversalTime().ToString("r"));
// Displays Thu, 10 Apr 2008 13:30:00 GMT                       
Console.WriteLine(dateOffset.ToUniversalTime().ToString("r"));
// Displays Thu, 10 Apr 2008 13:30:00 GMT  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Dim dateOffset As New DateTimeOffset(date1, TimeZoneInfo.Local.GetUtcOFfset(date1))
Console.WriteLine(date1.ToUniversalTime.ToString("r"))
' Displays Thu, 10 Apr 2008 13:30:00 GMT                       
Console.WriteLine(dateOffset.ToUniversalTime.ToString("r"))
' Displays Thu, 10 Apr 2008 13:30:00 GMT
```

## <a name="the-sortable-s-format-specifier"></a>Identificatore di formato ordinabile ("s")

L'identificatore di formato standard "s" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.SortableDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern) corrente. Lo schema riflette uno standard definito (ISO 8601) e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "yyyy'-'MM'-'dd'T'HH':'mm':'ss".

L'identificatore di formato "s" ha lo scopo di produrre stringhe di risultati organizzate coerentemente in ordine crescente o decrescente, in base ai valori di data e ora. Di conseguenza, anche se l'identificatore di formato standard "s" rappresenta un valore di data e ora in un formato coerente, l'operazione di formattazione non modifica il valore dell'oggetto data e ora che viene formattato per riflettere la proprietà [DateTime.Kind](xref:System.DateTime.Kind) o il valore [DateTimeOffset.Offset](xref:System.DateTimeOffset.Offset) corrispondente. Ad esempio, le stringhe di risultati generate dalla formattazione dei valori di data e ora 2014-11-15T18:32:17+00:00 e 2014-11-15T18:32:17+08:00 sono identiche. 

Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti. 

Nell'esempio seguente viene usato l'identificatore di formato "s" per visualizzare una serie di valori [DateTime](xref:System.DateTime) e un valore [DateTimeOffset](xref:System.DateTimeOffset) in un sistema nel fuso orario Pacifico (Stati Uniti).

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("s"));
// Displays 2008-04-10T06:30:00
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("s"))
' Displays 2008-04-10T06:30:00 
```

## <a name="the-short-time-t-format-specifier"></a>Identificatore di formato di ora breve ("t")

L'identificatore di formato standard "t" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "HH:mm".

La stringa risultato è influenzata dalle informazioni sulla formattazione di un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà [DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[DateTimeFormatInfo.ShortTimePattern](xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern) | Definisce il formato del componente relativo all'ora della stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "t" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("t", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 6:30 AM                        
Console.WriteLine(date1.ToString("t", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays 6:30  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("t", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 6:30 AM                        
Console.WriteLine(date1.ToString("t", _
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays 6:30
```

## <a name="the-long-time-t-format-specifier"></a>Identificatore di formato di ora estesa ("T")

L'identificatore di formato standard "T" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) di una specifica impostazione cultura. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "HH:mm:ss".

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà [DateTimeFormatInfo.LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[LongTimePattern](xref:System.Globalization.DateTimeFormatInfo.LongTimePattern) | Definisce il formato del componente relativo all'ora della stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

Nell'esempio seguente viene usato l'identificatore di formato "T" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("T", 
                  CultureInfo.CreateSpecificCulture("en-us")));
// Displays 6:30:00 AM                       
Console.WriteLine(date1.ToString("T", 
                  CultureInfo.CreateSpecificCulture("es-ES")));
// Displays 6:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("T", _
                  CultureInfo.CreateSpecificCulture("en-us")))
' Displays 6:30:00 AM                       
Console.WriteLine(date1.ToString("T", _
                  CultureInfo.CreateSpecificCulture("es-ES")))
' Displays 6:30:00 
```

## <a name="the-universal-sortable-u-format-specifier"></a>Identificatore di formato ordinabile universale ("u")

L'identificatore di formato standard "u" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.UniversalSortableDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern) corrente. Lo schema riflette uno standard definito e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "yyyy'-'MM'-'dd HH':'mm':'ss'Z". Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti. 

Sebbene la stringa di risultato debba esprimere un'ora in formato UTC (Coordinated Universal Time), non viene eseguita alcuna conversione del valore [DateTime](xref:System.DateTime) originale durante l'operazione di formattazione. È pertanto necessario convertire un valore [DateTime](xref:System.DateTime) in formato UTC chiamando il metodo [DateTime.ToUniversalTime](xref:System.DateTime.ToUniversalTime) prima di formattarlo. Al contrario, i valori [DateTimeOffset](xref:System.DateTimeOffset) eseguono questa conversione automaticamente; non è necessario chiamare il metodo [DateTimeOffset.ToUniversalTime](xref:System.DateTimeOffset.ToUniversalTime) prima dell'operazione di formattazione.   

Nell'esempio seguente viene usato l'identificatore di formato "u" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToUniversalTime().ToString("u"));
// Displays 2008-04-10 13:30:00Z
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToUniversalTime.ToString("u"))
' Displays 2008-04-10 13:30:00Z                       
```

## <a name="the-universal-full-u-format-specifier"></a>Identificatore di formato completo universale ("U")

L'identificatore di formato standard "U" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) di una specifica impostazione cultura. Lo schema corrisponde a quello di "F". Il valore [DateTime](xref:System.DateTime), tuttavia, viene convertito automaticamente in formato UTC prima di essere formattato.

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà [FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.

Proprietà | Descrizione
-------- | -----------
[FullDateTimePattern](xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern) | Definisce il formato complessivo della stringa di risultato.
[DayNames](xref:System.Globalization.DateTimeFormatInfo.DayNames) | Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.
[AMDesignator](xref:System.Globalization.DateTimeFormatInfo.AMDesignator) | Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.
[PMDesignator](xref:System.Globalization.DateTimeFormatInfo.PMDesignator) | Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.

L'identificatore di formato "U" non è supportato per il tipo [DateTimeOffset](xref:System.DateTimeOffset) e genera una [FormatException](xref:System.FormatException) se viene usato per formattare un valore [DateTimeOffset](xref:System.DateTimeOffset).

Nell'esempio seguente viene usato l'identificatore di formato "U" per visualizzare un valore di data e ora.

``` csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("U", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays Thursday, April 10, 2008 1:30:00 PM                       
Console.WriteLine(date1.ToString("U", 
                  CultureInfo.CreateSpecificCulture("sv-FI")));
// Displays den 10 april 2008 13:30:00  
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("U", CultureInfo.CreateSpecificCulture("en-US")))
' Displays Thursday, April 10, 2008 1:30:00 PM                       
Console.WriteLine(date1.ToString("U", CultureInfo.CreateSpecificCulture("sv-FI")))
' Displays den 10 april 2008 13:30:00                       
```

## <a name="the-year-month-y-y-format-specifier"></a>Identificatore di formato di mese e anno ("Y", "y")

L'identificatore di formato standard "Y" o "y" rappresenta una stringa di formato data e ora personalizzato definita dalla proprietà [DateTimeFormatInfo.YearMonthPattern](xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern) di una specifica impostazione cultura. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "yyyy MMMM".

Nella tabella seguente sono elencate le proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che consentono di controllare la formattazione della stringa restituita.

Proprietà | Descrizione
-------- | -----------
[YearMonthPattern](xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern) | Definisce il formato complessivo della stringa di risultato.
[MonthNames](xref:System.Globalization.DateTimeFormatInfo.MonthNames) | Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.

Nell'esempio seguente viene usato l'identificatore di formato "Y" per visualizzare un valore di data e ora.

```csharp
DateTime date1 = new DateTime(2008, 4, 10, 6, 30, 0);
Console.WriteLine(date1.ToString("Y", 
                  CultureInfo.CreateSpecificCulture("en-US")));
// Displays April, 2008                       
Console.WriteLine(date1.ToString("y", 
                  CultureInfo.CreateSpecificCulture("af-ZA")));
// Displays April 2008 
```

```vb
Dim date1 As Date = #4/10/2008 6:30AM#
Console.WriteLine(date1.ToString("Y", CultureInfo.CreateSpecificCulture("en-US")))
' Displays April, 2008                       
Console.WriteLine(date1.ToString("y", CultureInfo.CreateSpecificCulture("af-ZA")))
' Displays April 2008
```                       

## <a name="notes"></a>Note

### <a name="datetimeformatinfo-properties"></a>Proprietà DateTimeFormatInfo

La formattazione è influenzata dalle proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrente, che viene specificato in modo implicito dalle impostazioni cultura del thread corrente o in modo esplicito dal parametro [IFormatProvider](xref:System.IFormatProvider) del metodo che chiama la formattazione. Per il parametro [IFormatProvider](xref:System.IFormatProvider) l'applicazione deve specificare un oggetto [CultureInfo](xref:System.Globalization.CultureInfo) che rappresenta un tipo di impostazioni cultura o un oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) che rappresenta le convenzioni di formattazione di data e ora di una specifica impostazione cultura. Molti degli identificatori di formato data e ora standard sono alias di schemi di formattazione definiti dalle proprietà dell'oggetto [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrente. Nell'applicazione può quindi essere modificato il risultato prodotto da alcuni identificatori di formato data e ora personalizzati standard modificando gli schemi di formato di data e ora corrispondenti della proprietà [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) corrispondente.

## <a name="see-also"></a>Vedere anche

[Formattazione di tipi](formatting-types.md)

[Stringhe di formato di data e ora personalizzato](custom-datetime.md)




<!--HONumber=Nov16_HO1-->


