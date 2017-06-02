---
title: "Utilizzo di calendari | Microsoft Docs"
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
  - "calendari, applicazioni globali"
  - "impostazioni cultura, calendari"
  - "applicazioni globali, calendari"
  - "globalizzazione [.NET Framework], calendari"
  - "applicazioni internazionali [.NET Framework], calendari"
  - "applicazioni world-ready, calendari"
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Utilizzo di calendari
Sebbene un valore di data e ora rappresenti un momento, la relativa rappresentazione di stringa è dipendente dalle impostazioni cultura e dipende sia dalle convenzioni utilizzate per visualizzare i valori di data e ora da impostazioni cultura specifiche che dal calendario utilizzato dalle impostazioni cultura.  In questo argomento vengono illustrati il supporto dei calendari in .NET Framework e l'utilizzo delle classi di calendario quando si utilizzano i valori di data.  
  
## Calendari in .NET Framework  
 Tutti i calendari in .NET Framework derivano dalla classe <xref:System.Globalization.Calendar?displayProperty=fullName>, che fornisce l'implementazione del calendario di base.  Una delle classi che eredita dalla classe <xref:System.Globalization.Calendar> è la classe <xref:System.Globalization.EastAsianLunisolarCalendar>, che è la classe di base per tutti i calendari lunisolari.  .NET Framework include le implementazioni dei calendari seguenti:  
  
-   <xref:System.Globalization.ChineseLunisolarCalendar>, che rappresenta il calendario lunisolare cinese.  
  
-   <xref:System.Globalization.GregorianCalendar>, che rappresenta il calendario gregoriano.  Questo calendario viene ulteriormente suddiviso in sottotipi, ad esempio la versione araba e francese mediorientale, definiti dall'enumerazione <xref:System.Globalization.GregorianCalendarTypes?displayProperty=fullName>.  La proprietà <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=fullName> specifica il sottotipo del calendario gregoriano.  
  
-   <xref:System.Globalization.HebrewCalendar>, che rappresenta il calendario ebraico.  
  
-   <xref:System.Globalization.HijriCalendar>, che rappresenta il calendario Hijri.  
  
-   <xref:System.Globalization.JapaneseCalendar>, che rappresenta il calendario giapponese.  
  
-   <xref:System.Globalization.JapaneseLunisolarCalendar>, che rappresenta il calendario lunisolare giapponese.  
  
-   <xref:System.Globalization.JulianCalendar>, che rappresenta il calendario giuliano.  
  
-   <xref:System.Globalization.KoreanCalendar>, che rappresenta il calendario coreano.  
  
-   <xref:System.Globalization.KoreanLunisolarCalendar>, che rappresenta il calendario lunisolare coreano.  
  
-   <xref:System.Globalization.PersianCalendar>, che rappresenta il calendario persiano.  
  
-   <xref:System.Globalization.TaiwanCalendar>, che rappresenta il calendario taiwanese.  
  
-   <xref:System.Globalization.TaiwanLunisolarCalendar>, che rappresenta il calendario lunisolare taiwanese.  
  
-   <xref:System.Globalization.ThaiBuddhistCalendar>, che rappresenta il calendario buddista thailandese.  
  
-   <xref:System.Globalization.UmAlQuraCalendar>, che rappresenta il calendario Um Al Qura.  
  
 Un calendario può essere utilizzato in uno dei due modi seguenti:  
  
-   Come calendario utilizzato da impostazioni cultura specifiche.  Ogni oggetto <xref:System.Globalization.CultureInfo> dispone di un calendario corrente, che rappresenta il calendario utilizzato attualmente dall'oggetto.  Le rappresentazioni di stringa di tutti i valori di data e ora riflettono automaticamente le impostazioni cultura correnti e il relativo calendario corrente.  In genere, il calendario corrente è il calendario predefinito delle impostazioni cultura.  Gli oggetti <xref:System.Globalization.CultureInfo> dispongono inoltre di calendari facoltativi, che includono i calendari aggiuntivi utilizzati da tali impostazioni cultura.  
  
-   Come calendario autonomo indipendente da impostazioni cultura specifiche.  In questo caso, vengono utilizzati i metodi <xref:System.Globalization.Calendar> per esprimere le date come valori che riflettono il calendario.  
  
 Si noti che come calendari autonomi è possibile utilizzare solo sei classi di calendario, ovvero <xref:System.Globalization.ChineseLunisolarCalendar>, <xref:System.Globalization.JapaneseLunisolarCalendar>, <xref:System.Globalization.JulianCalendar>, <xref:System.Globalization.KoreanLunisolarCalendar>, <xref:System.Globalization.PersianCalendar> e <xref:System.Globalization.TaiwanLunisolarCalendar>.  Esse non vengono utilizzate dalle impostazioni cultura né come calendari predefiniti né come calendari facoltativi.  
  
## Calendari e impostazioni cultura  
 Le impostazioni cultura hanno un calendario predefinito, che viene definito dalla proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName>.  La proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> restituisce una matrice di oggetti <xref:System.Globalization.Calendar> che specifica tutti i calendari supportati dalle specifiche impostazioni cultura, incluso il calendario predefinito di tali impostazioni cultura.  
  
 Nell'esempio seguente vengono illustrate le proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>.  Vengono creati gli oggetti `CultureInfo` per le impostazioni cultura thailandesi \(Thailandia\) e giapponesi \(Giappone\) e vengono visualizzati i relativi calendari predefiniti e facoltativi.  Si noti che in entrambi i casi il calendario predefinito delle impostazioni cultura è incluso anche nella raccolta <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
 [!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]  
  
 Il calendario attualmente in uso da un oggetto <xref:System.Globalization.CultureInfo> specifico viene definito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName> delle impostazioni cultura.  L'oggetto <xref:System.Globalization.DateTimeFormatInfo> delle impostazioni cultura viene restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>.  Quando vengono create le impostazioni cultura, il relativo valore predefinito è uguale al valore della proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName>.  È tuttavia possibile sostituire il calendario corrente delle impostazioni cultura con qualsiasi calendario contenuto nella matrice restituita dalla proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>.  Se si tenta di impostare il calendario corrente su un calendario che non è incluso nel valore della proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>, viene generato un oggetto <xref:System.ArgumentException>.  
  
 Nell'esempio seguente viene modificato il calendario utilizzato dalle impostazioni cultura arabe \(Arabia Saudita\).  Viene innanzitutto creata un'istanza di un valore <xref:System.DateTime>, il quale viene quindi visualizzato utilizzando le impostazioni cultura correnti che, in questo caso, sono quelle inglesi \(Stati Uniti\) e il calendario corrente delle impostazioni cultura che, in questo caso, è il calendario gregoriano.  A questo punto vengono impostate le impostazioni cultura arabe \(Arabia Saudita\) e la data viene visualizzata utilizzando il calendario Um Al\-Qura predefinito.  Viene quindi chiamato il metodo `CalendarExists` per determinare se il calendario Hijri è supportato dalle impostazioni cultura arabe \(Arabia Saudita\).  Poiché il calendario è supportato, il calendario corrente viene sostituito con il calendario Hijri e viene visualizzata nuovamente la data.  Si noti che in ogni caso la data viene visualizzata utilizzando il calendario corrente delle impostazioni cultura correnti.  
  
 [!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
 [!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]  
  
## Date e calendari  
 Ad eccezione dei costruttori che includono un parametro di tipo <xref:System.Globalization.Calendar> e consentono agli elementi di una data, ad esempio mese, giorno e anno, di riflettere i valori in un calendario designato, entrambi i valori <xref:System.DateTime> e <xref:System.DateTimeOffset> si basano sempre sul calendario gregoriano.  Ciò significa, ad esempio, che la proprietà <xref:System.DateTime.Year%2A?displayProperty=fullName> restituisce l'anno nel calendario gregoriano e la proprietà <xref:System.DateTime.Day%2A?displayProperty=fullName> restituisce il giorno del mese nel calendario gregoriano.  
  
> [!IMPORTANT]
>  È importante tenere presente che esiste una differenza tra un valore di data e la relativa rappresentazione di stringa.  Il primo si basa sul calendario gregoriano, mentre il secondo si basa sul calendario corrente delle impostazioni cultura specifiche.  
  
 Nell'esempio seguente viene illustrata la differenza tra le proprietà <xref:System.DateTime> e i relativi metodi <xref:System.Globalization.Calendar> corrispondenti.  Nell'esempio le impostazioni cultura correnti sono quelle arabe \(Egitto\) e il calendario corrente è Um Al Qura.  Il valore <xref:System.DateTime> viene impostato sul quindicesimo giorno del settimo mese del 2011.  Risulta chiaro che tale valore viene interpretato come data del calendario gregoriano, poiché questi stessi valori vengono restituiti dal metodo <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> quando vengono utilizzate le convenzioni delle impostazioni cultura inglesi.  La rappresentazione di stringa della data formattata utilizzando le convenzioni delle impostazioni cultura correnti è 14\/08\/32, che è la data equivalente nel calendario Um Al Qura.  Successivamente, vengono utilizzati i membri di `DateTime` e `Calendar` per restituire il giorno, il mese e l'anno del valore <xref:System.DateTime>.  In ogni caso, i valori restituiti dai membri di <xref:System.DateTime> riflettono i valori del calendario gregoriano, mentre i valori restituiti dai membri di <xref:System.Globalization.UmAlQuraCalendar> riflettono i valori del calendario Um Al Qura.  
  
 [!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
 [!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]  
  
### Creazione di un'istanza delle date basate su un calendario  
 Poiché i valori <xref:System.DateTimeOffset> e <xref:System.DateTime> si basano sul calendario gregoriano, è necessario chiamare un costruttore di overload che include un parametro di tipo <xref:System.Globalization.Calendar> per creare un'istanza di un valore di data se si desidera utilizzare i valori di giorno, mese o anno da un calendario diverso.  È inoltre possibile chiamare uno degli overload del metodo <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=fullName> del calendario specifico per creare un'istanza di un oggetto <xref:System.DateTime> basato sui valori di un determinato calendario.  
  
 Nell'esempio seguente viene creata un'istanza di un valore <xref:System.DateTime> passando un oggetto <xref:System.Globalization.HebrewCalendar> a un costruttore <xref:System.DateTime> e viene creata un'istanza di un secondo valore <xref:System.DateTime> chiamando il metodo <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>.  Poiché i due valori vengono creati con valori identici dal calendario ebraico, la chiamata al metodo <xref:System.DateTime.Equals%2A?displayProperty=fullName> mostra che i due valori <xref:System.DateTime> sono uguali.  
  
 [!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
 [!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]  
  
### Rappresentazione delle date nel calendario corrente  
 I metodi di formattazione di data e ora utilizzano sempre il calendario corrente quando si convertono le date in stringhe.  Ciò significa che le rappresentazioni di stringa dell'anno, del mese e del giorno del mese riflettono il calendario corrente e non necessariamente il calendario gregoriano.  
  
 Nell'esempio seguente viene illustrato come il calendario corrente influisce sulla rappresentazione di stringa di una data.  Vengono sostituite le impostazioni cultura correnti con quelle cinesi \(tradizionale, Taiwan\) e viene creata un'istanza di un valore di data.  Viene quindi visualizzato il calendario corrente e la data, viene sostituito il calendario corrente con <xref:System.Globalization.TaiwanCalendar> e viene visualizzato il calendario corrente e di nuovo la data.  La prima volta che viene visualizzata la data, essa viene rappresentata come data del calendario gregoriano.  La seconda volta che viene visualizzata, essa viene rappresentata come data del calendario taiwanese.  
  
 [!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
 [!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]  
  
### Rappresentazione delle date in un calendario non corrente  
 Per rappresentare una data utilizzando un calendario che non è il calendario corrente delle impostazioni cultura specifiche, è necessario chiamare i metodi dell'oggetto <xref:System.Globalization.Calendar>.  Ad esempio, i metodi <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=fullName>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=fullName> e <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=fullName> convertono l'anno, il mese e il giorno in valori che riflettono un determinato calendario.  
  
> [!WARNING]
>  Poiché alcuni calendari non sono calendari facoltativi delle impostazioni cultura, per rappresentare le date in tali calendari è necessario chiamare sempre i metodi del calendario.  Ciò vale per tutti i calendari che derivano dalle classi <xref:System.Globalization.EastAsianLunisolarCalendar>, <xref:System.Globalization.JulianCalendar> e <xref:System.Globalization.PersianCalendar>.  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Globalization.JulianCalendar> per creare un'istanza di una data, il 9 gennaio 1905, nel calendario giuliano.  Quando tale data viene visualizzata utilizzando il calendario predefinito \(gregoriano\), essa viene rappresentata come il 22 gennaio 1905.  Le chiamate ai singoli metodi <xref:System.Globalization.JulianCalendar> consentono di rappresentare la data nel calendario giuliano.  
  
 [!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
 [!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]  
  
### Calendari e intervalli di date  
 La data più vicina supportata da un calendario è indicata dalla proprietà <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=fullName> del calendario.  Per la classe <xref:System.Globalization.GregorianCalendar>, tale data è il 1° gennaio, 0001. d.C. La maggior parte degli altri calendari in .NET Framework supportano una data successiva.  Il tentativo di utilizzare un valore di data e ora che precede la data più vicina supportata da un calendario genera un'eccezione <xref:System.ArgumentOutOfRangeException>.  
  
 Tuttavia, esiste un'eccezione importante.  Il valore \(non inizializzato\) predefinito di un oggetto <xref:System.DateTime> e un oggetto <xref:System.DateTimeOffset> è uguale al valore <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=fullName>.  Se si tenta di formattare la data in un calendario che non supporta il 1° gennaio, 0001. d. C. e non viene fornito un identificatore di formato, il metodo di formattazione utilizza l'identificatore di formato "s" \(schema di data\/ora ordinabile\), anziché l'identificatore di formato "G" \(schema di data\/ora generale\).  Di conseguenza, l'operazione di formattazione non genera un'eccezione <xref:System.ArgumentOutOfRangeException>.  Al contrario, restituisce la data non supportata.  Come illustrato nell'esempio, viene mostrato il valore <xref:System.DateTime.MinValue?displayProperty=fullName> quando le impostazioni cultura correnti sono impostate su giapponese \(Giappone\) con il calendario giapponese e su arabo \(Egitto\) con il calendario Um al Qura.  Vengono inoltre impostate le impostazioni cultura correnti su inglese \(Stati Uniti\) e viene chiamato il metodo <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=fullName> con ognuno di questi oggetti <xref:System.Globalization.CultureInfo>.  In ogni caso, la data viene visualizzata utilizzando lo schema di data\/ora ordinabile.  
  
 [!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
 [!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]  
  
## Utilizzo delle ere  
 I calendari dividono in genere le date in ere.  Tuttavia, le classi <xref:System.Globalization.Calendar> di .NET Framework non supportano tutte le ere definite da un calendario e la maggior parte delle classi <xref:System.Globalization.Calendar> supporta una sola era.  Solo le classi <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar> supportano più ere.  
  
### Ere e nomi di ere  
 In .NET Framework gli interi che rappresentano le ere supportate dall'implementazione di un calendario specifico vengono archiviati in ordine inverso nella matrice <xref:System.Globalization.Calendar.Eras%2A?displayProperty=fullName>.  L'era corrente è in corrispondenza dell'indice zero e per le classi <xref:System.Globalization.Calendar> che supportano più ere ciascun indice successivo riflette l'era precedente.  La proprietà <xref:System.Globalization.Calendar.CurrentEra?displayProperty=fullName> statica definisce l'indice dell'era corrente nella matrice <xref:System.Globalization.Calendar.Eras%2A?displayProperty=fullName>. Si tratta di una costante il cui valore è sempre zero.  Le singole classi <xref:System.Globalization.Calendar> includono anche i campi statici che restituiscono il valore dell'era corrente.  Tali valori vengono elencati nella tabella seguente.  
  
|Classe di calendario|Campo era corrente|  
|--------------------------|------------------------|  
|<xref:System.Globalization.ChineseLunisolarCalendar>|<xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>|  
|<xref:System.Globalization.GregorianCalendar>|<xref:System.Globalization.GregorianCalendar.ADEra>|  
|<xref:System.Globalization.HebrewCalendar>|<xref:System.Globalization.HebrewCalendar.HebrewEra>|  
|<xref:System.Globalization.HijriCalendar>|<xref:System.Globalization.HijriCalendar.HijriEra>|  
|<xref:System.Globalization.JapaneseLunisolarCalendar>|<xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra>|  
|<xref:System.Globalization.JulianCalendar>|<xref:System.Globalization.JulianCalendar.JulianEra>|  
|<xref:System.Globalization.KoreanCalendar>|<xref:System.Globalization.KoreanCalendar.KoreanEra>|  
|<xref:System.Globalization.KoreanLunisolarCalendar>|<xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>|  
|<xref:System.Globalization.PersianCalendar>|<xref:System.Globalization.PersianCalendar.PersianEra>|  
|<xref:System.Globalization.ThaiBuddhistCalendar>|<xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>|  
|<xref:System.Globalization.UmAlQuraCalendar>|<xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>|  
  
 Il nome corrispondente al numero dell'era specifico può essere recuperato passando il numero dell'era al metodo <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=fullName> o <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=fullName>.  Nell'esempio seguente vengono chiamati questi metodi per recuperare le informazioni sul supporto dell'era nella classe <xref:System.Globalization.GregorianCalendar>.  
  
 [!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs#7)]
 [!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb#7)]  
  
 Inoltre, la stringa di formato di data e ora personalizzata "g" include il nome dell'era di un calendario nella rappresentazione di stringa di una data e ora.  Per ulteriori informazioni, vedere [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md).  
  
### Creazione di un'istanza di una data con un'era  
 Per le due classi <xref:System.Globalization.Calendar> che supportano più ere, una data costituita da un valore specifico di anno, mese e giorno del mese può risultare ambigua. Ad esempio, tutte e quattro le ere di <xref:System.Globalization.JapaneseCalendar> hanno gli anni numerati da 1 a 15.  In genere, se non viene specificata un'era, entrambi i metodi del calendario e di data e ora presuppongono che i valori appartengano all'era corrente.  Per specificare in modo esplicito l'era quando viene creata un'istanza di una data per una classe <xref:System.Globalization.Calendar> che supporta più ere, è possibile chiamare il metodo <xref:System.Globalization.Calendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>.  Questo metodo consente di specificare in modo esplicito un'era insieme all'anno, al mese, al giorno, all'ora, al minuto, al secondo e al millisecondo del calendario.  
  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Globalization.Calendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName> per creare un'istanza della stessa data, il primo mese del primo giorno del secondo anno, in ogni era supportata dalla classe <xref:System.Globalization.JapaneseCalendar>.  Viene quindi visualizza la data sia nel calendario giapponese che in quello gregoriano.  Viene inoltre chiamato un costruttore <xref:System.DateTime> per illustrare che i metodi che creano i valori di data senza specificare un'era creano le date nell'era corrente.  
  
 [!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs#7)]
 [!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb#7)]  
  
### Rappresentazione delle date nei calendari con le ere  
 Se un oggetto <xref:System.Globalization.Calendar> supporta le ere ed è il calendario corrente di un oggetto <xref:System.Globalization.CultureInfo>, l'era viene inclusa nella rappresentazione di stringa di un valore di data e ora per i modelli di data e ora completa, di data estesa e di data breve.  Nell'esempio seguente vengono visualizzati questi modelli di data quando le impostazioni cultura correnti sono quelle giapponesi \(Giappone\) e il calendario corrente è il calendario giapponese.  
  
 [!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
 [!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]  
  
> [!WARNING]
>  La classe <xref:System.Globalization.JapaneseCalendar> è l'unica classe di calendario in .NET Framework che supporta le date in più ere e che può essere il calendario corrente di un oggetto <xref:System.Globalization.CultureInfo>, soprattutto di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura giapponesi \(Giappone\).  
  
 Per tutti i calendari l'identificatore di formato personalizzato "g" include l'era nella stringa di risultato.  Nell'esempio seguente viene utilizzata la stringa di formato personalizzata "MM\-dd\-yyyy g" per includere l'era nella stringa di risultato quando il calendario corrente è il calendario gregoriano.  
  
 [!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
 [!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]  
  
 Nei casi in cui la rappresentazione di stringa di una data viene espressa in un calendario che non è il calendario corrente, la classe <xref:System.Globalization.Calendar> include un metodo <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=fullName> che può essere utilizzato con i metodi <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=fullName>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=fullName> e <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=fullName> per indicare in modo non ambiguo una data, nonché l'era a cui appartiene.  Nell'esempio seguente viene utilizzata la classe <xref:System.Globalization.JapaneseLunisolarCalendar> per fornire un'illustrazione.  Si noti, tuttavia, che se si include un nome significativo o un'abbreviazione anziché un intero per l'era nella stringa di risultato, è necessario creare un'istanza di un oggetto <xref:System.Globalization.DateTimeFormatInfo> e rendere <xref:System.Globalization.JapaneseCalendar> il calendario corrente. Il calendario <xref:System.Globalization.JapaneseLunisolarCalendar> non può essere il calendario corrente delle impostazioni cultura, ma in questo caso i due calendari condividono le stesse ere.  
  
 [!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
 [!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]  
  
## Vedere anche  
 [Procedura: Visualizzare le date in calendari non gregoriani](../../../docs/standard/base-types/how-to-display-dates-in-non-gregorian-calendars.md)   
 [Esempio: Utilità per la visualizzazione di intervalli di settimane del calendario](http://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)