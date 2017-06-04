---
title: "Analisi di stringhe numeriche in .NET Framework | Microsoft Docs"
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
  - "analisi di stringhe, stringhe numeriche"
  - "stringhe numeriche"
  - "enumerazioni [.NET Framework], analisi di stringhe"
  - "tipi di base, analisi di stringhe"
ms.assetid: e39324ee-72e5-42d4-a80d-bf3ee7fc6c59
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Analisi di stringhe numeriche in .NET Framework
Tutti i tipi numerici dispongono di due metodi di analisi statici, `Parse` e `TryParse`, che è possibile utilizzare per convertire la rappresentazione di stringa di un numero in un tipo numerico.  Questi metodi consentono di analizzare le stringhe che sono state generate mediante le stringhe di formato descritte in [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md) e [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md).  Per impostazione predefinita, i metodi `TryParse` e `Parse` possono essere utilizzati per convertire correttamente le stringhe contenenti solo cifre decimali integrali in valori integer.  Consentono di convertire correttamente le stringhe contenenti cifre decimali integrali e frazionarie, separatori di gruppi e un separatore decimale in valori a virgola mobile.  Se l'operazione ha esito negativo, il metodo `Parse` genera un'eccezione, mentre il metodo `TryParse` restituisce `false`.  
  
## Analisi e provider di formato  
 In genere, le rappresentazioni di stringa di valori numerici differiscono in base alle impostazioni cultura.  Gli elementi delle stringhe numeriche, ad esempio simboli di valuta, separatori di gruppi \(o migliaia\) e separatori decimali, variano tutti in base alle impostazioni cultura.  I metodi di analisi sia in modo implicito che in modo esplicito utilizzano un provider di formato che riconosce tali variazioni specifiche delle impostazioni cultura.  Se in una chiamata al metodo `TryParse` o `Parse` non viene specificato alcun provider di formato, viene utilizzato il provider di formato associato alle impostazioni cultura del thread corrente, ovvero l'oggetto <xref:System.Globalization.NumberFormatInfo> restituito dalla proprietà <xref:System.Globalization.NumberFormatInfo.CurrentInfo%2A?displayProperty=fullName>.  
  
 Un provider di formato è rappresentato da un'implementazione di <xref:System.IFormatProvider>.  Questa interfaccia dispone di un singolo membro, il metodo <xref:System.IFormatProvider.GetFormat%2A>, il cui unico parametro è un oggetto <xref:System.Type> che rappresenta il tipo da formattare.  Questo metodo restituisce l'oggetto che fornisce le informazioni sulla formattazione.  .NET Framework supporta le seguenti due implementazioni di <xref:System.IFormatProvider> per analizzare le stringhe numeriche:  
  
-   Oggetto <xref:System.Globalization.CultureInfo> il cui metodo <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=fullName> restituisce un oggetto <xref:System.Globalization.NumberFormatInfo> che fornisce le informazioni sulla formattazione specifiche delle impostazioni cultura.  
  
-   Oggetto <xref:System.Globalization.NumberFormatInfo> il cui metodo <xref:System.Globalization.NumberFormatInfo.GetFormat%2A?displayProperty=fullName> restituisce se stesso.  
  
 Nell'esempio seguente si tenta di convertire ogni stringa di una matrice in un valore <xref:System.Double>.  Viene innanzitutto tentata l'analisi della stringa utilizzando un provider di formato che riflette le convenzioni delle impostazioni cultura inglesi \(Stati Uniti\).  Se l'operazione genera un'eccezione <xref:System.FormatException>, viene tentata l'analisi della stringa utilizzando un provider di formato che riflette le convenzioni delle impostazioni cultura francesi \(Francia\).  
  
 [!code-csharp[Parsing.Numbers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/formatproviders1.cs#1)]
 [!code-vb[Parsing.Numbers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/formatproviders1.vb#1)]  
  
## Analisi e valori NumberStyles  
 Gli elementi di stile, ad esempio spazio vuoto, separatori di gruppi e separatore decimale, che possono essere gestiti dall'operazione di analisi vengono definiti da un valore di enumerazione <xref:System.Globalization.NumberStyles>.  Per impostazione predefinita, le stringhe che rappresentano i valori integer vengono analizzate utilizzando il valore <xref:System.Globalization.NumberStyles?displayProperty=fullName>, che consente solo cifre numeriche, gli spazi iniziale e finale e un segno iniziale.  Le stringhe che rappresentano i valori a virgola mobile vengono analizzate utilizzando una combinazione dei valori <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>. Questo stile composto consente cifre decimali con spazi iniziale e finale, un segno iniziale, un separatore decimale, un separatore di gruppi e un esponente.  Chiamando un overload del metodo `TryParse` o `Parse` che include un parametro di tipo <xref:System.Globalization.NumberStyles> e impostando uno o più flag <xref:System.Globalization.NumberStyles>, è possibile controllare gli elementi di stile che possono essere presenti nella stringa affinché l'operazione di analisi abbia esito positivo.  
  
 Ad esempio, una stringa contenente un separatore di gruppi non può essere convertita in un valore <xref:System.Int32> tramite il metodo <xref:System.Int32.Parse%28System.String%29?displayProperty=fullName>.  Tuttavia, la conversione avrà esito positivo se si utilizza il flag <xref:System.Globalization.NumberStyles?displayProperty=fullName>, come illustrato di seguito.  
  
 [!code-csharp[Parsing.Numbers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/styles1.cs#2)]
 [!code-vb[Parsing.Numbers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/styles1.vb#2)]  
  
> [!WARNING]
>  L'operazione di analisi utilizza sempre le convenzioni di formattazione delle impostazioni cultura specifiche.  Se non vengono specificate impostazioni cultura passando un oggetto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.NumberFormatInfo>, verranno utilizzate le impostazioni cultura associate al thread corrente.  
  
 Nella tabella seguente sono elencati i membri dell'enumerazione <xref:System.Globalization.NumberStyles> e viene descritto l'effetto che hanno sull'operazione di analisi.  
  
|Valore NumberStyles|Effetto sulla stringa da analizzare|  
|-------------------------|-----------------------------------------|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Solo consentite solo cifre numeriche.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Sono consentiti il separatore decimale e cifre frazionarie.  Per i valori integer è consentito solo lo zero come cifra frazionaria.  I separatori decimali validi sono determinati dalla proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A?displayProperty=fullName> o <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È possibile utilizzare il carattere "e" o "E" per indicare la notazione esponenziale.  Per ulteriori informazioni, vedere <xref:System.Globalization.NumberStyles>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È consentito lo spazio iniziale.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È consentito lo spazio finale.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Un segno positivo o negativo può precedere le cifre numeriche.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Un segno positivo o negativo può seguire le cifre numeriche.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È possibile utilizzare le parentesi per indicare valori negativi.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È consentito il separatore di gruppi.  Il carattere separatore di gruppi è determinato dalla proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A?displayProperty=fullName> o <xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|È consentito il simbolo di valuta.  Il simbolo di valuta è definito dalla proprietà <xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|La stringa da analizzare viene interpretata come numero esadecimale.  È possibile includere le cifre esadecimali 0\-9, A\-F e a\-f.  Questo flag può essere utilizzato solo per analizzare i valori integer.|  
  
 Inoltre, l'enumerazione <xref:System.Globalization.NumberStyles> fornisce i seguenti stili compositi, che includono più flag <xref:System.Globalization.NumberStyles>.  
  
|Valore NumberStyles composito|Membri inclusi|  
|-----------------------------------|--------------------|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include gli stili <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>.  Si tratta dello stile predefinito utilizzato per analizzare i valori integer.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include gli stili <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include gli stili <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include tutti gli stili tranne <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include tutti gli stili tranne <xref:System.Globalization.NumberStyles?displayProperty=fullName>.|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|Include gli stili <xref:System.Globalization.NumberStyles?displayProperty=fullName>, <xref:System.Globalization.NumberStyles?displayProperty=fullName> e <xref:System.Globalization.NumberStyles?displayProperty=fullName>.|  
  
## Analisi e cifre Unicode  
 Lo standard Unicode definisce gli elementi di codice per le cifre in diversi sistemi di scrittura.  Ad esempio, gli elementi di codice compresi tra U\+0030 e U\+0039 rappresentano le cifre latine di base da 0 a 9, gli elementi di codice compresi tra U\+09E6 e U\+09EF rappresentano le cifre bengalesi da 0 a 9 e gli elementi di codice compresi tra U\+FF10 e U\+FF19 rappresentano le cifre Fullwidth da 0 a 9.  Tuttavia, le uniche cifre numeriche riconosciute dai metodi di analisi sono le cifre latine di base da 0 a 9 con gli elementi di codice compresi tra U\+0030 e U\+0039.  Se a un metodo di analisi numerico viene passata una stringa che contiene altre cifre, il metodo genera un'eccezione <xref:System.FormatException>.  
  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Int32.Parse%2A?displayProperty=fullName> per analizzare le stringhe costituite da cifre in diversi sistemi di scrittura.  Come illustrato nell'output dell'esempio, il tentativo di analizzare le cifre latine di base ha esito positivo, mentre il tentativo di analisi delle cifre Fullwidth, indoarabiche e bengalesi ha esito negativo.  
  
 [!code-csharp[Parsing.Numbers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/unicode1.cs#3)]
 [!code-vb[Parsing.Numbers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/unicode1.vb#3)]  
  
## Vedere anche  
 <xref:System.Globalization.NumberStyles>   
 [Analisi di stringhe](../../../docs/standard/base-types/parsing-strings.md)   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)