---
title: "Stringhe di formato di data e ora personalizzato | Microsoft Docs"
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
  - "stringhe di formato data e ora personalizzate"
  - "stringhe di formato di data e ora personalizzate"
  - "identificatori di formato, data e ora personalizzate"
  - "stringhe di formato"
  - "formattazione [.NET Framework], date"
  - "formattazione [.NET Framework], time"
ms.assetid: 98b374e3-0cc2-4c78-ab44-efb671d71984
caps.latest.revision: 79
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 77
---
# Stringhe di formato di data e ora personalizzato
Una stringa di formato di data e ora definisce la rappresentazione di testo di un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> risultante da un'operazione di formattazione. Può anche definire la rappresentazione di un valore di data e ora richiesto in un'operazione di analisi per convertire correttamente la stringa in una data e ora. Una stringa di formato personalizzata è costituita da uno o più identificatori di formato di data e ora personalizzati. Qualsiasi stringa diversa da una [stringa di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md) viene interpretata come stringa di formato di data e ora personalizzata.  
  
 Le stringhe di formato data e ora personalizzate possono essere usate sia con valori <xref:System.DateTime> sia con valori <xref:System.DateTimeOffset>.  
  
> [!TIP]
>  È possibile scaricare l'[utilità di formattazione](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d), un'applicazione che consente di applicare stringhe di formato a valori numerici o data e ora e di visualizzare la stringa di risultato.  
  
<a name="table"></a> Nelle operazioni di formattazione, le stringhe di formato di data e ora personalizzate possono essere usate con il metodo `ToString` di un'istanza di data e ora o con un metodo che supporta la formattazione composita. Nell'esempio seguente vengono illustrati entrambi gli usi.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#17](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/custandformatting1.cs#17)]
 [!code-vb[Formatting.DateAndTime.Custom#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/custandformatting1.vb#17)]  
  
 Nelle operazioni di analisi, le stringhe di formato di data e ora personalizzate possono essere usate con i metodi <xref:System.DateTime.ParseExact%2A?displayProperty=fullName>, <xref:System.DateTime.TryParseExact%2A?displayProperty=fullName>, <xref:System.DateTimeOffset.ParseExact%2A?displayProperty=fullName> e <xref:System.DateTimeOffset.TryParseExact%2A?displayProperty=fullName>. Questi metodi richiedono che una stringa di input sia esattamente conforme a un modello specifico affinché l'operazione di analisi abbia esito positivo. Nell'esempio seguente viene illustrata una chiamata al metodo <xref:System.DateTimeOffset.ParseExact%28System.String%2CSystem.String%2CSystem.IFormatProvider%29?displayProperty=fullName> per analizzare una data che deve includere un giorno, un mese e un anno a due cifre.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#18](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/custandparsing1.cs#18)]
 [!code-vb[Formatting.DateAndTime.Custom#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/custandparsing1.vb#18)]  
  
 Nella tabella seguente vengono descritti gli identificatori di formato data e ora personalizzati e viene visualizzata una stringa di risultato prodotta da ogni identificatore di formato. Per impostazione predefinita, le stringhe di risultato riflettono le convenzioni di formattazione delle impostazioni cultura en\-US. Se un identificatore di formato specifico produce una stringa di risultato localizzata, nell'esempio vengono anche indicate le impostazioni cultura alle quali si applica la stringa di risultato. Vedere la sezione Note per altre informazioni sull'uso di stringhe di formato di data e ora personalizzate.  
  
|Identificatore di formato|Descrizione|Esempi|  
|-------------------------------|-----------------|------------|  
|"d"|Giorno del mese, da 1 a 31.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "d"](#dSpecifier).|2009\-06\-01T13:45:30 \-\> 1<br /><br /> 2009\-06\-15T13:45:30 \-\> 15|  
|"dd"|Giorno del mese, da 01 a 31.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "dd"](#ddSpecifier).|2009\-06\-01T13:45:30 \-\> 01<br /><br /> 2009\-06\-15T13:45:30 \-\> 15|  
|"ddd"|Nome abbreviato del giorno della settimana.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ddd"](#dddSpecifier).|2009\-06\-15T13:45:30 \-\> Mon \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Пн \(ru\-RU\)<br /><br /> 2009\-06\-15T13:45:30 \-\> lun. \(fr\-FR\)|  
|"dddd"|Nome completo del giorno della settimana.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "dddd"](#ddddSpecifier).|2009\-06\-15T13:45:30 \-\> Monday \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> понедельник \(ru\-RU\)<br /><br /> 2009\-06\-15T13:45:30 \-\> lundi \(fr\-FR\)|  
|"f"|Decimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "f"](#fSpecifier).|2009\-06\-15T13:45:30.6170000 \-\> 6<br /><br /> 2009\-06\-15T13:45:30.05 \-\> 0|  
|"ff"|Centesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ff"](#ffSpecifier).|2009\-06\-15T13:45:30.6170000 \-\> 61<br /><br /> 2009\-06\-15T13:45:30.0050000 \-\> 00|  
|"fff"|Millisecondi in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fff"](#fffSpecifier).|6\/15\/2009 13:45:30.617 \-\> 617<br /><br /> 6\/15\/2009 13:45:30.0005 \-\> 000|  
|"ffff"|Decimillesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ffff"](#ffffSpecifier).|2009\-06\-15T13:45:30.6175000 \-\> 6175<br /><br /> 2009\-06\-15T13:45:30.0000500  \-\> 0000|  
|"fffff"|Centomillesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fffff"](#fffffSpecifier).|2009\-06\-15T13:45:30.6175400 \-\> 61754<br /><br /> 6\/15\/2009 13:45:30.000005 \-\> 00000|  
|"ffffff"|Milionesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ffffff"](#ffffffSpecifier).|2009\-06\-15T13:45:30.6175420 \-\> 617542<br /><br /> 2009\-06\-15T13:45:30.0000005 \-\> 000000|  
|"fffffff"|Decine di milionesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "fffffff"](#fffffffSpecifier).|2009\-06\-15T13:45:30.6175425 \-\> 6175425<br /><br /> 2009\-06\-15T13:45:30.0001150 \-\> 0001150|  
|"F"|Se diverso da zero, decimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "F"](#F_Specifier).|2009\-06\-15T13:45:30.6170000 \-\> 6<br /><br /> 2009\-06\-15T13:45:30.0500000 \-\> \(nessun output\)|  
|"FF"|Se diverso da zero, centesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FF"](#FF_Specifier).|2009\-06\-15T13:45:30.6170000 \-\> 61<br /><br /> 2009\-06\-15T13:45:30.0050000 \-\> \(nessun output\)|  
|"FFF"|Se diverso da zero, millisecondi in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFF"](#FFF_Specifier).|2009\-06\-15T13:45:30.6170000 \-\> 617<br /><br /> 2009\-06\-15T13:45:30.0005000 \-\> \(nessun output\)|  
|"FFFF"|Se diverso da zero, decimillesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFF"](#FFFF_Specifier).|2009\-06\-15T13:45:30.5275000 \-\> 5275<br /><br /> 2009\-06\-15T13:45:30.0000500 \-\> \(nessun output\)|  
|"FFFFF"|Se diverso da zero, centomillesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFF"](#FFFFF_Specifier).|2009\-06\-15T13:45:30.6175400 \-\> 61754<br /><br /> 2009\-06\-15T13:45:30.0000050 \-\> \(nessun output\)|  
|"FFFFFF"|Se diverso da zero, milionesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFFF"](#FFFFFF_Specifier).|2009\-06\-15T13:45:30.6175420 \-\> 617542<br /><br /> 2009\-06\-15T13:45:30.0000005 \-\> \(nessun output\)|  
|"FFFFFFF"|Se diverso da zero, decimilionesimi di secondo in un valore data e ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "FFFFFFF"](#FFFFFFF_Specifier).|2009\-06\-15T13:45:30.6175425 \-\> 6175425<br /><br /> 2009\-06\-15T13:45:30.0001150 \-\> 000115|  
|"g", "gg"|Periodo o era.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "g" o "gg"](#gSpecifier).|2009\-06\-15T13:45:30.6170000 \-\> A.D.|  
|"h"|Ora, usando un orario in formato 12 ore da 1 a 12.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "h"](#hSpecifier).|2009\-06\-15T01:45:30 \-\> 1<br /><br /> 2009\-06\-15T13:45:30 \-\> 1|  
|"hh"|Ora, usando un orario in formato 12 ore da 01 a 12.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "hh"](#hhSpecifier).|2009\-06\-15T01:45:30 \-\> 01<br /><br /> 2009\-06\-15T13:45:30 \-\> 01|  
|"H"|Ora, usando un orario in formato 24 ore da 0 a 23.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "H"](#H_Specifier).|2009\-06\-15T01:45:30 \-\> 1<br /><br /> 2009\-06\-15T13:45:30 \-\> 13|  
|"HH"|Ora, usando un orario in formato 24 ore da 00 a 23.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "HH"](#HH_Specifier).|2009\-06\-15T01:45:30 \-\> 01<br /><br /> 2009\-06\-15T13:45:30 \-\> 13|  
|"K"|Informazioni sul fuso orario.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "K"](#KSpecifier).|Con valori <xref:System.DateTime>:<br /><br /> 2009\-06\-15T13:45:30, tipo non specificato \-\><br /><br /> 2009\-06\-15T13:45:30, tipo UTC \-\> Z<br /><br /> 2009\-06\-15T13:45:30, tipo locale \-\> \-07:00 \(dipende dalle impostazioni del computer locale\)<br /><br /> Con valori <xref:System.DateTimeOffset>:<br /><br /> 2009\-06\-15T01:45:30\-07:00 \-\-\> \-07:00<br /><br /> 2009\-06\-15T08:45:30\+00:00 \-\-\> \+00:00|  
|"m"|Minuti, da 0 a 59.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "m"](#mSpecifier).|2009\-06\-15T01:09:30 \-\> 9<br /><br /> 2009\-06\-15T13:29:30 \-\> 29|  
|"mm"|Minuti, da 00 a 59.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "mm"](#mmSpecifier).|2009\-06\-15T01:09:30 \-\> 09<br /><br /> 2009\-06\-15T01:45:30 \-\> 45|  
|"M"|Mese, da 1 a 12.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "M"](#M_Specifier).|2009\-06\-15T13:45:30 \-\> 6|  
|"MM"|Mese, da 01 a 12.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "MM"](#MM_Specifier).|2009\-06\-15T13:45:30 \-\> 06|  
|"MMM"|Nome abbreviato del mese.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "MMM"](#MMM_Specifier).|2009\-06\-15T13:45:30 \-\> Jun \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> juin \(fr\-FR\)<br /><br /> 2009\-06\-15T13:45:30 \-\> Jun \(zu\-ZA\)|  
|"MMMM"|Nome completo del mese.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "MMMM"](#MMMM_Specifier).|2009\-06\-15T13:45:30 \-\> June \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> juni \(da\-DK\)<br /><br /> 2009\-06\-15T13:45:30 \-\> uJuni \(zu\-ZA\)|  
|"s"|Secondi, da 0 a 59.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "s"](#sSpecifier).|2009\-06\-15T13:45:09 \-\> 9|  
|"ss"|Secondi, da 00 a 59.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "ss"](#ssSpecifier).|2009\-06\-15T13:45:09 \-\> 09|  
|"t"|Primo carattere dell'indicatore AM\/PM.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "t"](#tSpecifier).|2009\-06\-15T13:45:30 \-\> P \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 午 \(ja\-JP\)<br /><br /> 2009\-06\-15T13:45:30 \-\>  \(fr\-FR\)|  
|"tt"|Indicatore AM\/PM.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "tt"](#ttSpecifier).|2009\-06\-15T13:45:30 \-\> PM \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> 午後 \(ja\-JP\)<br /><br /> 2009\-06\-15T13:45:30 \-\>  \(fr\-FR\)|  
|"y"|Anno, da 0 a 99.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "y"](#ySpecifier).|0001\-01\-01T00:00:00 \-\> 1<br /><br /> 0900\-01\-01T00:00:00 \-\> 0<br /><br /> 1900\-01\-01T00:00:00 \-\> 0<br /><br /> 2009\-06\-15T13:45:30 \-\> 9<br /><br /> 2019\-06\-15T13:45:30 \-\> 19|  
|"yy"|Anno, da 00 a 99.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "yy"](#yySpecifier).|0001\-01\-01T00:00:00 \-\> 01<br /><br /> 0900\-01\-01T00:00:00 \-\> 00<br /><br /> 1900\-01\-01T00:00:00 \-\> 00<br /><br /> 2019\-06\-15T13:45:30 \-\> 19|  
|"yyy"|Anno, con un minimo di tre cifre.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "yyy"](#yyySpecifier).|0001\-01\-01T00:00:00 \-\> 001<br /><br /> 0900\-01\-01T00:00:00 \-\> 900<br /><br /> 1900\-01\-01T00:00:00 \-\> 1900<br /><br /> 2009\-06\-15T13:45:30 \-\> 2009|  
|"yyyy"|Anno, come numero a quattro cifre.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "yyyy"](#yyyySpecifier).|0001\-01\-01T00:00:00 \-\> 0001<br /><br /> 0900\-01\-01T00:00:00 \-\> 0900<br /><br /> 1900\-01\-01T00:00:00 \-\> 1900<br /><br /> 2009\-06\-15T13:45:30 \-\> 2009|  
|"yyyyy"|Anno, come numero a cinque cifre.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "yyyyy"](#yyyyySpecifier).|0001\-01\-01T00:00:00 \-\> 00001<br /><br /> 2009\-06\-15T13:45:30 \-\> 02009|  
|"z"|Offset delle ore rispetto a UTC, senza zeri iniziali.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "z"](#zSpecifier).|2009\-06\-15T13:45:30\-07:00 \-\> \-7|  
|"zz"|Offset delle ore rispetto a UTC, con uno zero iniziale per un valore a una sola cifra.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "zz"](#zzSpecifier).|2009\-06\-15T13:45:30\-07:00 \-\> \-07|  
|"zzz"|Offset di ore e minuti rispetto a UTC.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "zzz"](#zzzSpecifier).|2009\-06\-15T13:45:30\-07:00 \-\> \-07:00|  
|":"|Separatore dell'ora.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato ":"](#timeSeparator).|2009\-06\-15T13:45:30 \-\> : \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> . \(it\-IT\)<br /><br /> 2009\-06\-15T13:45:30 \-\> : \(ja\-JP\)|  
|"\/"|Separatore di data.<br /><br /> Altre informazioni: [Identificatore di formato personalizzato "\/"](#dateSeparator).|2009\-06\-15T13:45:30 \-\> \/ \(en\-US\)<br /><br /> 2009\-06\-15T13:45:30 \-\> \- \(ar\-DZ\)<br /><br /> 2009\-06\-15T13:45:30 \-\> . \(tr\-TR\)|  
|"*string*"<br /><br /> '*string*'|Delimitatore di stringa letterale.|2009\-06\-15T13:45:30 \("arr:" h:m t\) \-\> arr: 1:45 P<br /><br /> 2009\-06\-15T13:45:30 \('arr:' h:m t\) \-\> arr: 1:45 P|  
|%|Definisce il carattere seguente come identificatore di formato personalizzato.<br /><br /> Altre informazioni: [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers).|2009\-06\-15T13:45:30 \(%h\) \-\> 1|  
|\\|Carattere di escape.|2009\-06\-15T13:45:30 \(h \\h\) \-\> 1 h|  
|Qualsiasi altro carattere|Il carattere viene copiato nella stringa di risultato senza alcuna modifica.<br /><br /> Altre informazioni: [Uso del carattere di escape](#escape).|2009\-06\-15T01:45:30 \(arr hh:mm t\) \-\> arr 01:45 A|  
  
 Nelle sezioni seguenti vengono fornite altre informazioni su ogni identificatore di formato data e ora personalizzato. Se non specificato diversamente, ogni identificatore genera una rappresentazione di stringa identica, indipendentemente dal fatto che venga usato con un valore <xref:System.DateTime> o con un valore <xref:System.DateTimeOffset>.  
  
<a name="dSpecifier"></a>   
## Identificatore di formato personalizzato "d"  
 L'identificatore di formato personalizzato "d" rappresenta il giorno del mese come numero compreso tra 1 e 31. Un giorno a una sola cifra viene formattato senza uno zero iniziale.  
  
 Se l'identificatore di formato "d" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "d". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "d" in diverse stringhe di formato.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#1)]
 [!code-vb[Formatting.DateAndTime.Custom#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#1)]  
  
 [Torna alla tabella](#table)  
  
<a name="ddSpecifier"></a>   
## Identificatore di formato personalizzato "dd"  
 La stringa di formato personalizzata "dd" rappresenta il giorno del mese come numero compreso tra 01 e 31. Un giorno a una sola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "dd" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#2)]  
  
 [Torna alla tabella](#table)  
  
<a name="dddSpecifier"></a>   
## Identificatore di formato personalizzato "ddd"  
 L'identificatore di formato personalizzato "ddd" rappresenta il nome abbreviato del giorno della settimana. Il nome abbreviato localizzato del giorno della settimana viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "ddd" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#3)]  
  
 [Torna alla tabella](#table)  
  
<a name="ddddSpecifier"></a>   
## Identificatore di formato personalizzato "dddd"  
 L'identificatore di formato personalizzato "dddd" \(più qualsiasi numero di identificatori "d" aggiuntivi\) rappresenta il nome completo del giorno della settimana. Il nome localizzato del giorno della settimana viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.DayNames%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "dddd" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#4)]  
  
 [Torna alla tabella](#table)  
  
<a name="fSpecifier"></a>   
## Identificatore di formato personalizzato "f"  
 L'identificatore di formato personalizzato "f" rappresenta la cifra più significativa della frazione di secondi, ovvero i decimi di secondo in un valore di data e ora.  
  
 Se l'identificatore di formato "f" viene usato senza altri identificatori di formato, viene interpretato come l'identificatore di formato di data e ora standard "f". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 Quando si usano identificatori di formato "f" come parte di una stringa di formato fornita al metodo <xref:System.DateTime.ParseExact%2A>, <xref:System.DateTime.TryParseExact%2A>, <xref:System.DateTimeOffset.ParseExact%2A> o <xref:System.DateTimeOffset.TryParseExact%2A>, il numero di identificatori di formato "f" indica il numero di cifre più significative della frazione di secondi che deve essere presente per analizzare correttamente la stringa.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "f" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="ffSpecifier"></a>   
## Identificatore di formato personalizzato "ff"  
 L'identificatore di formato personalizzato "ff" rappresenta le due cifre più significative della frazione di secondi, ovvero i centesimi di secondo in un valore di data e ora.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "ff" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="fffSpecifier"></a>   
## Identificatore di formato personalizzato "fff"  
 L'identificatore di formato personalizzato "fff" rappresenta le tre cifre più significative della frazione di secondi, ovvero i millisecondi in un valore di data e ora.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "fff" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="ffffSpecifier"></a>   
## Identificatore di formato personalizzato "ffff"  
 L'identificatore di formato personalizzato "ffff" rappresenta le quattro cifre più significative della frazione di secondi, ovvero i decimillesimi di secondo in un valore di data e ora.  
  
 Sebbene sia possibile visualizzare i decimillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT versione 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="fffffSpecifier"></a>   
## Identificatore di formato personalizzato "fffff"  
 L'identificatore di formato personalizzato "fffff" rappresenta le cinque cifre più significative della frazione di secondi, ovvero i centomillesimi di secondo in un valore di data e ora.  
  
 Sebbene sia possibile visualizzare i centomillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="ffffffSpecifier"></a>   
## Identificatore di formato personalizzato "ffffff"  
 L'identificatore di formato personalizzato "ffffff" rappresenta le sei cifre più significative della frazione di secondi, ovvero i milionesimi di secondo in un valore di data e ora.  
  
 Sebbene sia possibile visualizzare i milionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="fffffffSpecifier"></a>   
## Identificatore di formato personalizzato "fffffff"  
 L'identificatore di formato personalizzato "fffffff" rappresenta le sette cifre più significative della frazione di secondi, ovvero i decimilionesimi di secondo in un valore di data e ora.  
  
 Sebbene sia possibile visualizzare i decimilionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="F_Specifier"></a>   
## Identificatore di formato personalizzato "F"  
 L'identificatore di formato personalizzato "F" rappresenta la cifra più significativa della frazione di secondi, ovvero i decimi di secondo in un valore di data e ora. Se la cifra è zero, non viene prodotta alcuna visualizzazione.  
  
 Se l'identificatore di formato "F" viene usato senza altri identificatori di formato, viene interpretato come l'identificatore di formato di data e ora standard "F". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 Il numero di identificatoti di formato "F" usati con il metodo <xref:System.DateTime.ParseExact%2A>, <xref:System.DateTime.TryParseExact%2A>, <xref:System.DateTimeOffset.ParseExact%2A> o <xref:System.DateTimeOffset.TryParseExact%2A> indica il numero massimo di cifre più significative della frazione di secondi che possono essere presenti per analizzare correttamente la stringa.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "F" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="FF_Specifier"></a>   
## Identificatore di formato personalizzato "FF"  
 L'identificatore di formato personalizzato "FF" rappresenta le due cifre più significative della frazione di secondi, ovvero i centesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con due zeri non vengono tuttavia visualizzate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "FF" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="FFF_Specifier"></a>   
## Identificatore di formato personalizzato "FFF"  
 L'identificatore di formato personalizzato "FFF" rappresenta le tre cifre più significative della frazione di secondi, ovvero i millisecondi in un valore di data e ora. Gli zeri finali o le cifre con tre zeri non vengono tuttavia visualizzate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "FFF" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#5)]
 [!code-vb[Formatting.DateAndTime.Custom#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#5)]  
  
 [Torna alla tabella](#table)  
  
<a name="FFFF_Specifier"></a>   
## Identificatore di formato personalizzato "FFFF"  
 L'identificatore di formato personalizzato "FFFF" rappresenta le quattro cifre più significative della frazione di secondi, ovvero i decimillesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con quattro zeri non vengono tuttavia visualizzate.  
  
 Sebbene sia possibile visualizzare i decimillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="FFFFF_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFF"  
 L'identificatore di formato personalizzato "FFFFF" rappresenta le cinque cifre più significative della frazione di secondi, ovvero i centomillesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con cinque zeri non vengono tuttavia visualizzate.  
  
 Sebbene sia possibile visualizzare i centomillesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="FFFFFF_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFFF"  
 L'identificatore di formato personalizzato "FFFFFF" rappresenta le sei cifre più significative della frazione di secondi, ovvero i milionesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con sei zeri non vengono visualizzate.  
  
 Sebbene sia possibile visualizzare i milionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="FFFFFFF_Specifier"></a>   
## Identificatore di formato personalizzato "FFFFFFF"  
 L'identificatore di formato personalizzato "FFFFFFF" rappresenta le sette cifre più significative della frazione di secondi, ovvero i decimilionesimi di secondo in un valore di data e ora. Gli zeri finali o le cifre con sette zeri non vengono tuttavia visualizzate.  
  
 Sebbene sia possibile visualizzare i decimilionesimi di un componente relativo ai secondi di un valore di ora, tale valore potrebbe non essere significativo. La precisione dei valori di data e ora dipende dalla risoluzione del clock di sistema. Nei sistemi operativi Windows NT 3.5 e versioni successive e Windows Vista la risoluzione del clock è di circa 10\-15 millisecondi.  
  
 [Torna alla tabella](#table)  
  
<a name="gSpecifier"></a>   
## Identificatore di formato personalizzato "g" o "gg"  
 Gli identificatori di formato personalizzati "g" o "gg" \(più qualsiasi numero di identificatori "g" aggiuntivi\) rappresentano il periodo o l'era, ad esempio D.C. Questo identificatore viene ignorato dall'operazione di formattazione se la data da formattare non è associata a una stringa di periodo o di era.  
  
 Se l'identificatore di formato "g" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "g". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "g" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#6)]
 [!code-vb[Formatting.DateAndTime.Custom#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#6)]  
  
 [Torna alla tabella](#table)  
  
<a name="hSpecifier"></a>   
## Identificatore di formato personalizzato "h"  
 L'identificatore di formato personalizzato "h" rappresenta l'ora come numero compreso tra 1 e 12, ovvero l'ora rappresentata nell'orario in formato 12 ore in base al quale il conteggio riparte da mezzanotte o da mezzogiorno. Una particolare ora dopo mezzanotte non è distinguibile dalla stessa ora dopo mezzogiorno. L'ora non viene arrotondata e se è costituita da una singola cifra viene formattata senza zero iniziale. Se viene, ad esempio, specificata un'ora equivalente alle 5:43 della mattina o del pomeriggio, tramite questo identificatore di formato personalizzato viene visualizzato "5".  
  
 Se l'identificatore di formato "h" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "h" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="hhSpecifier"></a>   
## Identificatore di formato personalizzato "hh"  
 L'identificatore di formato personalizzato "hh" \(più qualsiasi numero di identificatori "h" aggiuntivi\) rappresenta l'ora come numero compreso tra 01 e 12, ovvero l'ora rappresentata nell'orario in formato 12 ore in base al quale il conteggio riparte da mezzanotte o da mezzogiorno. Una particolare ora dopo mezzanotte non è distinguibile dalla stessa ora dopo mezzogiorno. L'ora non viene arrotondata e se è costituita da una singola cifra viene formattata con uno zero iniziale. Se viene, ad esempio, specificata un'ora equivalente alle 5:43 della mattina o del pomeriggio, tramite questo identificatore di formato viene visualizzato "05".  
  
 L'esempio seguente include l'identificatore di formato personalizzato "hh" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]  
  
 [Torna alla tabella](#table)  
  
<a name="H_Specifier"></a>   
## Identificatore di formato personalizzato "H"  
 L'identificatore di formato personalizzato "H" rappresenta l'ora come numero compreso tra 0 e 23, ovvero l'ora rappresentata nell'orario in formato 24 ore a base zero in base al quale il conteggio riparte da mezzanotte. Un'ora costituita da una singola cifra viene formattata senza zero iniziale.  
  
 Se l'identificatore di formato "H" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "H" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#9)]
 [!code-vb[Formatting.DateAndTime.Custom#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#9)]  
  
 [Torna alla tabella](#table)  
  
<a name="HH_Specifier"></a>   
## Identificatore di formato personalizzato "HH"  
 L'identificatore di formato personalizzato "HH" \(più qualsiasi numero di identificatori "H" aggiuntivi\) rappresenta l'ora come numero compreso tra 00 e 23, ovvero l'ora rappresentata nell'orario in formato 24 ore a base zero in base al quale il conteggio riparte da mezzanotte. Un'ora costituita da una singola cifra viene formattata con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "HH" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#10)]
 [!code-vb[Formatting.DateAndTime.Custom#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#10)]  
  
 [Torna alla tabella](#table)  
  
<a name="KSpecifier"></a>   
## Identificatore di formato personalizzato "K"  
 L'identificatore di formato personalizzato "K" rappresenta le informazioni sul fuso orario di un valore di data e ora. Quando questo identificatore di formato viene usato con valori <xref:System.DateTime>, la stringa di risultato viene definita dal valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName>:  
  
-   Per il fuso orario locale \(un valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> uguale a <xref:System.DateTimeKind?displayProperty=fullName>\) questo identificatore è equivalente all'identificatore "zzz" e genera una stringa di risultato che contiene l'offset locale rispetto all'ora UTC \(Coordinated Universal Time\), ad esempio "\-07.00".  
  
-   Per un'ora UTC \(un valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> uguale a <xref:System.DateTimeKind?displayProperty=fullName>\) la stringa di risultato include un carattere "Z" per rappresentare una data UTC.  
  
-   Per un'ora di un fuso orario non specificato \(un'ora la cui proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> è uguale a <xref:System.DateTimeKind?displayProperty=fullName>\) il risultato è equivalente a <xref:System.String.Empty?displayProperty=fullName>.  
  
 Per i valori <xref:System.DateTimeOffset>, l'identificatore di formato "K" è equivalente all'identificatore di formato "zz" e genera una stringa di risultato che contiene l'offset del valore <xref:System.DateTimeOffset> rispetto a UTC.  
  
 Se l'identificatore di formato "K" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente mostra la stringa risultante dall'uso dell'identificatore di formato personalizzato "K" con vari valori <xref:System.DateTime> e <xref:System.DateTimeOffset> in un sistema nel fuso orario Pacifico \(Stati Uniti\).  
  
 [!code-csharp[Formatting.DateAndTime.Custom#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#12)]
 [!code-vb[Formatting.DateAndTime.Custom#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#12)]  
  
 [Torna alla tabella](#table)  
  
<a name="mSpecifier"></a>   
## Identificatore di formato personalizzato "m"  
 L'identificatore di formato personalizzato "m" rappresenta i minuti come numero compreso tra 0 e 59. Tali minuti rappresentano il numero intero di minuti passati dall'ultima ora. Un minuto costituito da una singola cifra viene formattato senza zero iniziale.  
  
 Se l'identificatore di formato "m" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "m". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "m" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="mmSpecifier"></a>   
## Identificatore di formato personalizzato "mm"  
 L'identificatore di formato personalizzato "mm" \(più qualsiasi numero di identificatori "m" aggiuntivi\) rappresenta i minuti come numero compreso tra 00 e 59. Tali minuti rappresentano il numero intero di minuti passati dall'ultima ora. Un minuto costituito da una singola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "mm" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]  
  
 [Torna alla tabella](#table)  
  
<a name="M_Specifier"></a>   
## Identificatore di formato personalizzato "M"  
 L'identificatore di formato personalizzato "M" rappresenta il mese come numero compreso tra 1 e 12 \(o tra 1 e 13 per i calendari con 13 mesi\). Un mese a una sola cifra viene formattato senza uno zero iniziale.  
  
 Se l'identificatore di formato "M" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "M". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "M" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#11)]
 [!code-vb[Formatting.DateAndTime.Custom#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#11)]  
  
 [Torna alla tabella](#table)  
  
<a name="MM_Specifier"></a>   
## Identificatore di formato personalizzato "MM"  
 L'identificatore di formato personalizzato "MM" rappresenta il mese come numero compreso tra 01 e 12 \(o tra 1 e 13 per i calendari con 13 mesi\). Un mese a una sola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "MM" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#2)]
 [!code-vb[Formatting.DateAndTime.Custom#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#2)]  
  
 [Torna alla tabella](#table)  
  
<a name="MMM_Specifier"></a>   
## Identificatore di formato personalizzato "MMM"  
 L'identificatore di formato personalizzato "MMM" rappresenta il nome abbreviato del mese. Il nome abbreviato localizzato del mese viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedMonthNames%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "MMM" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#3)]
 [!code-vb[Formatting.DateAndTime.Custom#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#3)]  
  
 [Torna alla tabella](#table)  
  
<a name="MMMM_Specifier"></a>   
## Identificatore di formato personalizzato "MMMM"  
 L'identificatore di formato personalizzato "MMMM" rappresenta il nome completo del mese. Il nome localizzato del mese viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "MMMM" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#4)]
 [!code-vb[Formatting.DateAndTime.Custom#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#4)]  
  
 [Torna alla tabella](#table)  
  
<a name="sSpecifier"></a>   
## Identificatore di formato personalizzato "s"  
 L'identificatore di formato personalizzato "s" rappresenta i secondi come numero compreso tra 0 e 59. Il risultato rappresenta il numero intero di secondi passati dall'ultimo minuto. Un secondo costituito da una singola cifra viene formattato senza zero iniziale.  
  
 Se l'identificatore di formato "s" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "s". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "s" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="ssSpecifier"></a>   
## Identificatore di formato personalizzato "ss"  
 L'identificatore di formato personalizzato "ss" \(più qualsiasi numero di identificatori "s" aggiuntivi\) rappresenta i secondi come numero compreso tra 00 e 59. Il risultato rappresenta il numero intero di secondi passati dall'ultimo minuto. Un secondo costituito da una singola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "ss" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]  
  
 [Torna alla tabella](#table)  
  
<a name="tSpecifier"></a>   
## Identificatore di formato personalizzato "t"  
 L'identificatore di formato personalizzato "t" rappresenta il primo carattere dell'indicatore AM\/PM. L'indicatore localizzato appropriato viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A?displayProperty=fullName> o <xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate. L'indicatore AM viene usato per tutti gli orari da 0:00:00 \(mezzanotte\) a 11:59:59.999. L'indicatore PM viene usato per tutti gli orari da 12:00:00 \(mezzogiorno\) a 23:59:59.999.  
  
 Se l'identificatore di formato "t" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato data e ora standard "t". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "t" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#7)]
 [!code-vb[Formatting.DateAndTime.Custom#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#7)]  
  
 [Torna alla tabella](#table)  
  
<a name="ttSpecifier"></a>   
## Identificatore di formato personalizzato "tt"  
 L'identificatore di formato personalizzato "tt" \(più qualsiasi numero di identificatori "t" aggiuntivi\) rappresenta l'indicatore AM\/PM completo. L'indicatore localizzato appropriato viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.AMDesignator%2A?displayProperty=fullName> o <xref:System.Globalization.DateTimeFormatInfo.PMDesignator%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate. L'indicatore AM viene usato per tutti gli orari da 0:00:00 \(mezzanotte\) a 11:59:59.999. L'indicatore PM viene usato per tutti gli orari da 12:00:00 \(mezzogiorno\) a 23:59:59.999.  
  
 Assicurarsi di usare l'identificatore "tt" per le lingue per le quali è necessario mantenere la distinzione tra AM e PM. Un esempio è la lingua giapponese per cui gli indicatori AM e PM differiscono in corrispondenza del secondo carattere anziché del primo.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "tt" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#8)]
 [!code-vb[Formatting.DateAndTime.Custom#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#8)]  
  
 [Torna alla tabella](#table)  
  
<a name="ySpecifier"></a>   
## Identificatore di formato personalizzato "y"  
 L'identificatore di formato personalizzato "y" rappresenta l'anno come numero a una cifra o a due cifre. Se l'anno ha più di due cifre, nel risultato vengono visualizzate solo le due cifre di ordine inferiore. Se la prima cifra di un anno a due cifre inizia con zero \(ad esempio, 2008\), il numero viene formattato senza zero iniziale.  
  
 Se l'identificatore di formato "y" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard "y". Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "y" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="yySpecifier"></a>   
## Identificatore di formato personalizzato "yy"  
 L'identificatore di formato personalizzato "yy" rappresenta l'anno come numero a due cifre. Se l'anno ha più di due cifre, nel risultato vengono visualizzate solo le due cifre di ordine inferiore. Se l'anno a due cifre ha meno di due cifre significative, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere due cifre.  
  
 In un'operazione di analisi, un anno a due cifre analizzato usando l'identificatore di formato personalizzato "yy" viene interpretato in base alla proprietà <xref:System.Globalization.Calendar.TwoDigitYearMax%2A?displayProperty=fullName> del calendario corrente del provider di formato. Nell'esempio seguente viene analizzata la rappresentazione di stringa di una data con un anno a due cifre usando il calendario gregoriano predefinito delle impostazioni cultura en\-US, che, in questo caso, sono le impostazioni cultura correnti. Modifica quindi l'oggetto <xref:System.Globalization.CultureInfo> delle impostazioni cultura correnti per usare un oggetto <xref:System.Globalization.GregorianCalendar> la cui proprietà <xref:System.Globalization.GregorianCalendar.TwoDigitYearMax%2A> è stata modificata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#19](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/parseexact2digityear1.cs#19)]
 [!code-vb[Formatting.DateAndTime.Custom#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/parseexact2digityear1.vb#19)]  
  
 L'esempio seguente include l'identificatore di formato personalizzato "yy" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="yyySpecifier"></a>   
## Identificatore di formato personalizzato "yyy"  
 L'identificatore di formato personalizzato "yyy" rappresenta l'anno con un minimo di tre cifre. Se l'anno ha più di tre cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di tre cifre, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere tre cifre.  
  
> [!NOTE]
>  Per il calendario buddista tailandese, in cui sono previsti anni di cinque cifre, questo identificatore di formato consente di visualizzare tutte le cifre significative.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "yyy" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="yyyySpecifier"></a>   
## Identificatore di formato personalizzato "yyyy"  
 L'identificatore di formato personalizzato "yyyy" rappresenta l'anno con un minimo di quattro cifre. Se l'anno ha più di quattro cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di quattro cifre, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere quattro cifre.  
  
> [!NOTE]
>  Per il calendario buddista tailandese, in cui sono previsti anni di cinque cifre, questo identificatore di formato visualizza un minimo di quattro cifre.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "yyyy" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="yyyyySpecifier"></a>   
## Identificatore di formato personalizzato "yyyyy"  
 L'identificatore di formato personalizzato "yyyyy" \(più qualsiasi numero di identificatori "y" aggiuntivi\) rappresenta l'anno con un minimo di cinque cifre. Se l'anno ha più di cinque cifre significative, queste vengono incluse nella stringa di risultato. Se l'anno ha meno di cinque cifre, al numero vengono anteposti tanti zeri quanto sono necessari per ottenere cinque cifre.  
  
 Se sono presenti identificatori "y" aggiuntivi, al numero vengono anteposti tanti zeri quanti sono necessari per ottenere il numero di identificatori "y".  
  
 L'esempio seguente include l'identificatore di formato personalizzato "yyyyy" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#13)]
 [!code-vb[Formatting.DateAndTime.Custom#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#13)]  
  
 [Torna alla tabella](#table)  
  
<a name="zSpecifier"></a>   
## Identificatore di formato personalizzato "z"  
 Con valori <xref:System.DateTime>, l'identificatore di formato personalizzato "z" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto a UTC \(Coordinated Universal Time\), misurato in ore. Non riflette il valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> di un'istanza. Per questo motivo non è consigliabile usare l'identificatore di formato "z" con valori <xref:System.DateTime>.  
  
 Con valori <xref:System.DateTimeOffset>, questo identificatore di formato rappresenta l'offset del valore <xref:System.DateTimeOffset> rispetto a UTC, in ore.  
  
 Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più \(\+\) indica le ore in più e un segno meno \(\-\) le ore in meno rispetto all'ora UTC. Un valore di offset a una sola cifra viene formattato senza uno zero iniziale.  
  
 Se l'identificatore di formato "z" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "z" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="zzSpecifier"></a>   
## Identificatore di formato personalizzato "zz"  
 Con valori <xref:System.DateTime>, l'identificatore di formato personalizzato "zz" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto a UTC, misurato in ore. Non riflette il valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> di un'istanza. Per questo motivo, non è consigliabile usare l'identificatore di formato "zz" con valori <xref:System.DateTime>.  
  
 Con valori <xref:System.DateTimeOffset>, questo identificatore di formato rappresenta l'offset del valore <xref:System.DateTimeOffset> rispetto a UTC, in ore.  
  
 Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più \(\+\) indica le ore in più e un segno meno \(\-\) le ore in meno rispetto all'ora UTC. Un valore di offset di una sola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "zz" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="zzzSpecifier"></a>   
## Identificatore di formato personalizzato "zzz"  
 Con valori <xref:System.DateTime>, l'identificatore di formato personalizzato "zzz" rappresenta l'offset con segno del fuso orario del sistema operativo locale rispetto a UTC, misurato in ore e minuti. Non riflette il valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> di un'istanza. Per questo motivo, non è consigliabile usare l'identificatore di formato "zzz" con valori <xref:System.DateTime>.  
  
 Con valori <xref:System.DateTimeOffset>, questo identificatore di formato rappresenta l'offset del valore <xref:System.DateTimeOffset> rispetto a UTC, in ore e minuti.  
  
 Lo scarto viene visualizzato sempre con un segno iniziale. Un segno più \(\+\) indica le ore in più e un segno meno \(\-\) le ore in meno rispetto all'ora UTC. Un valore di offset di una sola cifra viene formattato con uno zero iniziale.  
  
 L'esempio seguente include l'identificatore di formato personalizzato "zzz" in una stringa di formato personalizzata.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/Custom1.cs#14)]
 [!code-vb[Formatting.DateAndTime.Custom#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/Custom1.vb#14)]  
  
 [Torna alla tabella](#table)  
  
<a name="timeSeparator"></a>   
## Identificatore di formato personalizzato ":"  
 L'identificatore di formato personalizzato ":" rappresenta il separatore di ora che viene usato per distinguere ore, minuti e secondi. Il separatore di ora localizzato appropriato viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
> [!NOTE]
>  Per modificare il separatore dell'ora per una particolare stringa di data e ora, specificare il carattere separatore all'interno di un delimitatore di stringa letterale. Ad esempio, la stringa con formato personalizzato `hh'_'dd'_'ss` produce una stringa in cui "\_" \(carattere di sottolineatura\) è sempre usato come separatore dell'ora. Per cambiare il separatore dell'ora per tutte le date per una impostazione cultura, modificare il valore della proprietà <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A?displayProperty=fullName> per l'impostazione cultura attuale oppure creare un'istanza di un oggetto <xref:System.Globalization.DateTimeFormatInfo>, assegnare il carattere alla relativa proprietà <xref:System.Globalization.DateTimeFormatInfo.TimeSeparator%2A> e chiamare un overload del metodo di formattazione che include un parametro <xref:System.IFormatProvider>.  
  
 Se l'identificatore di formato ":" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 [Torna alla tabella](#table)  
  
<a name="dateSeparator"></a>   
## Identificatore di formato personalizzato "\/"  
 L'identificatore di formato personalizzato "\/" rappresenta il separatore di data usato per distinguere anni, mesi e giorni. Il separatore di data localizzato appropriato viene recuperato dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A?displayProperty=fullName> delle impostazioni cultura correnti o specificate.  
  
> [!NOTE]
>  Per modificare il separatore della data per una particolare stringa di data e ora, specificare il carattere separatore all'interno di un delimitatore di stringa letterale. Ad esempio, la stringa con formato personalizzato `mm'/'dd'/'yyyy` produce una stringa in cui "\/" è sempre usato come separatore dell'ora. Per cambiare il separatore della data per tutte le date per una impostazione cultura, modificare il valore della proprietà <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A?displayProperty=fullName> per l'impostazione cultura attuale oppure creare un'istanza di un oggetto <xref:System.Globalization.DateTimeFormatInfo>, assegnare il carattere alla relativa proprietà <xref:System.Globalization.DateTimeFormatInfo.DateSeparator%2A> e chiamare un overload del metodo di formattazione che include un parametro <xref:System.IFormatProvider>.  
  
 Se l'identificatore di formato "\/" viene usato senza altri identificatori di formato personalizzati, viene interpretato come l'identificatore di formato di data e ora standard e viene generato un evento <xref:System.FormatException>. Per altre informazioni sull'uso di un singolo identificatore di formato, vedere [Uso di singoli identificatori di formato personalizzati](#UsingSingleSpecifiers), più avanti in questo argomento.  
  
 [Torna alla tabella](#table)  
  
<a name="Notes"></a>   
## Note  
  
<a name="UsingSingleSpecifiers"></a>   
### Uso di singoli identificatori di formato personalizzati  
 Una stringa di formato di data e ora personalizzata è costituita da due o più caratteri. I metodi di formattazione di data e ora interpretano qualsiasi stringa a carattere singolo come stringa di formato di data e ora standard. Se il carattere non viene riconosciuto come identificatore di formato valido, viene generato un evento <xref:System.FormatException>. Una stringa di formato costituita solo dall'identificatore "h" viene ad esempio interpretata come una stringa di formato di data e ora standard. In questo caso specifico, tuttavia, viene generata un'eccezione in quanto non vi è alcun identificatore di formato di data e ora``standard "h".  
  
 Per usare qualsiasi identificatore di formato di data e ora personalizzato come unico identificatore in una stringa di formato \(ovvero, per usare l'identificatore di formato personalizzato "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" o "\/" da solo\), includere uno spazio prima o dopo l'identificatore oppure includere un identificatore di formato percentuale \("%"\) prima del singolo identificatore di data e ora personalizzato.  
  
 La stringa `%h"` viene ad esempio interpretata come una stringa di formato di data e ora personalizzata che consente di visualizzare l'ora rappresentata dal valore di data e ora corrente. È anche possibile usare la stringa di formato " h" o "h ", sebbene, in questo caso, verrà incluso uno spazio nella stringa di risultato insieme all'ora. Nell'esempio seguente vengono illustrate queste tre stringhe di formato.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#16](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/literal1.cs#16)]
 [!code-vb[Formatting.DateAndTime.Custom#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/literal1.vb#16)]  
  
<a name="escape"></a>   
### Uso del carattere di escape  
 I caratteri "d", "f", "F", "g", "h", "H", "K", "m", "M", "s", "t", "y", "z", ":" o "\/" in una stringa di formato vengono interpretati come identificatori di formato personalizzati anziché come caratteri letterali. Per impedire che un carattere venga interpretato come un identificatore di formato, è possibile anteporvi una barra rovesciata \(\\\), che rappresenta il carattere di escape. Il carattere di escape indica che il carattere seguente è un valore letterale carattere che deve essere incluso nella stringa di risultato senza modifiche.  
  
 Per includere una barra rovesciata in una stringa dei risultati, è necessario aggiungere un carattere di escape facendolo quindi precedere da un'altra barra rovesciata \(`\\`\).  
  
> [!NOTE]
>  Alcuni compilatori, ad esempio i compilatori C\+\+ e C\#, possono anche interpretare un singolo carattere barra rovesciata come carattere di escape. Per assicurarsi che una stringa venga interpretata correttamente quando viene eseguita la formattazione, è possibile usare il carattere del valore letterale stringa letterale \(carattere @\) prima della stringa in C\# o aggiungere un altro carattere barra rovesciata prima di ogni barra rovesciata in C\# e C\+\+. Nell'esempio C\# seguente vengono illustrati entrambi gli approcci.  
  
 Nell'esempio seguente viene usato il carattere di escape per impedire che durante l'operazione di formattazione i caratteri "h" e "m" vengano interpretati come identificatori di formato.  
  
 [!code-csharp[Formatting.DateAndTime.Custom#15](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.DateAndTime.Custom/cs/escape1.cs#15)]
 [!code-vb[Formatting.DateAndTime.Custom#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.DateAndTime.Custom/vb/escape1.vb#15)]  
  
### Impostazioni del Pannello di controllo  
 L'impostazione **Opzioni internazionali e della lingua** nel Pannello di controllo influisce sulla stringa di risultato prodotta da un'operazione di formattazione che include molti degli identificatori di formato di data e ora personalizzati. Queste impostazioni vengono usate per inizializzare l'oggetto <xref:System.Globalization.DateTimeFormatInfo> associato alle impostazioni cultura del thread corrente, che fornisce i valori usati per definire la formattazione. Computer con impostazioni diverse generano stringhe di risultato diverse.  
  
 Se inoltre viene usato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29?displayProperty=fullName> per creare un'istanza di un nuovo oggetto <xref:System.Globalization.CultureInfo> che rappresenta le stesse impostazioni cultura delle impostazioni cultura del sistema correnti, le eventuali personalizzazioni definite tramite **Opzioni internazionali e della lingua** nel Pannello di controllo verranno applicate al nuovo oggetto <xref:System.Globalization.CultureInfo>. È possibile usare il costruttore di <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> per creare un oggetto <xref:System.Globalization.CultureInfo> che non rifletta le personalizzazioni di un sistema.  
  
### Proprietà DateTimeFormatInfo  
 La formattazione è influenzata dalle proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> corrente, che viene fornito in modo implicito dalle impostazioni cultura del thread correnti o in modo esplicito dal parametro <xref:System.IFormatProvider> del metodo che richiama la formattazione. Per il parametro <xref:System.IFormatProvider>, è necessario specificare un oggetto <xref:System.Globalization.CultureInfo>, che rappresenta determinate impostazioni cultura o un oggetto <xref:System.Globalization.DateTimeFormatInfo>.  
  
 La stringa di risultato prodotta da molti degli identificatori di formato di data e ora personalizzati dipende anche dalle proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> corrente. Nell'applicazione può quindi essere modificato il risultato prodotto da alcuni identificatori di formato di data e ora personalizzati modificando la proprietà <xref:System.Globalization.DateTimeFormatInfo> corrispondente. L'identificatore di formato "ddd" aggiunge, ad esempio, un nome di giorno della settimana abbreviato trovato nella matrice di stringhe <xref:System.Globalization.DateTimeFormatInfo.AbbreviatedDayNames%2A> alla stringa di risultato. In modo analogo, l'identificatore di formato "MMMM" aggiunge alla stringa di risultato un nome del mese completo trovato nella matrice di stringhe <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A>.  
  
## Vedere anche  
 <xref:System.DateTime?displayProperty=fullName>   
 <xref:System.IFormatProvider?displayProperty=fullName>   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [Esempio: Utilità di formattazione in .NET Framework 4](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)