---
title: "Formattazione di tipi in .NET Framework | Microsoft Docs"
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
  - "dati (formattazione) [.NET Framework]"
  - "date [.NET Framework], formattazione"
  - "data (formattazione) [.NET Framework]"
  - "numeri (formattazione) [.NET Framework]"
  - "ToString (metodo)"
  - "impostazioni cultura personalizzate [.NET Framework]"
  - "numeri [.NET Framework], formattazione"
  - "formattazione delle stringhe [.NET Framework]"
  - "ora [.NET Framework], formattazione"
  - "valuta [.NET Framework], formattazione"
  - "tipi [.NET Framework], formattazione"
  - "identificatori di formato [.NET Framework]"
  - "ore [.NET Framework], formattazione"
  - "cultura [.NET Framework], formattazione"
  - "formattazione [.NET Framework], tipi supportati"
  - "tipi di base [.NET Framework], formattazione"
  - "formattazione personalizzata [.NET Framework]"
  - "stringhe [.NET Framework], formattazione"
ms.assetid: 0d1364da-5b30-4d42-8e6b-03378343343f
caps.latest.revision: 43
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 43
---
# Formattazione di tipi in .NET Framework
<a name="Introduction"></a> La formattazione è il processo di conversione di un'istanza di una classe, una struttura o un valore di enumerazione nella relativa rappresentazione di stringa, eseguito spesso in modo che la stringa risultante possa essere visualizzata dagli utenti o deserializzata per ripristinare il tipo di dati originale. Questa conversione può comportare le difficoltà seguenti:  
  
-   Il modo in cui i valori vengono archiviati internamente non riflette necessariamente il modo in cui gli utenti desiderano visualizzarli. Un numero di telefono potrebbe ad esempio venire archiviato nel formato 8009999999, che non è di immediata comprensione. Potrebbe invece essere preferibile visualizzarlo come 02 123 456. Vedere la sezione [Stringhe di formato personalizzate](#customStrings) per un esempio in cui un numero viene formattato in questo modo.  
  
-   La conversione di un oggetto nella relativa rappresentazione di stringa non è sempre intuitiva. Non è ad esempio chiaro come dovrebbe venire visualizzata la rappresentazione di stringa di un oggetto Temperature o di un oggetto Person. Per un esempio in cui viene formattato un oggetto Temperature in modi diversi, vedere la sezione [Stringhe di formato standard](#standardStrings).  
  
-   I valori richiedono spesso una formattazione dipendente dalle impostazioni cultura. In un'applicazione in cui vengono usati i numeri per riflettere valori monetari, ad esempio, le stringhe numeriche devono includere il simbolo di valuta, il separatore di gruppi, che nella maggior parte delle impostazioni cultura corrisponde al separatore delle migliaia, e il separatore decimale delle impostazioni cultura correnti. Per un esempio, vedere la sezione [Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider](#FormatProviders).  
  
-   È possibile che in un'applicazione lo stesso valore debba essere visualizzato in diversi modi. È ad esempio possibile che un membro di enumerazione venga rappresentato visualizzando una rappresentazione di stringa del relativo nome oppure visualizzando il relativo valore sottostante. Per un esempio in cui viene formattato un membro dell'enumerazione <xref:System.DayOfWeek> in modi diversi, vedere la sezione [Stringhe di formato standard](#standardStrings).  
  
> [!NOTE]
>  La formattazione consente di convertire il valore di un tipo in una rappresentazione di stringa, mentre l'analisi è l'operazione inversa. Un'operazione di analisi consente di creare un'istanza di un tipo di dati dalla relativa rappresentazione di stringa. Per informazioni sulla conversione di stringhe in altri tipi di dati, vedere [Analisi di stringhe](../../../docs/standard/base-types/parsing-strings.md).  
  
 In .NET Framework è disponibile un supporto avanzato della formattazione che consente agli sviluppatori di soddisfare questi requisiti.  
  
 In questa panoramica sono incluse le sezioni seguenti:  
  
-   [Formattazione in .NET Framework](#NetFormatting)  
  
-   [Formattazione predefinita tramite il metodo ToString](#DefaultToString)  
  
-   [Override del metodo ToString](#OverrideToString)  
  
-   [Metodo ToString e stringhe di formato](#FormatStrings)  
  
    -   [Stringhe di formato standard](#standardStrings)  
  
    -   [Stringhe di formato personalizzate](#customStrings)  
  
    -   [Stringhe di formato e tipi di libreria di classi .NET Framework](#stringRef)  
  
-   [Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider](#FormatProviders)  
  
    -   [Formattazione dipendente dalle impostazioni cultura di valori numerici](#numericCulture)  
  
    -   [Formattazione dipendente dalle impostazioni cultura di valori data e ora](#dateCulture)  
  
-   [Interfaccia IFormattable](#IFormattable)  
  
-   [Formattazione composita](#CompositeFormatting)  
  
-   [Formattazione personalizzata con ICustomFormatter](#Custom)  
  
-   [Argomenti correlati](#RelatedTopics)  
  
-   [Riferimento](#Reference)  
  
<a name="NetFormatting"></a>   
## Formattazione in .NET Framework  
 Il meccanismo di base per la formattazione è costituito dall'implementazione predefinita del metodo <xref:System.Object.ToString%2A?displayProperty=fullName>, illustrato nella sezione [Formattazione predefinita tramite il metodo ToString](#DefaultToString) più avanti in questo argomento. In .NET Framework sono tuttavia disponibili diversi metodi per modificare ed estendere il supporto predefinito della formattazione, tra cui:  
  
-   Override del metodo <xref:System.Object.ToString%2A?displayProperty=fullName> per definire una rappresentazione di stringa personalizzata del valore di un oggetto. Per altre informazioni, vedere la sezione [Override del metodo ToString](#OverrideToString) più avanti in questo argomento.  
  
-   Definizione di identificatori di formato che consentono l'assunzione di più forme da parte della rappresentazione di stringa del valore di un oggetto. L'identificatore di formato "X" nell'istruzione seguente consente, ad esempio, di convertire un valore intero nella rappresentazione di stringa di un valore esadecimale.  
  
     [!code-csharp[Conceptual.Formatting.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/specifier1.cs#3)]
     [!code-vb[Conceptual.Formatting.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/specifier1.vb#3)]  
  
     Per altre informazioni sugli identificatori di formato, vedere la sezione [Metodo ToString e stringhe di formato](#FormatStrings).  
  
-   Uso di provider di formato per sfruttare le convenzioni di formattazione di impostazioni cultura specifiche. Nell'istruzione seguente, ad esempio, viene visualizzato un valore di valuta usando le convenzioni di formattazione delle impostazioni cultura en\-US.  
  
     [!code-csharp[Conceptual.Formatting.Overview#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/specifier1.cs#10)]
     [!code-vb[Conceptual.Formatting.Overview#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/specifier1.vb#10)]  
  
     Per altre informazioni sulla formattazione con i provider di formato, vedere la sezione [Provider di formato e interfaccia IFormatProvider](#FormatProviders).  
  
-   Implementazione dell'interfaccia <xref:System.IFormattable> per supportare sia la conversione di stringa con la classe <xref:System.Convert> che la formattazione composita. Per altre informazioni, vedere la sezione [Interfaccia IFormattable](#IFormattable).  
  
-   Uso della formattazione composita per incorporare la rappresentazione di stringa di un valore in una stringa di dimensioni maggiori. Per altre informazioni, vedere la sezione [Formattazione composita](#CompositeFormatting).  
  
-   Implementazione di <xref:System.ICustomFormatter> e <xref:System.IFormatProvider> per fornire una soluzione di formattazione personalizzata completa. Per altre informazioni, vedere la sezione [Formattazione personalizzata con ICustomFormatter](#Custom).  
  
 Nelle sezioni seguenti vengono esaminati questi metodi per la conversione di un oggetto nella relativa rappresentazione di stringa.  
  
 [Torna all'inizio](#Introduction)  
  
<a name="DefaultToString"></a>   
## Formattazione predefinita tramite il metodo ToString  
 Ogni tipo derivato da <xref:System.Object?displayProperty=fullName> eredita automaticamente un metodo `ToString` senza parametri che, per impostazione predefinita, restituisce il nome del tipo. Nell'esempio seguente viene illustrato il metodo `ToString` predefinito. Viene definita una classe denominata `Automobile` che non dispone di implementazione. Quando viene creata un'istanza della classe e viene chiamato il relativo metodo `ToString`, viene visualizzato il nome del tipo relativo. Si noti che il metodo `ToString` non viene chiamato in modo esplicito nell'esempio. Il metodo <xref:System.Console.WriteLine%28System.Object%29?displayProperty=fullName> chiama in modo implicito il metodo `ToString` dell'oggetto passato come argomento.  
  
 [!code-csharp[Conceptual.Formatting.Overview#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/default1.cs#1)]
 [!code-vb[Conceptual.Formatting.Overview#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/default1.vb#1)]  
  
> [!WARNING]
>  A partire da [!INCLUDE[win81](../../../includes/win81-md.md)], [!INCLUDE[wrt](../../../includes/wrt-md.md)] include un'interfaccia [IStringable](http://msdn.microsoft.com/library/windows/apps/windows.foundation.istringable.aspx) con un solo metodo, [IStringable.ToString](http://msdn.microsoft.com/library/windows/apps/windows.foundation.istringable.tostring.aspx), che fornisce il supporto per la formattazione predefinito. È tuttavia consigliabile che i tipi gestiti non implementino l'interfaccia `IStringable`. Per altre informazioni, vedere la sezione "[!INCLUDE[wrt](../../../includes/wrt-md.md)] e l'interfaccia `IStringable`" nella pagina di riferimento <xref:System.Object.ToString%2A?displayProperty=fullName>.  
  
 Poiché tutti i tipi diversi dalle interfacce sono derivati da <xref:System.Object>, questa funzionalità viene fornita automaticamente alle classi o alle strutture personalizzate. La funzionalità offerta dal metodo `ToString` predefinito è tuttavia limitata poiché non fornisce informazioni su un'istanza del tipo sebbene consenta di identificarlo. Per fornire una rappresentazione di stringa di un oggetto che fornisce informazioni su tale oggetto, è necessario eseguire l'override del metodo `ToString`.  
  
> [!NOTE]
>  Le strutture ereditano dall'oggetto <xref:System.ValueType>, che a sua volta viene derivato da <xref:System.Object>. Sebbene <xref:System.ValueType> esegua l'override di <xref:System.Object.ToString%2A?displayProperty=fullName>, l'implementazione è identica.  
  
 [Torna all'inizio](#Introduction)  
  
<a name="OverrideToString"></a>   
## Override del metodo ToString  
 La visualizzazione del nome di un tipo ha spesso un uso limitato e non consente agli utenti dei tipi di distinguere tra le istanze. È tuttavia possibile eseguire l'override del metodo `ToString` per fornire una rappresentazione più utile del valore di un oggetto. Nell'esempio seguente viene definito un oggetto `Temperature` e viene eseguito l'override del relativo metodo `ToString` per visualizzare la temperatura in gradi Celsius.  
  
 [!code-csharp[Conceptual.Formatting.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/overrides1.cs#2)]
 [!code-vb[Conceptual.Formatting.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/overrides1.vb#2)]  
  
 In .NET Framework è stato eseguito l'override del metodo `ToString` di ogni tipo di valore primitivo per visualizzare il valore dell'oggetto anziché il relativo nome. Nella tabella seguente viene illustrato l'override per ogni tipo primitivo. Si noti che la maggior parte dei metodi sottoposti a override chiama un altro overload del metodo `ToString` e passa a esso l'identificatore di formato "G", che definisce il formato generale per il tipo, e un oggetto <xref:System.IFormatProvider>, che rappresenta le impostazioni cultura correnti.  
  
|Tipo|Override di ToString|  
|----------|--------------------------|  
|<xref:System.Boolean>|Restituisce <xref:System.Boolean.TrueString?displayProperty=fullName> o <xref:System.Boolean.FalseString?displayProperty=fullName>.|  
|<xref:System.Byte>|Chiama `Byte.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Byte> per le impostazioni cultura correnti.|  
|<xref:System.Char>|Restituisce il carattere come stringa.|  
|<xref:System.DateTime>|Chiama `DateTime.ToString("G", DatetimeFormatInfo.CurrentInfo)` per formattare il valore di data e ora per le impostazioni cultura correnti.|  
|<xref:System.Decimal>|Chiama `Decimal.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Decimal> per le impostazioni cultura correnti.|  
|<xref:System.Double>|Chiama `Double.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Double> per le impostazioni cultura correnti.|  
|<xref:System.Int16>|Chiama `Int16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Int16> per le impostazioni cultura correnti.|  
|<xref:System.Int32>|Chiama `Int32.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Int32> per le impostazioni cultura correnti.|  
|<xref:System.Int64>|Chiama `Int64.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Int64> per le impostazioni cultura correnti.|  
|<xref:System.SByte>|Chiama `SByte.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.SByte> per le impostazioni cultura correnti.|  
|<xref:System.Single>|Chiama `Single.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.Single> per le impostazioni cultura correnti.|  
|<xref:System.UInt16>|Chiama `UInt16.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.UInt16> per le impostazioni cultura correnti.|  
|<xref:System.UInt32>|Chiama `UInt32.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.UInt32> per le impostazioni cultura correnti.|  
|<xref:System.UInt64>|Chiama `UInt64.ToString("G", NumberFormatInfo.CurrentInfo)` per formattare il valore <xref:System.UInt64> per le impostazioni cultura correnti.|  
  
 [Torna all'inizio](#Introduction)  
  
<a name="FormatStrings"></a>   
## Metodo ToString e stringhe di formato  
 L'utilizzo del metodo `ToString` predefinito o l'esecuzione dell'override di `ToString` è un'operazione appropriata quando un oggetto dispone di una singola rappresentazione di stringa. Spesso, tuttavia, il valore di un oggetto dispone di più rappresentazioni. È ad esempio possibile esprimere una temperatura in gradi Fahrenheit, gradi Celsius o gradi Kelvin. Analogamente, il valore intero 10 può essere rappresentato in diversi modi, tra cui 10, 10,0, 1.0e01 o €10,00.  
  
 Per consentire a un singolo valore di disporre di più rappresentazioni di stringa, in .NET Framework vengono usate le stringhe di formato. Una stringa di formato è una stringa che contiene uno o più identificatori di formato predefiniti costituiti da singoli caratteri o gruppi di caratteri che definiscono il modo in cui deve essere formattato l'output del metodo `ToString`. La stringa di formato viene quindi passata come parametro al metodo `ToString` dell'oggetto per determinare come deve venire visualizzata la rappresentazione di stringa del valore di tale oggetto.  
  
 Tutti i tipi numerici, di data e ora e di enumerazione in .NET Framework supportano un set predefinito di identificatori di formato. È anche possibile usare le stringhe di formato per definire più rappresentazioni di stringa dei tipi di dati definiti dall'applicazione.  
  
<a name="standardStrings"></a>   
### Stringhe di formato standard  
 Una stringa di formato standard contiene un singolo identificatore di formato, che è un carattere alfabetico che definisce la rappresentazione di stringa dell'oggetto a cui viene applicata, insieme a un identificatore di precisione facoltativo, che influisce sul numero di cifre visualizzate nella stringa di risultato. Se l'identificatore di precisione viene omesso o non è supportato, un identificatore di formato standard è equivalente a una stringa di formato standard.  
  
 In .NET Framework viene definito un set di identificatori di formato standard per tutti i tipi numerici, di data e ora e di enumerazione. Ognuna di queste categorie supporta, ad esempio, un identificatore di formato standard "G", che definisce una rappresentazione di stringa generale di un valore di tale tipo.  
  
 Le stringhe di formato standard per i tipi di enumerazione controllano direttamente la rappresentazione di stringa di un valore. Le stringhe di formato passate al metodo `ToString` del valore di un'enumerazione determinano se il valore viene visualizzato tramite il relativo nome di stringa \(identificatori di formato "G" e "F"\), il relativo valore integrale sottostante \(identificatore di formato "D"\) oppure il relativo valore esadecimale \(identificatore di formato "X"\). Nell'esempio seguente viene illustrato l'uso delle stringhe di formato standard per formattare un valore dell'enumerazione <xref:System.DayOfWeek>.  
  
 [!code-csharp[Conceptual.Formatting.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/standard1.cs#4)]
 [!code-vb[Conceptual.Formatting.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/standard1.vb#4)]  
  
 Per informazioni sulle stringhe del formato di enumerazione, vedere [Stringhe di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md).  
  
 Le stringhe di formato standard per i tipi numerici definiscono in genere una stringa di risultato il cui aspetto preciso viene controllato da uno o più valori delle proprietà. L'identificatore di formato "C", ad esempio, consente di formattare un numero come valore di valuta. Quando si chiama il metodo `ToString` con l'identificatore di formato "C" come unico parametro, vengono usati i valori delle proprietà seguenti dell'oggetto <xref:System.Globalization.NumberFormatInfo> delle impostazioni cultura correnti per definire la rappresentazione di stringa del valore numerico:  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A>, che specifica il simbolo di valuta delle impostazioni cultura correnti.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A> o <xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern%2A>, che restituisce un valore intero che determina gli aspetti seguenti:  
  
    -   Posizione del simbolo di valuta.  
  
    -   Utilizzo di un segno negativo iniziale, di un segno negativo finale o di parentesi per indicare i valori negativi.  
  
    -   Inserimento di uno spazio tra il valore numerico e il simbolo di valuta.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A>, che definisce il numero di cifre frazionarie nella stringa di risultato.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A>, che definisce il simbolo del separatore decimale nella stringa di risultato.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A>, che definisce il simbolo del separatore di gruppi.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes%2A>, che definisce il numero di cifre in ogni gruppo a sinistra del separatore decimale.  
  
-   Proprietà <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>, che determina il segno negativo usato nella stringa di risultato se non vengono usate parentesi per indicare i valori negativi.  
  
 Le stringhe di formato numerico possono inoltre includere un identificatore di precisione. Il significato di questo identificatore dipende dalla stringa di formato con la quale viene usato, ma in genere esso indica il numero totale di cifre o il numero di cifre frazionarie che devono essere presenti nella stringa di risultato. Nell'esempio seguente vengono usati, ad esempio, la stringa numerica standard "X4"e un identificatore di precisione per creare un valore stringa con quattro cifre esadecimali.  
  
 [!code-csharp[Conceptual.Formatting.Overview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/precisionspecifier1.cs#6)]
 [!code-vb[Conceptual.Formatting.Overview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/precisionspecifier1.vb#6)]  
  
 Per altre informazioni sulle stringhe di formattazione numerica standard, vedere [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md).  
  
 Le stringhe di formato standard per i valori di data e ora sono alias per stringhe di formato personalizzate archiviate da una proprietà <xref:System.Globalization.DateTimeFormatInfo> specifica. Se viene chiamato, ad esempio, il metodo `ToString` di un valore di data e ora con l'identificatore di formato "D", la data e l'ora vengono visualizzate usando la stringa di formato personalizzata archiviata nella proprietà <xref:System.Globalization.DateTimeFormatInfo.LongDatePattern%2A?displayProperty=fullName> delle impostazioni cultura correnti. Per altre informazioni sulle stringhe di formato personalizzate, vedere la [sezione successiva](#customStrings). Nell'esempio seguente viene illustrata questa relazione.  
  
 [!code-csharp[Conceptual.Formatting.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/alias1.cs#5)]
 [!code-vb[Conceptual.Formatting.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/alias1.vb#5)]  
  
 Per altre informazioni sulle stringhe di formato di data e ora standard, vedere [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md).  
  
 È anche possibile usare le stringhe di formato standard per definire la rappresentazione di stringa di un oggetto definito dall'applicazione, prodotta dal metodo `ToString(String)` dell'oggetto. È possibile definire gli identificatori di formato standard specifici supportati dall'oggetto, nonché determinare se per essi viene fatta o meno distinzione tra maiuscole e minuscole. L'implementazione del metodo `ToString(String)` deve supportare gli elementi seguenti:  
  
-   Un identificatore di formato "G" che rappresenta un formato abituale o comune dell'oggetto. L'overload senza parametri del metodo `ToString` dell'oggetto deve chiamare il relativo overload di `ToString(String)` e passare a esso la stringa di formato standard "G".  
  
-   Supporto per un identificatore di formato equivalente a un riferimento Null \(`Nothing` in Visual Basic\). Un identificatore di formato equivalente a un riferimento Null deve essere considerato equivalente all'identificatore di formato "G".  
  
 Una classe `Temperature` può, ad esempio, archiviare internamente la temperatura in gradi Celsius e usare gli identificatori di formato per rappresentare il valore dell'oggetto `Temperature` in gradi Celsius, gradi Fahrenheit e gradi Kelvin. Nell'esempio seguente viene illustrato questo concetto.  
  
 [!code-csharp[Conceptual.Formatting.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/appstandard1.cs#7)]
 [!code-vb[Conceptual.Formatting.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/appstandard1.vb#7)]  
  
 [Torna all'inizio](#Introduction)  
  
<a name="customStrings"></a>   
### Stringhe di formato personalizzate  
 Oltre alle stringhe di formato standard, in .NET Framework sono definite stringhe di formato personalizzate sia per valori numerici che per valori di data e ora. Una stringa di formato personalizzata è costituita da uno o più identificatori di formato personalizzati che definiscono la rappresentazione di stringa di un valore. La stringa di formato di data e ora personalizzata "yyyy\/mm\/dd hh:mm:ss.ffff t zzz" consente, ad esempio, di convertire una data nella relativa rappresentazione di stringa nel formato "2008\/11\/15 07:45:00.0000 P \-08:00" per le impostazioni cultura en\-US. Analogamente, la stringa di formato personalizzata "0000" consente di convertire il valore intero 12 in "0012". Per un elenco completo di stringhe di formato personalizzate, vedere [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md) e [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md).  
  
 Se una stringa di formato è costituita da un solo identificatore di formato personalizzato, l'identificatore di formato deve essere preceduto dal simbolo di percentuale \(%\) per evitare confusione con un identificatore di formato standard. Nell'esempio seguente viene usato l'identificatore di formato personalizzato "M" per visualizzare un numero a una cifra o a due cifre del mese di una data specifica.  
  
 [!code-csharp[Conceptual.Formatting.Overview#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/singlecustom1.cs#8)]
 [!code-vb[Conceptual.Formatting.Overview#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/singlecustom1.vb#8)]  
  
 Numerose stringhe di formato standard per i valori di data e ora sono alias per stringhe di formato personalizzate definite dalle proprietà dell'oggetto <xref:System.Globalization.DateTimeFormatInfo>. Le stringhe di formato personalizzate offrono inoltre una notevole flessibilità in quanto consentono una formattazione definita dall'applicazione per valori numerici o di data e ora. È possibile definire stringhe di risultato personalizzate sia per valori numerici che per valori di data e ora combinando più identificatori di formato personalizzati in una singola stringa di formato personalizzata. Nell'esempio seguente viene definita una stringa di formato personalizzata che consente di visualizzare il giorno della settimana tra parentesi dopo il nome del mese, il giorno e l'anno.  
  
 [!code-csharp[Conceptual.Formatting.Overview#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/custom1.cs#9)]
 [!code-vb[Conceptual.Formatting.Overview#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/custom1.vb#9)]  
  
 L'esempio seguente definisce una stringa di formato personalizzata che visualizza un valore <xref:System.Int64> come numero di telefono degli Stati Uniti standard di sette cifre con il relativo prefisso.  
  
 [!code-csharp[Conceptual.Formatting.Overview#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/telnumber1.cs#21)]
 [!code-vb[Conceptual.Formatting.Overview#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/telnumber1.vb#21)]  
  
 Sebbene le stringhe di formato standard consentano in genere di gestire la maggior parte delle necessità relative alla formattazione per i tipi definiti dall'applicazione, è anche possibile definire identificatori di formato personalizzati per formattare i tipi.  
  
 [Torna all'inizio](#Introduction)  
  
<a name="stringRef"></a>   
### Stringhe di formato e tipi di libreria di classi .NET Framework  
 Tutti i tipi numerici, vale a dire i tipi <xref:System.Byte>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64> e <xref:System.Numerics.BigInteger>  
  
 , nonché <xref:System.DateTime>, <xref:System.DateTimeOffset>, <xref:System.TimeSpan>, <xref:System.Guid> e tutti i tipi di enumerazione supportano la formattazione con stringhe di formato. Per informazioni sulle stringhe di formato specifiche supportate da ogni tipo, vedere gli argomenti seguenti  
  
|Titolo|Definizione|  
|------------|-----------------|  
|[Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori numerici.|  
|[Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori numerici.|  
|[Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori <xref:System.DateTime>.|  
|[Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori <xref:System.DateTime>.|  
|[Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di intervalli di tempo.|  
|[Stringhe di formato TimeSpan personalizzate](../../../docs/standard/base-types/custom-timespan-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per intervalli di tempo.|  
|[Stringhe di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa di valori di enumerazione.|  
|<xref:System.Guid.ToString%28System.String%29?displayProperty=fullName>|Descrive le stringhe di formato standard per i valori <xref:System.Guid>.|  
  
<a name="FormatProviders"></a>   
## Formattazione dipendente dalle impostazioni cultura con provider di formato e l'interfaccia IFormatProvider  
 Sebbene gli identificatori di formato consentano di personalizzare la formattazione degli oggetti, la creazione di una rappresentazione di stringa significativa degli oggetti richiede spesso informazioni aggiuntive sulla formattazione. La formattazione, ad esempio, di un numero come valore di valuta tramite la stringa di formato standard "C" o una stringa di formato personalizzata, come ad esempio "$ \#,\#.00", richiede almeno la possibilità di includere nella stringa formattata le informazioni relative al simbolo di valuta, al separatore di gruppi e al separatore decimale corretti. In .NET Framework queste informazioni aggiuntive sulla formattazione vengono rese disponibili tramite l'interfaccia <xref:System.IFormatProvider>, fornita come parametro di uno o più overload del metodo `ToString` di tipi numerici e di data e ora. Le implementazioni di<xref:System.IFormatProvider> vengono usate in .NET Framework per supportare la formattazione specifica delle impostazioni cultura. Nell'esempio seguente viene illustrato come cambia la rappresentazione di stringa di un oggetto quando viene formattata con tre oggetti <xref:System.IFormatProvider> che rappresentano impostazioni cultura diverse.  
  
 [!code-csharp[Conceptual.Formatting.Overview#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformatprovider1.cs#11)]
 [!code-vb[Conceptual.Formatting.Overview#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformatprovider1.vb#11)]  
  
 L'interfaccia <xref:System.IFormatProvider> include un metodo, <xref:System.IFormatProvider.GetFormat%28System.Type%29>, che dispone di un singolo parametro che specifica il tipo di oggetto che fornisce informazioni sulla formattazione. Se il metodo può fornire un oggetto di tale tipo, lo restituisce. In caso contrario, restituisce un riferimento Null \(`Nothing` in Visual Basic\).  
  
 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> è un metodo di callback. Quando si chiama un overload del metodo `ToString` che include un parametro <xref:System.IFormatProvider>, viene chiamato il metodo <xref:System.IFormatProvider.GetFormat%2A> di tale oggetto <xref:System.IFormatProvider>. Il metodo <xref:System.IFormatProvider.GetFormat%2A> è responsabile della restituzione di un oggetto che fornisce le informazioni sulla formattazione necessarie, specificate dal relativo parametro `formatType`, al metodo `ToString`.  
  
 Diversi metodi di conversione di stringhe o di formattazione includono un parametro di tipo <xref:System.IFormatProvider>, ma in molti casi il valore del parametro viene ignorato quando il metodo viene chiamato. Nella tabella seguente sono elencati alcuni dei metodi di formattazione che usano il parametro e il tipo dell'oggetto <xref:System.Type> che passano al metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName>.  
  
|Metodo|Tipo di parametro `formatType`|  
|------------|------------------------------------|  
|Metodo `ToString` di tipi numerici|<xref:System.Globalization.NumberFormatInfo?displayProperty=fullName>|  
|Metodo `ToString` di tipi di data e ora|<xref:System.Globalization.DateTimeFormatInfo?displayProperty=fullName>|  
|<xref:System.String.Format%2A?displayProperty=fullName>|<xref:System.ICustomFormatter?displayProperty=fullName>|  
|<xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>|<xref:System.ICustomFormatter?displayProperty=fullName>|  
  
> [!NOTE]
>  I metodi `ToString` dei tipi numerici e di data e ora sono sottoposti a overload e solo alcuni degli overload includono un parametro <xref:System.IFormatProvider>. Se un metodo non dispone di un parametro di tipo <xref:System.IFormatProvider>, al suo posto viene passato l'oggetto restituito dalla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>. Una chiamata al metodo <xref:System.Int32.ToString?displayProperty=fullName> predefinito comporta, ad esempio, in definitiva, una chiamata al metodo come la seguente: `Int32.ToString("G", System.Globalization.CultureInfo.CurrentCulture)`.  
  
 In .NET Framework sono disponibili tre classi che implementano <xref:System.IFormatProvider>:  
  
-   <xref:System.Globalization.DateTimeFormatInfo>, una classe che fornisce informazioni sulla formattazione per i valori di data e ora per impostazioni cultura specifiche. L'implementazione del metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> della classe restituisce un'istanza della classe stessa.  
  
-   <xref:System.Globalization.NumberFormatInfo>, una classe che fornisce informazioni sulla formattazione numerica per impostazioni cultura specifiche. L'implementazione del metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> della classe restituisce un'istanza della classe stessa.  
  
-   <xref:System.Globalization.CultureInfo>. L'implementazione del metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> della classe può restituire un oggetto <xref:System.Globalization.NumberFormatInfo> per fornire informazioni sulla formattazione numerica o un oggetto <xref:System.Globalization.DateTimeFormatInfo> per fornire informazioni sulla formattazione per i valori di data e ora.  
  
 È anche possibile implementare un provider di formato personalizzato per sostituire una di queste classi. Il metodo <xref:System.IFormatProvider.GetFormat%2A> dell'implementazione, tuttavia, deve restituire un oggetto del tipo elencato nella tabella precedente, se deve fornire informazioni sulla formattazione al metodo `ToString`.  
  
 [Torna all'inizio](#Introduction)  
  
<a name="numericCulture"></a>   
### Formattazione dipendente dalle impostazioni cultura di valori numerici  
 Per impostazione predefinita, la formattazione di valori numerici è dipendente dalle impostazioni cultura. Se non si specificano impostazioni cultura quando si chiama un metodo di formattazione, vengono usate le convenzioni di formattazione delle impostazioni cultura del thread corrente. Questa situazione viene illustrata nell'esempio seguente in cui le impostazioni cultura del thread corrente vengono modificate quattro volte e viene chiamato il metodo <xref:System.Decimal.ToString%28System.String%29?displayProperty=fullName>. In ogni caso, la stringa risultante riflette le convenzioni di formattazione delle impostazioni cultura correnti. Questo accade perché i metodi `ToString` e `ToString(String)` eseguono il wrapping di chiamate al metodo `ToString(String, IFormatProvider)` di ogni tipo numerico.  
  
 [!code-csharp[Conceptual.Formatting.Overview#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific3.cs#19)]
 [!code-vb[Conceptual.Formatting.Overview#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific3.vb#19)]  
  
 È anche possibile formattare un valore numerico per impostazioni cultura specifiche chiamando un overload di `ToString` con un parametro `provider` e passando uno degli elementi seguenti:  
  
-   Oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura, di cui verranno usate le convenzioni di formattazione. Il metodo <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=fullName> relativo restituisce il valore della proprietà <xref:System.Globalization.CultureInfo.NumberFormat%2A?displayProperty=fullName>, che rappresenta l'oggetto <xref:System.Globalization.NumberFormatInfo> che fornisce informazioni di formattazione specifiche delle impostazioni cultura per i valori numerici.  
  
-   Oggetto <xref:System.Globalization.NumberFormatInfo> che definisce le convenzioni di formattazione specifiche delle impostazioni cultura da usare. Il metodo <xref:System.Globalization.NumberFormatInfo.GetFormat%2A> relativo restituisce un'istanza di se stesso.  
  
 Nell'esempio seguente vengono usati gli oggetti <xref:System.Globalization.NumberFormatInfo> che rappresentano le impostazioni cultura della lingua inglese di Stati Uniti e di Gran Bretagna, nonché le impostazioni cultura non associate alle lingue francese e russa per formattare un numero a virgola mobile.  
  
 [!code-csharp[Conceptual.Formatting.Overview#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific4.cs#20)]
 [!code-vb[Conceptual.Formatting.Overview#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific4.vb#20)]  
  
<a name="dateCulture"></a>   
### Formattazione dipendente dalle impostazioni cultura di valori data e ora  
 Per impostazione predefinita, la formattazione dei valori data e ora è dipendente dalle impostazioni cultura. Se non si specificano impostazioni cultura quando si chiama un metodo di formattazione, vengono usate le convenzioni di formattazione delle impostazioni cultura del thread corrente. Questa situazione viene illustrata nell'esempio seguente in cui le impostazioni cultura del thread corrente vengono modificate quattro volte e viene chiamato il metodo <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName>. In ogni caso, la stringa risultante riflette le convenzioni di formattazione delle impostazioni cultura correnti. Questo si verifica perché i metodi <xref:System.DateTime.ToString?displayProperty=fullName>, <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName>, <xref:System.DateTimeOffset.ToString?displayProperty=fullName>e <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> eseguono il wrapping di chiamate ai metodi <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> e <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName>.  
  
 [!code-csharp[Conceptual.Formatting.Overview#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific1.cs#17)]
 [!code-vb[Conceptual.Formatting.Overview#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific1.vb#17)]  
  
 È anche possibile formattare un valore data e ora per impostazioni cultura specifiche chiamando un overload <xref:System.DateTime.ToString%2A?displayProperty=fullName> o <xref:System.DateTimeOffset.ToString%2A?displayProperty=fullName> contenente un parametro `provider` e passandolo agli elementi seguenti:  
  
-   Oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura, di cui verranno usate le convenzioni di formattazione. Il metodo <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=fullName> restituisce il valore della proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>, che rappresenta l'oggetto <xref:System.Globalization.DateTimeFormatInfo> che fornisce informazioni di formattazione specifiche delle impostazioni cultura per valori data e ora.  
  
-   Oggetto <xref:System.Globalization.DateTimeFormatInfo> che definisce le convenzioni di formattazione specifiche delle impostazioni cultura da usare. Il metodo <xref:System.Globalization.DateTimeFormatInfo.GetFormat%2A> relativo restituisce un'istanza di se stesso.  
  
 Nell'esempio seguente vengono usati gli oggetti <xref:System.Globalization.DateTimeFormatInfo> che rappresentano le impostazioni cultura della lingua inglese di Stati Uniti e Gran Bretagna e le impostazioni cultura non associate alle lingue francese e russa per formattare una data.  
  
 [!code-csharp[Conceptual.Formatting.Overview#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/culturespecific2.cs#18)]
 [!code-vb[Conceptual.Formatting.Overview#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/culturespecific2.vb#18)]  
  
<a name="IFormattable"></a>   
## Interfaccia IFormattable  
 In genere, i tipi che eseguono l'overload del metodo `ToString` con una stringa di formato e un parametro <xref:System.IFormatProvider> implementano anche l'interfaccia <xref:System.IFormattable>. Questa interfaccia dispone di un singolo membro, <xref:System.IFormattable.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName>, che include sia una stringa di formato che un provider di formato come parametri.  
  
 L'implementazione dell'interfaccia <xref:System.IFormattable> per la classe definita dall'applicazione offre due vantaggi:  
  
-   Supporto per la conversione di stringhe da parte della classe <xref:System.Convert>. Le chiamate ai metodi <xref:System.Convert.ToString%28System.Object%29?displayProperty=fullName> e <xref:System.Convert.ToString%28System.Object%2CSystem.IFormatProvider%29?displayProperty=fullName> comportano una chiamata direttamente all'implementazione di <xref:System.IFormattable>.  
  
-   Supporto per la formattazione composita. Se viene usato un elemento di formato che include una stringa di formato per formattare il tipo personalizzato, tramite Common Language Runtime viene chiamata automaticamente l'implementazione di <xref:System.IFormattable>, che viene passata alla stringa di formato. Per altre informazioni sulla formattazione composita con metodi come <xref:System.String.Format%2A?displayProperty=fullName> o <xref:System.Console.WriteLine%2A?displayProperty=fullName>, vedere la sezione [Formattazione composita](#CompositeFormatting).  
  
 Nell'esempio seguente viene definita una classe `Temperature` che implementa l'interfaccia <xref:System.IFormattable>. Sono supportati gli identificatori di formato "C" e "G" per visualizzare la temperatura in Celsius, l'identificatore di formato "F" per visualizzare la temperatura in Fahrenheit e l'identificatore di formato "K" per visualizzare la temperatura in Kelvin.  
  
 [!code-csharp[Conceptual.Formatting.Overview#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformattable.cs#12)]
 [!code-vb[Conceptual.Formatting.Overview#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformattable.vb#12)]  
  
 Nell'esempio seguente viene creata un'istanza di un oggetto `Temperature`. Viene quindi chiamato il metodo <xref:System.Convert.ToString%2A> e vengono usate diverse stringhe di formato composite per ottenere diverse rappresentazioni di stringa di un oggetto `Temperature`. Ognuna di queste chiamate al metodo chiama, a sua volta, l'implementazione di <xref:System.IFormattable> della classe `Temperature`.  
  
 [!code-csharp[Conceptual.Formatting.Overview#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/iformattable.cs#13)]
 [!code-vb[Conceptual.Formatting.Overview#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/iformattable.vb#13)]  
  
 [Torna all'inizio](#Introduction)  
  
<a name="CompositeFormatting"></a>   
## Formattazione composita  
 Alcuni metodi, ad esempio <xref:System.String.Format%2A?displayProperty=fullName> e <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>, supportano la formattazione composita. Una stringa di formato composita è un tipo di modello che restituisce una singola stringa che incorpora la rappresentazione di stringa di zero, uno o più oggetti. Ogni oggetto è rappresentato nella stringa di formato composita da un elemento di formato indicizzato. L'indice dell'elemento di formato corrisponde alla posizione dell'oggetto che esso rappresenta nell'elenco di parametri del metodo. Gli indici sono a base zero. Nella chiamata seguente al metodo <xref:System.String.Format%2A?displayProperty=fullName>, ad esempio, il primo elemento di formato, `{0:D}`, viene sostituito dalla rappresentazione di stringa `thatDate`, il secondo elemento di formato, `{1}`, viene sostituito dalla rappresentazione di stringa `item1` e il terzo elemento di formato, `{2:C2}`, viene sostituito dalla rappresentazione di stringa `item1.Value`.  
  
 [!code-csharp[Conceptual.Formatting.Overview#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/composite1.cs#14)]
 [!code-vb[Conceptual.Formatting.Overview#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/composite1.vb#14)]  
  
 Oltre a sostituire un elemento di formato con la rappresentazione di stringa dell'oggetto corrispondente, gli elementi di formato consentono anche di controllare gli aspetti seguenti:  
  
-   Il modo specifico in cui un oggetto è rappresentato come stringa, se l'oggetto implementa l'interfaccia <xref:System.IFormattable> e supporta le stringhe di formato. A tale scopo, dopo l'indice dell'elemento di formato è necessario aggiungere un simbolo `:` \(due punti\) seguito da una stringa di formato valida. Nell'esempio precedente viene eseguita questa operazione formattando un valore di data con la stringa di formato "d" \(modello di data breve\) \(ad esempio, `{0:d}`\) e formattando un valore numerico con la stringa di formato "C2" \(ad esempio, `{2:C2}`\) per rappresentare il numero come valore di valuta con due cifre decimali frazionarie.  
  
-   La larghezza del campo che contiene la rappresentazione di stringa dell'oggetto e l'allineamento della rappresentazione di stringa in tale campo. A tale scopo, dopo l'indice dell'elemento di formato è necessario aggiungere un simbolo `,` \(virgola\) seguito dalla larghezza del campo. La stringa viene allineata a destra nel campo se la larghezza del campo è un valore positivo e viene allineata a sinistra se la larghezza del campo è un valore negativo. L'esempio seguente consente di allineare a sinistra i valori di data in un campo di 20 caratteri e di allineare a destra i valori decimali con una cifra frazionaria in un campo di 11 caratteri.  
  
     [!code-csharp[Conceptual.Formatting.Overview#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/composite2.cs#22)]
     [!code-vb[Conceptual.Formatting.Overview#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/composite2.vb#22)]  
  
     Si noti che, se il componente stringa di allineamento e il componente stringa di formato sono entrambi presenti, il primo precede il secondo, ad esempio `{0,-20:g}`.  
  
 Per altre informazioni sulla formattazione composita, vedere [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md).  
  
 [Torna all'inizio](#Introduction)  
  
<a name="Custom"></a>   
## Formattazione personalizzata con ICustomFormatter  
 Due metodi di formattazione compositi, [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> e [StringBuilder.AppendFormat\(IFormatProvider, String, Object\<xref:System.Text.StringBuilder.AppendFormat%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, includono un parametro del provider di formato che supporta la formattazione personalizzata. Quando viene chiamato uno di questi metodi di formattazione, viene passato un oggetto <xref:System.Type> che rappresenta un'interfaccia <xref:System.ICustomFormatter> al metodo <xref:System.IFormatProvider.GetFormat%2A> del provider di formato. Il metodo <xref:System.IFormatProvider.GetFormat%2A> è quindi responsabile della restituzione dell'implementazione di <xref:System.ICustomFormatter> che fornisce formattazione personalizzata.  
  
 L'interfaccia <xref:System.ICustomFormatter> dispone di un singolo metodo, <xref:System.ICustomFormatter.Format%28System.String%2CSystem.Object%2CSystem.IFormatProvider%29>, chiamato automaticamente da un metodo di formattazione composita una volta per ogni elemento di formato in una stringa di formato composita. Il metodo <xref:System.ICustomFormatter.Format%28System.String%2CSystem.Object%2CSystem.IFormatProvider%29> dispone di tre parametri: una stringa di formato, che rappresenta l'argomento `formatString` in un elemento di formato, un oggetto da formattare e un oggetto <xref:System.IFormatProvider> che fornisce i servizi di formattazione. In genere, la classe che implementa <xref:System.ICustomFormatter> implementa anche <xref:System.IFormatProvider>, pertanto quest'ultimo parametro è un riferimento alla classe di formattazione personalizzata stessa. Questo metodo restituisce una rappresentazione di stringa formattata personalizzata dell'oggetto da formattare. Se il metodo non è in grado di formattare l'oggetto, deve restituire un riferimento Null \(`Nothing` in Visual Basic\).  
  
 Nell'esempio seguente viene fornita un'implementazione di <xref:System.ICustomFormatter> denominata `ByteByByteFormatter` che consente di visualizzare i valori interi come sequenza di valori esadecimali a due cifre seguiti da uno spazio.  
  
 [!code-csharp[Conceptual.Formatting.Overview#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/icustomformatter1.cs#15)]
 [!code-vb[Conceptual.Formatting.Overview#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/icustomformatter1.vb#15)]  
  
 Nell'esempio seguente viene usata la classe `ByteByByteFormatter` per formattare valori interi. Si noti che il metodo <xref:System.ICustomFormatter.Format%2A?displayProperty=fullName> viene chiamato più di una volta nella seconda chiamata al metodo [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> e che il provider <xref:System.Globalization.NumberFormatInfo> predefinito viene usato nella terza chiamata al metodo, in quanto il metodo `ByteByByteFormatter.Format` non riconosce la stringa di formato "N0" e restituisce un riferimento Null \(`Nothing` in Visual Basic\).  
  
 [!code-csharp[Conceptual.Formatting.Overview#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.formatting.overview/cs/icustomformatter1.cs#16)]
 [!code-vb[Conceptual.Formatting.Overview#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.formatting.overview/vb/icustomformatter1.vb#16)]  
  
 [Torna all'inizio](#Introduction)  
  
<a name="RelatedTopics"></a>   
## Argomenti correlati  
  
|Titolo|Definizione|  
|------------|-----------------|  
|[Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori numerici.|  
|[Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori numerici.|  
|[Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di valori <xref:System.DateTime>.|  
|[Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per valori <xref:System.DateTime>.|  
|[Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa usate comunemente di intervalli di tempo.|  
|[Stringhe di formato TimeSpan personalizzate](../../../docs/standard/base-types/custom-timespan-format-strings.md)|Vengono descritte le stringhe di formato personalizzate che consentono di creare formati specifici dell'applicazione per intervalli di tempo.|  
|[Stringhe di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md)|Vengono descritte le stringhe di formato standard che consentono di creare rappresentazioni di stringa di valori di enumerazione.|  
|[Formattazione composita](../../../docs/standard/base-types/composite-formatting.md)|Viene descritto come incorporare uno o più valori formattati in una stringa, che successivamente può essere visualizzata nella console oppure scritta in un flusso.|  
|[Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)|Sono elencati gli argomenti contenenti istruzioni dettagliate per l'esecuzione di operazioni di formattazione specifiche.|  
|[Analisi di stringhe](../../../docs/standard/base-types/parsing-strings.md)|Viene descritta l'inizializzazione di oggetti sui valori descritti dalle rappresentazioni in forma di stringa di tali oggetti. L'analisi è l'operazione contraria alla formattazione.|  
  
 [Torna all'inizio](#Introduction)  
  
<a name="Reference"></a>   
## Riferimento  
 <xref:System.IFormattable?displayProperty=fullName>  
  
 <xref:System.IFormatProvider?displayProperty=fullName>  
  
 <xref:System.ICustomFormatter?displayProperty=fullName>