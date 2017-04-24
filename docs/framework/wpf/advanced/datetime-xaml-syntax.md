---
title: "Sintassi DateTime XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DateTime (sintassi XAML) [WPF]"
  - "DateTime (sintassi XAML) [WPF], stringhe di formato"
  - "DateTime (sintassi XAML) [WPF], stringhe"
  - "DateTime (sintassi XAML) [WPF], utilizzo"
  - "DateTime (testo XAML) [WPF]"
  - "formato di data breve [WPF], DateTime"
ms.assetid: 5901710a-609b-40c8-9d65-f0016cd9090b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Sintassi DateTime XAML
Alcuni controlli, ad esempio <xref:System.Windows.Controls.Calendar> e <xref:System.Windows.Controls.DatePicker>, dispongono di proprietà che utilizzano il tipo <xref:System.DateTime>.  Sebbene in genere venga specificata una data o un'ora iniziale per questi controlli nel code\-behind in fase di esecuzione, è possibile specificare una data o un'ora iniziale in XAML.  Il parser XAML WPF gestisce analisi di valori <xref:System.DateTime> utilizzando una sintassi del testo XAML incorporata.  Questo argomento descrive le specifiche della sintassi del testo XAML <xref:System.DateTime>.  
  
   
  
<a name="where_datetime_xaml_syntax_is_used"></a>   
## Quando utilizzare la sintassi DateTime XAML  
 Impostare le date in XAML non è sempre necessario e può non essere appropriato.  Ad esempio, è possibile utilizzare la proprietà <xref:System.DateTime.Now%2A?displayProperty=fullName> per inizializzare una data in fase di esecuzione oppure è possibile apportare tutte le modifiche alla data di un calendario nel code\-behind basato sull'input dell'utente.  Vi sono tuttavia casi in cui è possibile specificare le date in <xref:System.Windows.Controls.Calendar> e <xref:System.Windows.Controls.DatePicker> in un modello di controlli.  La sintassi XAML <xref:System.DateTime> deve essere utilizzata per questi scenari.  
  
### La sintassi DateTime di XAML è un comportamento nativo  
 <xref:System.DateTime> è una classe definita nelle librerie di  classe base del CLR.  A causa del modo in cui le librerie della classe di base si riferiscono al resto di CLR, non è possibile applicare <xref:System.ComponentModel.TypeConverterAttribute> alla classe e utilizzare un convertitore di tipi per elaborare stringhe da XAML e convertirle in <xref:System.DateTime> nel modello a oggetti in fase di esecuzione.  Non esiste una classe `DateTimeConverter` che fornisce il comportamento di conversione. Il comportamento di conversione descritto in questo argomento è nativo del parser XAML WPF.  
  
<a name="format_strings_for_datetime_xaml_syntax"></a>   
## Stringhe di formato per la sintassi DateTime XAML  
 È possibile specificare il formato di <xref:System.DateTime> con una stringa di formato.  Le stringhe di formato formalizzano la sintassi del testo che può essere utilizzata per creare un valore.  I valori <xref:System.DateTime> per i controlli WPF utilizzano in genere solo i componenti data di <xref:System.DateTime> e non i componenti ora.  
  
 Quando si specifica un <xref:System.DateTime> in XAML, è possibile utilizzare indifferentemente qualsiasi stringa di formato.  
  
 È possibile utilizzare anche formati e stringhe di formato che non sono mostrate in maniera specifica in questo argomento.  Tecnicamente, XAML per qualsiasi valore <xref:System.DateTime> specificato e analizzato dal parser di XAML WPF, utilizza una chiamata interna a <xref:System.DateTime.Parse%2A?displayProperty=fullName>, pertanto è possibile utilizzare qualsiasi stringa accettata da <xref:System.DateTime.Parse%2A?displayProperty=fullName> per l'input XAML.  Per ulteriori informazioni, vedere <xref:System.DateTime.Parse%2A?displayProperty=fullName>.  
  
> [!IMPORTANT]
>  La sintassi DateTime XAML utilizza sempre `en-us` come <xref:System.Globalization.CultureInfo> per la conversione nativa.  Non è influenzato dal valore <xref:System.Windows.FrameworkElement.Language%2A> o `xml:lang` in XAML, perché gli atti di conversione dei tipi a livello di attributo XAML agiscono senza quel contesto.  Non tentare di interpolare le stringhe di formato mostrate qui a causa di variazioni relative alla lingua, quale l'ordine nel quale vengono visualizzati giorno e mese.  Le stringhe di formato mostrate qui sono le stesse stringhe di formato utilizzate in caso di analisi del XALM indipendentemente dalle altre impostazioni cultura.  
  
 Nelle sezioni seguenti vengono descritte alcune delle stringhe di formato comuni di <xref:System.DateTime>.  
  
### Schema di data breve \("d"\).  
 Il formato della data breve per <xref:System.DateTime> in XAML è il seguente:  
  
 `M/d/YYYY`  
  
 Questo è il form più semplice che specifica tutte le informazioni necessarie per il tipico utilizzo da parte dei controlli WPF e non può essere influenzato dagli offset di fuso orario rispetto a un componente relativo all'ora e viene consigliato pertanto sugli altri formati.  
  
 Ad esempio, per specificare la data del 1 giugno 2010, utilizzare la seguente stringa:  
  
 `3/1/2010`  
  
 Per ulteriori informazioni, vedere <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=fullName>.  
  
### Schema di data\/ora ordinabile \("s"\)  
 Di seguito viene illustrato il modello <xref:System.DateTime> ordinabile in XAML:  
  
 `yyyy'-'MM'-'dd'T'HH':'mm':'ss`  
  
 Ad esempio, per specificare la data del 1 giugno 2010, utilizzare la seguente stringa \(tutti i componenti relativi all'ora vengono immessi come 0\):  
  
 `2010-06-01T000:00:00`  
  
### Schema RFC1123 \("r"\).  
 Il modello RFC1123 è utile perché potrebbe essere un input di stringa da altri generatori di data che pure utilizzano il modello RFC1123 per via delle impostazioni cultura invariabili.  Di seguito viene illustrato il modello <xref:System.DateTime> RFC1123 in XAML:  
  
 `ddd, dd MMM yyyy HH':'mm':'ss 'UTC'`  
  
 Ad esempio, per specificare la data del 1 giugno 2010, utilizzare la seguente stringa \(tutti i componenti relativi all'ora vengono immessi come 0\):  
  
 `Mon, 01 Jun 2010 00:00:00 UTC`  
  
### Gli altri formati e modelli  
 Come dichiarato precedentemente, è possibile specificare <xref:System.DateTime> in XAML come qualsiasi stringa che sia accettabile come input per <xref:System.DateTime.Parse%2A?displayProperty=fullName>.  Questo include gli altri formati formalizzati \(ad esempio <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>\) e formati che non sono formalizzati come un particolare form <xref:System.Globalization.DateTimeFormatInfo>.  Ad esempio, il form `YYYY/mm/dd` sia accettabile come input per <xref:System.DateTime.Parse%2A?displayProperty=fullName>.  Questo argomento non tenta di descrivere tutti i possibili formati che funzionano e invece consiglia il formato di data breve come pratica standard.  
  
## Vedere anche  
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)