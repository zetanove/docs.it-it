---
title: "Analisi delle stringhe di data e ora in .NET Framework | Microsoft Docs"
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
  - "tipi di base, analisi di stringhe"
  - "stringhe di data e ora"
  - "DateTime (oggetto)"
  - "enumerazioni [.NET Framework], analisi di stringhe"
  - "ParseExact (metodo)"
  - "analisi di stringhe, stringhe di data e ora"
  - "stringhe di ora"
ms.assetid: 43bae51e-9b1d-41a6-a187-772c0d096d90
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Analisi delle stringhe di data e ora in .NET Framework
I metodi di analisi consentono di convertire la rappresentazione di stringhe di data e ora in un oggetto <xref:System.DateTime> equivalente.  Con i metodi <xref:System.DateTime.Parse%2A> e <xref:System.DateTime.TryParse%2A> è possibile convertire alcune rappresentazioni comuni di data e ora.  I metodi <xref:System.DateTime.ParseExact%2A> e <xref:System.DateTime.TryParseExact%2A> consentono di convertire una rappresentazione di stringa conforme al modello specificato da una stringa di formato di data e ora. Vedere gli argomenti [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md) e [Stringhe di formato di data e ora personalizzate](../../../docs/standard/base-types/custom-date-and-time-format-strings.md).  
  
 L'analisi è influenzata dalle proprietà di un provider di formato che fornisce informazioni quali le stringhe utilizzate per i separatori di data e ora e i nomi di mesi, giorni ed ere.  Il provider di formato è l'oggetto <xref:System.Globalization.DateTimeFormatInfo> corrente fornito implicitamente dalle impostazioni cultura del thread corrente o esplicitamente dal parametro <xref:System.IFormatProvider> di un metodo di analisi.  Per il parametro <xref:System.IFormatProvider>, specificare un oggetto <xref:System.Globalization.CultureInfo>, che rappresenta determinate impostazioni cultura, o un oggetto <xref:System.Globalization.DateTimeFormatInfo>.  
  
 Nella rappresentazione di stringa di una data da analizzare devono essere inclusi il mese e almeno un giorno o un anno.  Nella rappresentazione di stringa oraria devono essere inclusi l'ora e almeno i minuti o l'indicatore A.M.\/P.M.  L'analisi tuttavia fornisce se possibile valori predefiniti per i componenti omessi.  Se manca una data verrà utilizzato come valore predefinito la data corrente, se manca l'anno verrà utilizzato come valore predefinito l'anno corrente, se manca il giorno del mese verrà utilizzato come valore predefinito il primo giorno del mese e se manca l'ora verrà utilizzato come valore predefinito la mezzanotte.  
  
 Se nella rappresentazione di stringa viene specificata solo l'ora, l'analisi restituisce un oggetto <xref:System.DateTime> con le proprietà <xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A> e <xref:System.DateTime.Day%2A> impostate sui valori corrispondenti della proprietà <xref:System.DateTime.Today%2A>.  Se tuttavia nel metodo di analisi è specificata la costante <xref:System.Globalization.DateTimeStyles>, le proprietà dell'anno, del mese e del giorno risultanti vengono impostate sul valore `1`.  
  
 Oltre a un componente data e ora, la rappresentazione di stringa di una data e ora può includere un offset che indica la differenza dall'ora UTC \(Coordinated Universal Time\).  Ad esempio, la stringa "2\/14\/2007 5:32:00 \-7:00" definisce una data e ora indietro di sette ore rispetto all'ora UTC.  Se nella rappresentazione di stringa di data e ora viene omesso l'offset, l'analisi restituisce un oggetto <xref:System.DateTime> con la proprietà <xref:System.DateTime.Kind%2A> impostata su <xref:System.DateTimeKind?displayProperty=fullName>.  Se invece l'offset viene specificato, l'analisi restituisce un oggetto <xref:System.DateTime> con la proprietà <xref:System.DateTime.Kind%2A> impostata su <xref:System.DateTimeKind> e il valore regolato in base al fuso orario locale del computer.  È possibile modificare questo comportamento utilizzando una costante <xref:System.Globalization.DateTimeStyles> con il metodo di analisi.  
  
 Il provider di formato viene utilizzato anche per interpretare una data numerica ambigua.  Nella data rappresentata dalla stringa "02\/03\/04" ad esempio non è chiaro a quali componenti corrispondano il mese, il giorno e l'anno.  In questo caso i componenti vengono interpretati secondo l'ordine di formati di data simili del provider di formato.  
  
## Parse  
 Nell'esempio di codice riportato di seguito viene illustrato l'utilizzo del metodo **Parse** per convertire una stringa in un **DateTime**.  Per eseguire l'analisi, vengono utilizzate le impostazioni cultura associate al thread corrente.  Se l'oggetto <xref:System.Globalization.CultureInfo> associato alle impostazioni cultura correnti non è in grado di analizzare la stringa di input, verrà generata un'eccezione <xref:System.FormatException>.  
  
 [!code-csharp[Parsing.DateAndTime#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example.cs#1)]
 [!code-vb[Parsing.DateAndTime#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example.vb#1)]  
  
 È inoltre possibile specificare un oggetto **CultureInfo** impostato su una delle impostazioni cultura definite da tale oggetto oppure è possibile specificare uno degli oggetti <xref:System.Globalization.DateTimeFormatInfo> standard restituiti dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>.  Nell'esempio di codice che segue viene utilizzato un provider di formato per analizzare una stringa in lingua tedesca e convertirla in un **DateTime**.  Un **CultureInfo** relativo alle impostazioni cultura de\-DE viene definito e passato con la stringa da analizzare per assicurare che l'operazione venga eseguita correttamente.  In questo modo l'impostazione definita nell'oggetto **CurrentCulture** di **CurrentThread** viene ignorata.  
  
 [!code-csharp[Parsing.DateAndTime#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example2.cs#2)]
 [!code-vb[Parsing.DateAndTime#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example2.vb#2)]  
  
 Tuttavia, sebbene sia possibile utilizzare gli overload del metodo <xref:System.DateTime.Parse%2A> per specificare i provider di formato personalizzato, il metodo non supporta l'utilizzo di provider di formato non standard.  Per analizzare una data e un'ora espresse in un formato non standard, utilizzare in alternativa il metodo <xref:System.DateTime.ParseExact%2A>.  
  
 Nell'esempio di codice seguente viene utilizzata l'enumerazione <xref:System.Globalization.DateTimeStyles> per indicare che la data e ora correnti non devono essere aggiunte all'oggetto **DateTime** per i campi non definiti dalla stringa specificata.  
  
 [!code-csharp[Parsing.DateAndTime#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example3.cs#3)]
 [!code-vb[Parsing.DateAndTime#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example3.vb#3)]  
  
## ParseExact  
 Il metodo <xref:System.DateTime.ParseExact%2A?displayProperty=fullName> converte una stringa conforme a un modello di stringa specificato in un oggetto **DateTime**.  Se si passa a questo metodo una stringa di formato diverso da quello specificato, viene generata un'eccezione <xref:System.FormatException>.  È possibile specificare uno degli identificatori di formato di data e ora standard o una combinazione limitata degli identificatori di formato di data e ora personalizzati.  Gli identificatori di formato personalizzati consentono di creare una stringa di riconoscimento personalizzata.  Per informazioni sugli identificatori, vedere gli argomenti [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md) e [Stringhe di formato di data e ora personalizzate](../../../docs/standard/base-types/custom-date-and-time-format-strings.md).  
  
 Ogni overload del metodo <xref:System.DateTime.ParseExact%2A> ha anche un parametro <xref:System.IFormatProvider> che in genere fornisce informazioni sulle impostazioni cultura specifiche relative alla formattazione della stringa.  In genere, l'oggetto <xref:System.IFormatProvider> è un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura standard o un oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>.  Tuttavia, a differenza di altre funzioni di analisi di data e ora, questo metodo supporta anche un oggetto <xref:System.IFormatProvider> che definisce un formato di data e ora non standard.  
  
 Nell'esempio seguente, al metodo **ParseExact** viene passato un oggetto stringa da analizzare, seguito da un identificatore di formato e quindi da un oggetto **CultureInfo**.  Il metodo **ParseExact** consente di analizzare solamente le stringhe con il formato di data estesa delle impostazioni cultura en\-US.  
  
 [!code-csharp[Parsing.DateAndTime#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example4.cs#4)]
 [!code-vb[Parsing.DateAndTime#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example4.vb#4)]  
  
## Vedere anche  
 [Analisi di stringhe](../../../docs/standard/base-types/parsing-strings.md)   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Conversione di tipi in .NET Framework](../../../docs/standard/base-types/type-conversion.md)