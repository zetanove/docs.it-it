---
title: "Stringhe di formato di data e ora standard | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "date [.NET Framework], formattazione"
  - "identificatori di formato, data e ora"
  - "identificatori di formato, data e ora standard"
  - "stringhe di formato"
  - "formattazione [.NET Framework], date"
  - "formattazione [.NET Framework], time"
  - "stringhe di formato di data e ora standard"
  - "stringhe di formato di data e ora standard"
  - "stringhe di formato standard, data e ora"
  - "ora [.NET Framework], formattazione"
ms.assetid: bb79761a-ca08-44ee-b142-b06b3e2fc22b
caps.latest.revision: 92
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 90
---
# Stringhe di formato di data e ora standard
Una stringa di formato data e ora standard usa un singolo identificatore di formato per definire la rappresentazione di testo di un valore di data e ora. Le stringhe di formato di data e ora contenenti più caratteri, inclusi gli spazi, vengono interpretate come stringhe di formato di data e ora personalizzate. Per altre informazioni, vedere [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md). Una stringa di formato standard o personalizzata può essere usata in due modi:  
  
-   Per definire la stringa risultante da un'operazione di formattazione.  
  
-   Per definire la rappresentazione di testo di un valore di data e ora che può essere convertito in un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> da un'operazione di analisi.  
  
 Le stringhe di formato data e ora standard possono essere usate con i valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
> [!TIP]
>  È possibile scaricare l'[utilità di formattazione](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d), un'applicazione che consente di applicare stringhe di formato a valori numerici o di data e ora e di visualizzare la stringa di risultato.  
  
<a name="table"></a> Nella tabella seguente vengono descritti gli identificatori di formato di data e ora standard. Se non specificato diversamente, un identificatore di formato di data e ora standard specifico genera una rappresentazione di stringa identica, indipendentemente dal fatto che venga usato con un valore <xref:System.DateTime> o con un valore <xref:System.DateTimeOffset>. Per altre informazioni sull'uso di stringhe di formato di data e ora standard, vedere la sezione [Note](#Notes).  
  
|Identificatore di formato|Descrizione|Esempi|  
|-------------------------------|-----------------|------------|  
|"d"|Schema di data breve.<br /><br /> Altre informazioni:[Identificatore di formato di data breve \("d"\)](#ShortDate).|2009\-06\-15T13:45:30 \-\> 6\/15\/2009 \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15\/06\/2009 \(fr\-FR\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 2009\/06\/15 \(ja\-JP\)|  
|"D"|Schema di data estesa.<br /><br /> Altre informazioni: [Identificatore di formato di data estesa \("D"\)](#LongDate).|2009\-06\-15T13:45:30 \-\> Monday, June 15, 2009 \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15 июня 2009 г. \(ru\-RU\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Montag, 15. Juni 2009 \(de\-DE\)|  
|"f"|Schema di data\/ora completa \(ora breve\).<br /><br /> Altre informazioni: [Identificatore di formato di ora breve e data completa \("f"\)](#FullDateShortTime).|2009\-06\-15T13:45:30 \-\> Monday, June 15, 2009 1:45 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> den 15 juni 2009 13:45 \(sv\-SE\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Δευτέρα, 15 Ιουνίου 2009 1:45 μμ \(el\-GR\)|  
|"F"|Schema di data\/ora completa \(ora estesa\).<br /><br /> Altre informazioni: [Identificatore di formato di ora estesa e data completa \("F"\)](#FullDateLongTime).|2009\-06\-15T13:45:30 \-\> Monday, June 15, 2009 1:45:30 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> den 15 juni 2009 13:45:30 \(sv\-SE\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Δευτέρα, 15 Ιουνίου 2009 1:45:30 μμ \(el\-GR\)|  
|"g"|Schema di data\/ora generale \(ora breve\).<br /><br /> Altre informazioni: [Identificatore di formato di ora breve e data generale \("g"\)](#GeneralDateShortTime).|2009\-06\-15T13:45:30 \-\> 6\/15\/2009 1:45 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15\/06\/2009 13:45 \(es\-ES\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 2009\/6\/15 13:45 \(zh\-CN\)|  
|"G"|Schema di data\/ora generale \(ora estesa\).<br /><br /> Altre informazioni: [Identificatore di formato di ora estesa e data generale \("G"\)](#GeneralDateLongTime).|2009\-06\-15T13:45:30 \-\> 6\/15\/2009 1:45:30 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15\/06\/2009 13:45:30 \(es\-ES\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 2009\/6\/15 13:45:30 \(zh\-CN\)|  
|"M", "m"|Schema di mese\/giorno.<br /><br /> Altre informazioni: [Identificatore di formato di mese \("M", "m"\)](#MonthDay).|2009\-06\-15T13:45:30 \-\> June 15 \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15. juni \(da\-DK\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 15 Juni \(id\-ID\)|  
|"O", "o"|Schema di data\/ora di round trip.<br /><br /> Altre informazioni: [Identificatore di formato di round trip \("O", "o"\)](#Roundtrip).|Valori <xref:System.DateTime>:<br /><br /> 2009\-06\-15T13:45:30 \(DateTimeKind.Local\) \-\-\> 2009\-06\-15T13:45:30.0000000\-07:00<br /><br /> 2009\-06\-15T13:45:30 \(DateTimeKind.Utc\) \-\-\> 2009\-06\-15T13:45:30.0000000Z<br /><br /> 2009\-06\-15T13:45:30 \(DateTimeKind.Unspecified\) \-\-\> 2009\-06\-15T13:45:30.0000000<br /><br /> Valori <xref:System.DateTimeOffset>:<br /><br /> 2009\-06\-15T13:45:30\-07:00 \-\-\> 2009\-06\-15T13:45:30.0000000\-07:00|  
|"R", "r"|Schema RFC1123.<br /><br /> Altre informazioni: [Identificatore di formato RFC1123 \("R", "r"\)](#RFC1123).|2009\-06\-15T13:45:30 \-\> Mon, 15 Jun 2009 20:45:30 GMT|  
|"s"|Schema di data\/ora ordinabile.<br /><br /> Altre informazioni: [Identificatore di formato ordinabile \("s"\)](#Sortable).|2009\-06\-15T13:45:30 \(DateTimeKind.Local\) \-\> 2009\-06\-15T13:45:30<br /><br /> 2009\-06\-15T13:45:30 \(DateTimeKind.Utc\) \-\> 2009\-06\-15T13:45:30|  
|"t"|Schema di ora breve.<br /><br /> Altre informazioni: [Identificatore di formato di ora breve \("t"\)](#ShortTime).|2009\-06\-15T13:45:30 \-\> 1:45 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 13:45 \(hr\-HR\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 01:45 م \(ar\-EG\)|  
|"T"|Schema di ora estesa.<br /><br /> Altre informazioni: [Identificatore di formato di ora estesa \("T"\)](#LongTime).|2009\-06\-15T13:45:30 \-\> 1:45:30 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 13:45:30 \(hr\-HR\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 01:45:30 م \(ar\-EG\)|  
|"u"|Schema di data\/ora ordinabile universale.<br /><br /> Altre informazioni: [Identificatore di formato ordinabile universale \("u"\)](#UniversalSortable).|Con un valore <xref:System.DateTime>: 2009\-06\-15T13:45:30 \-\> 2009\-06\-15 13:45:30Z<br /><br /> Con un valore <xref:System.DateTimeOffset>: 2009\-06\-15T13:45:30 \-\> 2009\-06\-15 20:45:30Z|  
|"U"|Schema di data\/ora completa universale.<br /><br /> Altre informazioni: [Identificatore di formato completo universale \("U"\)](#UniversalFull).|2009\-06\-15T13:45:30 \-\> Monday, June 15, 2009 8:45:30 PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> den 15 juni 2009 20:45:30 \(sv\-SE\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Δευτέρα, 15 Ιουνίου 2009 8:45:30 μμ \(el\-GR\)|  
|"Y", "y"|Schema di mese e anno.<br /><br /> Altre informazioni: [Identificatore di formato di mese e anno \("Y"\)](#YearMonth).|2009\-06\-15T13:45:30 \-\> June, 2009 \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> juni 2009 \(da\-DK\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Juni 2009 \(id\-ID\)|  
|Qualsiasi altro carattere singolo|Identificatore sconosciuto.|Genera un evento <xref:System.FormatException> in fase di esecuzione.|  
  
## Funzionamento delle stringhe di formato standard  
 In un'operazione di formattazione, una stringa di formato standard è semplicemente un alias per una stringa di formato personalizzata. Il vantaggio dell'uso di un alias per fare riferimento a una stringa di formato personalizzata consiste nel fatto che, sebbene l'alias sia invariante, la stringa di formato personalizzata può variare. Questo aspetto è importante perché le rappresentazioni di stringa di valori di data e ora variano in genere in base alle impostazioni cultura. La stringa di formato standard "d" indica, ad esempio, che un valore di data e ora deve essere visualizzato usando uno schema di data breve. Per le impostazioni cultura invarianti questo schema è "MM\/dd\/yyyy". Per le impostazioni cultura fr\-FR questo schema è "dd\/MM\/yyyy". Per le impostazioni cultura ja\-JP questo schema è "yyyy\/MM\/dd".  
  
 Se in un'operazione di formattazione viene eseguito il mapping di una stringa di formato standard alla stringa di formato personalizzata di impostazioni cultura particolari, nell'applicazione possono essere definite le impostazioni cultura specifiche le cui stringhe di formato personalizzate vengono usate in una di queste modalità:  
  
-   È possibile usare le impostazioni cultura predefinite, o correnti. Nell'esempio seguente viene visualizzata una data usando il formato di data breve delle impostazioni cultura correnti. In questo caso le impostazioni cultura correnti sono en\-US.  
  
     [!code-csharp[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#1)]
     [!code-vb[System.DateTime.Conceptual.Formatting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#1)]  
  
-   È possibile passare un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura di cui deve essere usata la formattazione a un metodo con un parametro <xref:System.IFormatProvider>. Nell'esempio seguente viene visualizzata una data usando il formato di data breve delle impostazioni cultura pt\-BR.  
  
     [!code-csharp[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#2)]
     [!code-vb[System.DateTime.Conceptual.Formatting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#2)]  
  
-   È possibile passare un oggetto <xref:System.Globalization.DateTimeFormatInfo> che fornisce informazioni di formattazione a un metodo con un parametro <xref:System.IFormatProvider>. Nell'esempio seguente viene visualizzata una data usndo il formato di data breve da un oggetto <xref:System.Globalization.DateTimeFormatInfo> per le impostazioni cultura hr\-HR.  
  
     [!code-csharp[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/cs/StandardFormats1.cs#3)]
     [!code-vb[System.DateTime.Conceptual.Formatting#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTime.Conceptual.Formatting/vb/StandardFormats1.vb#3)]  
  
> [!NOTE]
>  Per informazioni sulla personalizzazione delle stringhe o dei modelli usati nella formattazione di data e ora, vedere l'argomento relativo alla classe <xref:System.Globalization.NumberFormatInfo>.  
  
 In alcuni casi la stringa di formato standard serve come una pratica abbreviazione per una stringa di formato personalizzata più lunga, che è invariante. In questa categoria rientrano quattro stringhe di formato standard: "O" \(o "o"\), "R" \(o "r"\), "s" e "u". Queste stringhe corrispondono a stringhe di formato personalizzate definite dalle impostazioni cultura invarianti. Producono rappresentazioni di stringa di valori di data e ora che dovranno essere identiche nelle diverse impostazioni cultura. Nella tabella seguente vengono fornite informazioni su queste quattro stringhe di formato di data e ora standard.  
  
|Stringa di formato standard|Definita dalla proprietà DateTimeFormatInfo.InvariantInfo|Stringa di formato personalizzata|  
|---------------------------------|---------------------------------------------------------------|---------------------------------------|  
|"O" o "o"|Nessuno|yyyy'\-'MM'\-'dd'T'HH':'mm':'ss'.'fffffffzz|  
|"R" o "r"|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|ddd, dd MMM yyyy HH':'mm':'ss 'GMT'|  
|"s"|<xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A>|yyyy'\-'MM'\-'dd'T'HH':'mm':'ss|  
|"u"|<xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>|yyyy'\-'MM'\-'dd HH':'mm':'ss'Z'|  
  
 Le stringhe di formato standard possono anche essere usate nelle operazioni di analisi con i metodi <xref:System.DateTime.ParseExact%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=fullName>, che richiedono che una stringa di input sia esattamente conforme a un modello specifico affinché l'operazione di analisi abbia esito positivo. Poiché viene eseguito il mapping di molte stringhe di formato standard a più stringhe di formato personalizzate, un valore di data e ora può essere rappresentato in diversi formati ma l'operazione di analisi verrà tuttavia eseguita correttamente. È possibile determinare la stringa o le stringhe di formato personalizzate che corrispondono a una stringa di formato standard chiamando il metodo <xref:System.Globalization.DateTimeFormatInfo.GetAllDateTimePatterns%28System.Char%29?displayProperty=fullName>. Nell'esempio seguente vengono visualizzate le stringhe di formato personalizzate che eseguono il mapping alla stringa di formato standard "d" \(modello di data breve\).  
  
 [!code-csharp[Formatting.DateAndTime.Standard#17](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/stdandparsing1.cs#17)]
 [!code-vb[Formatting.DateAndTime.Standard#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/stdandparsing1.vb#17)]  
  
 Nelle sezioni seguenti vengono descritti gli identificatori di formato standard per i valori <xref:System.DateTime> e <xref:System.DateTimeOffset>.  
  
<a name="ShortDate"></a>   
## Identificatore di formato di data breve \("d"\)  
 L'identificatore di formato standard "d" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=fullName> di impostazioni cultura specifiche. La stringa di formato personalizzata restituita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A> della lingua inglese è, ad esempio, "MM\/dd\/yyyy".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Definisce la stringa che separa i componenti relativi ad anno, mese e giorno di una data.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "d" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#1)]
 [!code-vb[Formatting.DateAndTime.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#1)]  
  
 [Torna alla tabella](#table)  
  
<a name="LongDate"></a>   
## Identificatore di formato di data estesa \("D"\)  
 L'identificatore di formato standard "D" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=fullName> corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "dddd, dd MMMM yyyy".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "D" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#2)]  
  
 [Torna alla tabella](#table)  
  
<a name="FullDateShortTime"></a>   
## Identificatore di formato di ora breve e data completa \("f"\)  
 L'identificatore di formato standard "f" rappresenta una combinazione degli schemi di data estesa \("D"\) e ora breve \("t"\), separati da uno spazio.  
  
 La stringa di risultato è influenzata dalle informazioni sulla formattazione di un oggetto <xref:System.Globalization.DateTimeFormatInfo> specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=fullName> e <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=fullName> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A>|Definisce il formato del componente relativo alla data della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definisce il formato del componente relativo all'ora della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "f" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#3)]  
  
 [Torna alla tabella](#table)  
  
<a name="FullDateLongTime"></a>   
## Identificatore di formato di ora estesa e data completa \("F"\)  
 L'identificatore di formato standard "F" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=fullName> corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "dddd, dd MMMM yyyy HH:mm:ss".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "F" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#4)]  
  
 [Torna alla tabella](#table)  
  
<a name="GeneralDateShortTime"></a>   
## Identificatore di formato di ora breve e data generale \("g"\)  
 L'identificatore di formato standard "g" rappresenta una combinazione degli schemi di data breve \("d"\) e ora breve \("t"\), separati da uno spazio.  
  
 La stringa di risultato è influenzata dalle informazioni sulla formattazione di un oggetto <xref:System.Globalization.DateTimeFormatInfo> specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=fullName> e <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=fullName> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definisce il formato del componente relativo alla data della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definisce il formato del componente relativo all'ora della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Definisce la stringa che separa i componenti relativi ad anno, mese e giorno di una data.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "g" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="GeneralDateLongTime"></a>   
## Identificatore di formato di ora estesa e data generale \("G"\)  
 L'identificatore di formato standard "G" rappresenta una combinazione degli schemi di data breve \("d"\) e ora estesa \("T"\), separati da uno spazio.  
  
 La stringa di risultato è influenzata dalle informazioni sulla formattazione di un oggetto <xref:System.Globalization.DateTimeFormatInfo> specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalle proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=fullName> e <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=fullName> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A>|Definisce il formato del componente relativo alla data della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|Definisce il formato del componente relativo all'ora della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A>|Definisce la stringa che separa i componenti relativi ad anno, mese e giorno di una data.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "G" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#6)]
 [!code-vb[Formatting.DateAndTime.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#6)]  
  
 [Torna alla tabella](#table)  
  
<a name="MonthDay"></a>   
## Identificatore di formato di mese \("M", "m"\)  
 L'identificatore di formato standard "M" o "m" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A?displayProperty=fullName> corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "MMMM dd".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthDayPattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "m" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="Roundtrip"></a>   
## Identificatore di formato di round trip \("O", "o"\)  
 L'identificatore di formato standard "O" o "o" rappresenta una stringa di formato di data e ora personalizzata con uno schema che mantiene le informazioni sul fuso orario e crea una stringa di risultato conforme allo standard ISO 8601. Per i valori <xref:System.DateTime>, questo identificatore di formato è progettato per mantenere valori di data e ora insieme alla proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> nel testo. È possibile analizzare di nuovo la stringa formattata usando il metodo <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=fullName> o <xref:System.DateTime.ParseExact%2A?displayProperty=fullName> se il parametro `styles` è impostato su <xref:System.Globalization.DateTimeStyles?displayProperty=fullName>.  
  
 L'identificatore di formato standard "O" o "o" corrisponde alla stringa di formato personalizzata "yyyy'\-'MM'\-'dd'T'HH':'mm':'ss'.'fffffffK" per valori <xref:System.DateTime> e alla stringa di formato personalizzata "yyyy'\-'MM'\-'dd'T'HH':'mm':'ss'.'fffffffzzz" per valori <xref:System.DateTimeOffset>. In questa stringa le coppie di virgolette singole che delimitano singoli caratteri, ad esempio trattini, due punti e la lettera "T", indicano che il singolo carattere è un valore letterale che non può essere modificato. Gli apostrofi non vengono visualizzati nella stringa di output.  
  
 L'identificatore di formato standard "O" o "o" \(e la stringa di formato personalizzata "yyyy'\-'MM'\-'dd'T'HH':'mm':'ss'.'fffffffK"\) sfrutta i tre modi in cui lo standard ISO 8601 rappresenta le informazioni sul fuso orario per preservare la proprietà <xref:System.DateTime.Kind%2A> dei valori <xref:System.DateTime>:  
  
-   Il componente relativo al fuso orario dei valori di data e ora <xref:System.DateTimeKind?displayProperty=fullName> è un offset rispetto all'ora UTC \(ad esempio \+01:00, \-07:00\). Anche tutti i valori <xref:System.DateTimeOffset> sono rappresentati in questo formato.  
  
-   Il componente relativo al fuso orario dei valori di data e ora <xref:System.DateTimeKind?displayProperty=fullName> usa "Z" \(che sta per zero offset\) per rappresentare l'ora UTC.  
  
-   I valori di data e ora <xref:System.DateTimeKind?displayProperty=fullName> non dispongono di informazioni sul fuso orario.  
  
 Poiché l'identificatore di formato standard O" o "o" è conforme a uno standard internazionale, l'operazione di formattazione o analisi che usa l'identificatore usa sempre le impostazioni cultura invarianti e il calendario gregoriano.  
  
 Le stringhe passate ai metodi `Parse`, `TryParse`, `ParseExact` e `TryParseExact` di <xref:System.DateTime> e <xref:System.DateTimeOffset> possono essere analizzate usando l'identificatore di formato "O" o "o" se sono in uno di questi formati. Nel caso degli oggetti <xref:System.DateTime>, l'overload di analisi chiamato deve anche includere un parametro `styles` con un valore <xref:System.Globalization.DateTimeStyles?displayProperty=fullName>. Tenere presente che se si chiama un metodo di analisi con la stringa di formato personalizzata che corrisponde all'identificatore di formato "O" o "o", non si otterranno gli stessi risultati di "O" o "o". Il motivo è che i metodi di analisi che usano una stringa di formato personalizzata non possono analizzare la rappresentazione in formato stringa di valori di data e ora in cui manca un componente di fuso orario o che usano "Z" per indicare l'ora UTC.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "o" per visualizzare una serie di valori <xref:System.DateTime> e un valore <xref:System.DateTimeOffset> in un sistema nel fuso orario Pacifico \(Stati Uniti\).  
  
 [!code-csharp[Formatting.DateAndTime.Standard#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/o1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Standard#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/o1.vb#8)]  
  
 Nell'esempio seguente viene usato l'identificatore di formato "o" per creare una stringa formattata, quindi viene ripristinato il valore di data e ora originale chiamando un metodo `Parse` di data e ora.  
  
 [!code-csharp[Formatting.DateandTime.Standard#16](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Roundtrip1.cs#16)]
 [!code-vb[Formatting.DateandTime.Standard#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/RoundTrip1.vb#16)]  
  
 [Torna alla tabella](#table)  
  
<a name="RFC1123"></a>   
## Identificatore di formato RFC1123 \("R", "r"\)  
 L'identificatore di formato standard "R" o "r" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A?displayProperty=fullName> corrente. Lo schema riflette uno standard definito e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "ddd, dd MMM yyyy HH':'mm':'ss 'GMT". Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti.  
  
 La stringa di risultato è influenzata dalle proprietà seguenti dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.InvariantInfo%2A?displayProperty=fullName> che rappresenta la lingua inglese.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.RFC1123Pattern%2A>|Definisce il formato della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A>|Definisce i nomi dei giorni abbreviati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames%2A>|Definisce i nomi dei mesi abbreviati che possono essere visualizzati nella stringa di risultato.|  
  
 Anche se lo standard RFC 1123 esprime un'ora in formato UTC \(Coordinated Universal Time\), l'operazione di formattazione non comporta la modifica del valore dell'oggetto <xref:System.DateTime> che viene formattato. È pertanto necessario convertire il valore <xref:System.DateTime> in formato UTC chiamando il metodo <xref:System.DateTime.ToUniversalTime%2A?displayProperty=fullName> prima di eseguire l'operazione di formattazione. Al contrario, i valori <xref:System.DateTimeOffset> eseguono questa conversione automaticamente; non è necessario chiamare il metodo <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=fullName> prima dell'operazione di formattazione.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "r" per visualizzare un valore <xref:System.DateTime> e un valore <xref:System.DateTimeOffset> in un sistema nel fuso orario Pacifico \(Stati Uniti\).  
  
 [!code-csharp[Formatting.DateAndTime.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#9)]
 [!code-vb[Formatting.DateAndTime.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#9)]  
  
 [Torna alla tabella](#table)  
  
<a name="Sortable"></a>   
## Identificatore di formato ordinabile \("s"\)  
 L'identificatore di formato standard "s" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.SortableDateTimePattern%2A?displayProperty=fullName> corrente. Lo schema riflette uno standard definito \(ISO 8601\) e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "yyyy'\-'MM'\-'dd'T'HH':'mm':'ss".  
  
 L'identificatore di formato "s" ha lo scopo di produrre stringhe di risultati organizzate coerentemente in ordine crescente o decrescente, in base ai valori di data e ora. Di conseguenza, anche se l'identificatore di formato standard "s" rappresenta un valore di data e ora in un formato coerente, l'operazione di formattazione non modifica il valore dell'oggetto data e ora che viene formattato per riflettere la proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> o il valore <xref:System.DateTimeOffset.Offset%2A?displayProperty=fullName> corrispondente. Ad esempio, le stringhe di risultati generate dalla formattazione dei valori di data e ora 2014\-11\-15T18:32:17\+00:00 e 2014\-11\-15T18:32:17\+08:00 sono identiche.  
  
 Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "s" per visualizzare un valore <xref:System.DateTime> e un valore <xref:System.DateTimeOffset> in un sistema nel fuso orario Pacifico \(Stati Uniti\).  
  
 [!code-csharp[Formatting.DateAndTime.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#10)]
 [!code-vb[Formatting.DateAndTime.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#10)]  
  
 [Torna alla tabella](#table)  
  
<a name="ShortTime"></a>   
## Identificatore di formato di ora breve \("t"\)  
 L'identificatore di formato standard "t" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=fullName> corrente. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "HH:mm".  
  
 La stringa di risultato è influenzata dalle informazioni sulla formattazione di un oggetto <xref:System.Globalization.DateTimeFormatInfo> specifico. Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A?displayProperty=fullName> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.ShortTimePattern%2A>|Definisce il formato del componente relativo all'ora della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "t" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#11)]
 [!code-vb[Formatting.DateAndTime.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#11)]  
  
 [Torna alla tabella](#table)  
  
<a name="LongTime"></a>   
## Identificatore di formato di ora estesa \("T"\)  
 L'identificatore di formato standard "T" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=fullName> di impostazioni cultura specifiche. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "HH:mm:ss".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A?displayProperty=fullName> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.LongTimePattern%2A>|Definisce il formato del componente relativo all'ora della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "T" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#12)]
 [!code-vb[Formatting.DateAndTime.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#12)]  
  
 [Torna alla tabella](#table)  
  
<a name="UniversalSortable"></a>   
## Identificatore di formato ordinabile universale \("u"\)  
 L'identificatore di formato standard "u" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A?displayProperty=fullName> corrente. Lo schema riflette uno standard definito e la proprietà è di sola lettura. Pertanto sarà sempre lo stesso, indipendentemente dalle impostazioni cultura usate o dal provider di formato fornito. La stringa di formato personalizzata è "yyyy'\-'MM'\-'dd HH':'mm':'ss'Z". Quando viene usato questo identificatore di formato standard, la formattazione o l'operazione di analisi usa sempre le impostazioni cultura invarianti.  
  
 Sebbene la stringa di risultato debba esprimere un'ora in formato UTC \(Coordinated Universal Time\), non viene eseguita alcuna conversione del valore <xref:System.DateTime> originale durante l'operazione di formattazione. È pertanto necessario convertire un valore <xref:System.DateTime> in formato UTC chiamando il metodo <xref:System.DateTime.ToUniversalTime%2A?displayProperty=fullName> prima di eseguire l'operazione di formattazione.  Al contrario, i valori <xref:System.DateTimeOffset> eseguono questa conversione automaticamente; non è necessario chiamare il metodo <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=fullName> prima dell'operazione di formattazione.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "u" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Standard#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="UniversalFull"></a>   
## Identificatore di formato completo universale \("U"\)  
 L'identificatore di formato standard "U" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=fullName> di impostazioni cultura specifiche. Lo schema corrisponde a quello di "F". Il valore <xref:System.DateTime>, tuttavia, viene convertito automaticamente in formato UTC prima di essere formattato.  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita. L'identificatore di formato personalizzato restituito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A> di alcune impostazioni cultura potrebbe non prevedere l'uso di tutte le proprietà.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.DayNames%2A>|Definisce i nomi dei giorni localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A>|Definisce la stringa che separa i componenti relativi a ora, minuti e secondi di un orario.|  
|<xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A>|Definisce la stringa che indica le ore da mezzanotte a prima di mezzogiorno in un orario in formato 12 ore.|  
|<xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A>|Definisce la stringa che indica le ore da mezzogiorno a prima di mezzanotte in un orario in formato 12 ore.|  
  
 L'identificatore di formato "U" non è supportato dal tipo <xref:System.DateTimeOffset> e genera un evento <xref:System.FormatException> se viene usato per formattare un valore <xref:System.DateTimeOffset>.  
  
 Nell'esempio seguente viene usato l'identificatore di formato "U" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Standard#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="YearMonth"></a>   
## Identificatore di formato di mese e anno \("Y", "y"\)  
 L'identificatore di formato standard "Y" o "y" rappresenta una stringa di formato di data e ora personalizzata definita dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A?displayProperty=fullName> di impostazioni cultura specifiche. La stringa di formato personalizzata per le impostazioni cultura invarianti ad esempio è "yyyy MMMM".  
  
 Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> che consentono di controllare la formattazione della stringa restituita.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Globalization.DateTimeFormatInfo.YearMonthPattern%2A>|Definisce il formato complessivo della stringa di risultato.|  
|<xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>|Definisce i nomi dei mesi localizzati che possono essere visualizzati nella stringa di risultato.|  
  
 Nell'esempio seguente viene usato l'identificatore di formato "Y" per visualizzare un valore di data e ora.  
  
 [!code-csharp[Formatting.DateAndTime.Standard#15](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Standard/cs/Standard1.cs#15)]
 [!code-vb[Formatting.DateAndTime.Standard#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Standard/vb/Standard1.vb#15)]  
  
 [Torna alla tabella](#table)  
  
<a name="Notes"></a>   
## Note  
  
### Impostazioni del Pannello di controllo  
 Le impostazioni di **Opzioni internazionali e della lingua** nel Pannello di controllo influiscono sulla stringa risultato prodotta da un'operazione di formattazione. Queste impostazioni vengono usate per inizializzare l'oggetto <xref:System.Globalization.DateTimeFormatInfo> associato alle impostazioni cultura del thread corrente, che fornisce i valori usati per definire la formattazione. Computer con impostazioni diverse generano stringhe di risultato diverse.  
  
 Se inoltre viene usato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=fullName> per creare un'istanza di un nuovo oggetto <xref:System.Globalization.CultureInfo> che rappresenta le stesse impostazioni cultura delle impostazioni cultura del sistema correnti, le eventuali personalizzazioni definite tramite **Opzioni internazionali e della lingua** nel Pannello di controllo verranno applicate al nuovo oggetto <xref:System.Globalization.CultureInfo>. È possibile usare il costruttore di <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> per creare un oggetto <xref:System.Globalization.CultureInfo> che non rifletta le personalizzazioni di un sistema.  
  
### Proprietà DateTimeFormatInfo  
 La formattazione è influenzata dalle proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> corrente, che viene fornito in modo implicito dalle impostazioni cultura del thread correnti o in modo esplicito dal parametro <xref:System.IFormatProvider> del metodo che richiama la formattazione. Per il parametro <xref:System.IFormatProvider> l'applicazione deve specificare un oggetto <xref:System.Globalization.CultureInfo> che rappresenta un tipo di impostazioni cultura o un oggetto <xref:System.Globalization.DateTimeFormatInfo> che rappresenta le convenzioni di formattazione di data e ora di impostazioni cultura particolari. Molti degli identificatori di formato di data e ora standard sono alias di schemi di formattazione definiti dalle proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> corrente. Nell'applicazione può quindi essere modificato il risultato prodotto da alcuni identificatori di formato di data e ora personalizzati standard modificando gli schemi di formato di data e ora corrispondenti della proprietà <xref:System.Globalization.DateTimeFormatInfo> corrispondente.  
  
## Vedere anche  
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)   
 [Esempio: Utilità di formattazione in .NET Framework 4](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)