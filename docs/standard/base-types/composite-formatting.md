---
title: "Formattazione composita | Microsoft Docs"
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
  - "formattazione composta"
  - "identificatori di formato, formattazione composta"
  - "oggetti [.NET Framework], formattazione di più oggetti"
  - "identificatori di parametro"
  - "stringhe [.NET Framework], allineamento"
  - "stringhe [.NET Framework], composte"
ms.assetid: 87b7d528-73f6-43c6-b71a-f23043039a49
caps.latest.revision: 36
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 33
---
# Formattazione composita
La funzionalità di formattazione composta di .NET Framework consente di usare come input un elenco di oggetti e una stringa di formato composto.  Una stringa di formato composto è costituita da testo fisso alternato a segnaposto indicizzati, denominati elementi di formato, che corrispondono agli oggetti dell'elenco.  L'operazione di formattazione produce una stringa risultato costituita dal testo fisso originale alternato alla rappresentazione di stringa degli oggetti dell'elenco.  
  
 La funzionalità di formattazione composita è supportata da metodi quali i seguenti:  
  
-   <xref:System.String.Format%2A?displayProperty=fullName>, che restituisce una stringa di risultato formattata.  
  
-   <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=fullName>, che aggiunge una stringa di risultato formattata a un oggetto <xref:System.Text.StringBuilder>.  
  
-   Alcuni overload del metodo di <xref:System.Console.WriteLine%2A?displayProperty=fullName>, che visualizza una stringa di risultato formattata nella console.  
  
-   Alcuni overload del metodo di <xref:System.IO.TextWriter.WriteLine%2A?displayProperty=fullName>, che visualizza una stringa di risultato formattata in un flusso o in un file.  Le classi derivate da <xref:System.IO.TextWriter>, come <xref:System.IO.StreamWriter> e <xref:System.Web.UI.HtmlTextWriter>, condividono questa funzionalità.  
  
-   [Debug.WriteLine\(String, Object\<xref:System.Diagnostics.Debug.WriteLine%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, che restituisce un messaggio formattato nei listener di traccia.  
  
-   Metodi [Trace.TraceError\(String, Object\<xref:System.Diagnostics.Trace.TraceError%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, [Trace.TraceInformation\(String, Object\<xref:System.Diagnostics.Trace.TraceInformation%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> e [Trace.TraceWarning\(String, Object\<xref:System.Diagnostics.Trace.TraceWarning%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, che restituiscono messaggi formattati nei listener di traccia.  
  
-   Metodo di [TraceSource.TraceInformation\(String, Object\<xref:System.Diagnostics.TraceSource.TraceInformation%28System.String%2CSystem.Object%5B%5D%29?displayProperty=fullName>, che scrive un metodo informativo nei listener di traccia.  
  
## Stringa di formato composto  
 Una stringa di formato composto e un elenco di oggetti vengono usati come argomenti di metodi che supportano la funzionalità di formattazione composta.  Una stringa di formato composto è costituita da zero o più esecuzioni di testo fisso alternate a uno o più elementi di formato.  Il testo fisso corrisponde a una stringa di propria scelta e ogni elemento di formato corrisponde a un oggetto o una struttura boxed dell'elenco.  La funzionalità di formattazione composta restituisce una nuova stringa risultato in cui ciascun elemento di formato viene sostituito dalla rappresentazione di stringa di origine dell'oggetto corrispondente dell'elenco.  
  
 Si consideri il frammento di codice <xref:System.String.Format%2A> riportato di seguito.  
  
 [!code-csharp[Formatting.Composite#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#1)]
 [!code-vb[Formatting.Composite#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#1)]  
  
 Il testo fisso è "`Name =` " e "`, hours =` ".  Gli elementi di formato sono "`{0}`", il cui indice è 0, che corrisponde all'elemento  `myName` dell'oggetto, e "`{1:hh}`", il cui indice è 1, che corrisponde all'elemento `DateTime.Now` dell'oggetto.  
  
## Sintassi degli elementi di formato  
 Ogni elemento di formato usa il formato seguente ed è costituito dai componenti riportati di seguito:  
  
 `{` *indice*\[`,`*allineamento*\]\[`:`*StringaFormato*\]`}`  
  
 Le parentesi graffe corrispondenti "{" e "}" sono obbligatorie.  
  
### Componente di indice  
 Il componente obbligatorio *indice*, denominato anche identificatore di parametro, corrisponde a un numero a partire da 0 che identifica un elemento corrispondente nell'elenco di oggetti.  Con l'elemento di formato con identificatore di parametro 0 viene formattato il primo oggetto dell'elenco, con l'elemento di formato con identificatore di parametro 1 viene formattato il secondo oggetto dell'elenco e così via.  L'esempio seguente include cinque identificatori di parametro per rappresentare i numeri primi inferiori a dieci:  
  
 [!code-csharp[Formatting.Composite#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/index1.cs#7)]
 [!code-vb[Formatting.Composite#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/index1.vb#7)]  
  
 Più elementi di formato possono fare riferimento allo stesso elemento dell'elenco di oggetti specificando lo stesso identificatore di parametro.  È ad esempio possibile formattare lo stesso valore numerico in formato esadecimale, scientifico e numerico specificando una stringa di formato composto "0x{0:X} {0:E} {0:N}", come nell'esempio seguente.  
  
 [!code-csharp[Formatting.Composite#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/index1.cs#10)]
 [!code-vb[Formatting.Composite#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/index1.vb#10)]  
  
 Ogni elemento di formato può fare riferimento a un oggetto dell'elenco.  Se ad esempio sono presenti tre oggetti, è possibile formattare il secondo, il primo e il terzo oggetto specificando una stringa di formato composto "{1} {0} {2}".  Gli oggetti a cui non fa riferimento un elemento di formato vengono ignorati.  Se un identificatore di parametro corrisponde a un elemento non incluso nei limiti dell'elenco di oggetti, verrà generata un'eccezione <xref:System.FormatException> in fase di esecuzione.  
  
### Componente di allineamento  
 Il componente facoltativo *allineamento* corrisponde a un valore Integer con segno che indica la larghezza preferita del campo formattato.  Se il valore di *allineamento* è inferiore alla lunghezza della stringa formattata, il componente *allineamento*verrà ignorato e come larghezza del campo verrà usata la lunghezza della stringa.  I dati formattati verranno allineati a destra se il valore di *allineamento* è positivo e a sinistra se il valore di *allineamento* è negativo.  Per la spaziatura eventualmente necessaria verranno usati spazi vuoti.  Se viene specificato il componente *allineamento*, la virgola è obbligatoria.  
  
 L'esempio seguente definisce due matrici, una contenente i nomi dei dipendenti e l'altra contenente il numero di ore in cui hanno lavorato per un periodo di due settimane.  La stringa di formato composto allinea a sinistra i nomi in un campo di 20 caratteri e allinea a destra le ore in un campo di 5 caratteri.  Si noti che la stringa di formato standard "N1" viene usata anche per formattare le ore con una cifra frazionaria.  
  
 [!code-csharp[Formatting.Composite#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/alignment1.cs#8)]
 [!code-vb[Formatting.Composite#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/alignment1.vb#8)]  
  
### Componente della stringa di formato  
 Il componente *StringaFormato* facoltativo è una stringa di formato appropriata per il tipo di oggetto formattato.  Specificare una stringa di formato numerico standard o personalizzata se l'oggetto corrispondente è un valore numerico, una stringa di formato di data e ora standard o personalizzata se l'oggetto corrispondente è un oggetto <xref:System.DateTime> o una [stringa di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md) se l'oggetto corrispondente è un valore di enumerazione.  Se il componente *StringaFormato* viene omesso, verrà usato l'identificatore di formato generale "G" per un tipo numerico, di data e ora o di enumerazione.  Se viene specificato il componente *StringaFormato*, i due punti sono obbligatori.  
  
 Nella tabella seguente sono elencati i tipi o le categorie di tipi della libreria di classi .NET Framework che supportano un set predefinito di stringhe di formato e vengono forniti collegamenti ad argomenti in cui vengono elencate le stringhe di formato supportate.  Si noti che la formattazione delle stringhe è un meccanismo estendibile che consente di definire nuove stringhe di formato per tutti i tipi esistenti nonché definire un set di stringhe di formato supportate da un tipo definito dall'applicazione.  Per altre informazioni, vedere gli argomenti delle interfacce <xref:System.IFormattable> e <xref:System.ICustomFormatter>.  
  
|Tipo o categoria di tipo|Vedere|  
|------------------------------|------------|  
|Tipi di data e ora \(<xref:System.DateTime>, <xref:System.DateTimeOffset>\)|[Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)<br /><br /> [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)|  
|Tipi di enumerazione \(tutti derivati da <xref:System.Enum?displayProperty=fullName>\)|[Stringhe di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md)|  
|Tipi numerici \(<xref:System.Numerics.BigInteger>, <xref:System.Byte>, <xref:System.Decimal>, <xref:System.Double>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.SByte>, <xref:System.Single>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>\)|[Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)<br /><br /> [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md)|  
|<xref:System.Guid>|<xref:System.Guid.ToString%28System.String%29?displayProperty=fullName>|  
|<xref:System.TimeSpan>|[Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)<br /><br /> [Stringhe di formato TimeSpan personalizzate](../../../docs/standard/base-types/custom-timespan-format-strings.md)|  
  
### Sequenze di escape delle parentesi graffe  
 Le parentesi graffe di apertura e di chiusura sono interpretate come l'inizio e la fine di un elemento di formato.  Di conseguenza, è necessario usare una sequenza di escape per visualizzare una parentesi graffa di apertura o di chiusura letterale.  Specificare due parentesi graffe di apertura \("{{"\) nel testo fisso per visualizzare una parentesi di apertura \("{"\) oppure due parentesi graffe di chiusura \("}}"\) per visualizzare una parentesi graffa di chiusura \("}"\).  Le parentesi graffe in un elemento di formato vengono interpretate sequenzialmente nell'ordine in cui sono rilevate.  L'interpretazione delle parentesi graffe annidate non è supportata.  
  
 Il tipo di interpretazione delle parentesi graffe in sequenza di escape può produrre risultati imprevisti.  Si consideri, ad esempio, l'elemento di formato "{{{0:D}}}", destinato alla visualizzazione di una parentesi graffa di apertura, un valore numerico formattato come numero decimale e una parentesi graffa di chiusura.  L'elemento di formato viene tuttavia interpretato nel modo seguente:  
  
1.  Le prime due parentesi apertura \("{{"\) presentano una sequenza di escape e producono una parentesi graffa di apertura.  
  
2.  I tre caratteri successivi \("{0:"\) sono interpretati come l'inizio di un elemento di formato.  
  
3.  Il carattere successivo \("D"\) verrebbe interpretato come identificatore del formato numerico standard Decimal, ma le due parentesi graffe successive con sequenza di escape \("}}"\) producono una parentesi graffa singola.  Poiché la stringa risultante \("D}"\) non è un identificatore di un formato numerico standard, viene interpretata come una stringa di formato personalizzata che indica la visualizzazione della stringa letterale "D}".  
  
4.  L'ultima parentesi graffa \("}"\) viene interpretata come la fine dell'elemento di formato.  
  
5.  Il risultato finale visualizzato è la stringa letterale "{D}".  Il valore numerico da formattare non viene visualizzato.  
  
 Per evitare di interpretare in modo errato gli elementi di formato e le parentesi graffe con sequenza di escape, è preferibile formattarli separatamente, ovvero  nella prima operazione di formattazione visualizzare una parentesi graffa di apertura letterale, nella successiva operazione visualizzare il risultato dell'elemento di formato, quindi nell'ultima operazione visualizzare una parentesi graffa di chiusura letterale.  Questo approccio viene illustrato nell'esempio seguente:  
  
 [!code-csharp[Formatting.Composite#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Escaping1.cs#2)]
 [!code-vb[Formatting.Composite#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Escaping1.vb#2)]  
  
### Ordine di elaborazione  
 Se la chiamata al metodo di formattazione composita include un argomento <xref:System.IFormatProvider> il cui valore non è `null`, il runtime chiama il metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> per richiedere un'implementazione di <xref:System.ICustomFormatter>.  Se il metodo può restituire un'implementazione di <xref:System.ICustomFormatter>, viene memorizzato nella cache per un utilizzo successivo.  
  
 Ogni valore nell'elenco di parametri che corrisponde a un elemento di formato viene convertito in una stringa, attenendosi alla procedura seguente.  Se una condizione qualsiasi nei primi tre passaggi è true, la rappresentazione in formato stringa del valore viene restituita in tale passaggio e i passaggi successivi non vengono eseguiti.  
  
1.  Se il valore da formattare è `null`, viene restituita una stringa vuota \(""\).  
  
2.  Se l'implementazione di <xref:System.ICustomFormatter> è disponibile, il runtime chiama il metodo <xref:System.ICustomFormatter.Format%2A>.  Passa al metodo il valore *StringaFormato* dell'elemento di formato, se disponibile, o `null` caso contrario, con l'implementazione di <xref:System.IFormatProvider>.  
  
3.  Se il valore implementa l'interfaccia <xref:System.IFormattable>, verrà chiamato il relativo metodo <xref:System.IFormattable.ToString%28System.String%2CSystem.IFormatProvider%29>.  Al metodo viene passato il valore *StringaFormato*, se disponibile nell'elemento di formato, o `null` in caso contrario.  L'argomento <xref:System.IFormatProvider> è determinato come segue:  
  
    -   Per un valore numerico, se viene chiamato un metodo di formattazione composita con un argomento non Null <xref:System.IFormatProvider>, il runtime richiede un oggetto <xref:System.Globalization.NumberFormatInfo> dal relativo metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName>.  Se non è in grado di fornirne uno, se il valore dell'argomento è `null` o se il metodo di formattazione composita non dispone di un parametro di <xref:System.IFormatProvider>, viene usato l'oggetto <xref:System.Globalization.NumberFormatInfo> per le impostazioni cultura del thread corrente.  
  
    -   Per un valore di data e ora, se viene chiamato un metodo di formattazione composita con un argomento non Null <xref:System.IFormatProvider>, il runtime richiede un oggetto <xref:System.Globalization.DateTimeFormatInfo> dal relativo metodo <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName>.  Se non è in grado di fornirne uno, se il valore dell'argomento è `null` o se il metodo di formattazione composita non dispone di un parametro di <xref:System.IFormatProvider>, viene usato l'oggetto <xref:System.Globalization.DateTimeFormatInfo> per le impostazioni cultura del thread corrente.  
  
    -   Per gli oggetti di altri tipi, se una formattazione composita viene chiamata con un argomento <xref:System.IFormatProvider>, il relativo valore \(incluso `null`, se no viene fornito alcun oggetto <xref:System.IFormatProvider>\) viene passato direttamente all'implementazione di <xref:System.IFormattable.ToString%2A?displayProperty=fullName>.  In caso contrario, un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura del thread corrente viene passato all'implementazione di <xref:System.IFormattable.ToString%2A?displayProperty=fullName>.  
  
4.  Viene chiamato il metodo senza parametri `ToString` del tipo, che esegue l'override di <xref:System.Object.ToString?displayProperty=fullName> o eredita il comportamento della relativa classe di base.  In questo caso, la stringa di formato specificata dal componente *StringaFormato* nell'elemento di formato, se presente, viene ignorata.  
  
 L'allineamento viene applicato al termine dei precedenti passaggi.  
  
## Esempi di codice  
 Nell'esempio seguente vengono illustrate una stringa creata con la formattazione composita e un'altra creata mediante il metodo `ToString` di un oggetto.  Entrambi i tipi di formattazione producono risultati equivalenti.  
  
 [!code-csharp[Formatting.Composite#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#3)]
 [!code-vb[Formatting.Composite#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#3)]  
  
 Presupponendo che il giorno corrente sia un giovedì di maggio, il valore di entrambe le stringhe dell'esempio precedente sarà `Thursday May` se sono specificate le impostazioni cultura  inglesi.  
  
 <xref:System.Console.WriteLine%2A?displayProperty=fullName> espone la stessa funzionalità di <xref:System.String.Format%2A?displayProperty=fullName>.  L'unica differenza tra i due metodi è che <xref:System.String.Format%2A?displayProperty=fullName> restituisce il risultato come stringa, mentre <xref:System.Console.WriteLine%2A?displayProperty=fullName> scrive il risultato nel flusso di output associato all'oggetto <xref:System.Console>.  Nell'esempio seguente viene usato il metodo <xref:System.Console.WriteLine%2A?displayProperty=fullName> per formattare il valore di `MyInt` come valore di valuta.  
  
 [!code-csharp[Formatting.Composite#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#4)]
 [!code-vb[Formatting.Composite#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#4)]  
  
 Nell'esempio riportato di seguito vengono illustrate la formattazione di più oggetti e la formattazione di un oggetto in due diversi modi.  
  
 [!code-csharp[Formatting.Composite#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#5)]
 [!code-vb[Formatting.Composite#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#5)]  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'allineamento nella formattazione.  Gli argomenti formattati sono inseriti tra barre verticali \(&#124;\) per evidenziare l'allineamento ottenuto.  
  
 [!code-csharp[Formatting.Composite#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Composite/cs/Composite1.cs#6)]
 [!code-vb[Formatting.Composite#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Composite/vb/Composite1.vb#6)]  
  
## Vedere anche  
 <xref:System.Console.WriteLine%2A>   
 <xref:System.String.Format%2A?displayProperty=fullName>   
 [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)   
 [Stringhe di formato numerico standard](../../../docs/standard/base-types/standard-numeric-format-strings.md)   
 [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md)   
 [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)   
 [Stringhe di formato TimeSpan standard](../../../docs/standard/base-types/standard-timespan-format-strings.md)   
 [Stringhe di formato TimeSpan personalizzate](../../../docs/standard/base-types/custom-timespan-format-strings.md)   
 [Stringhe di formato di enumerazione](../../../docs/standard/base-types/enumeration-format-strings.md)