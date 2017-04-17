---
title: "Procedura: Eseguire il round trip dei valori di data e ora | Microsoft Docs"
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
  - "valori di data e ora round trip"
  - "date [.NET Framework], valori round trip"
  - "fusi orari [.NET Framework], valori di data e ora round trip"
  - "ora [.NET Framework], valori round trip"
  - "formattazione delle stringhe [.NET Framework], valori round trip"
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: Eseguire il round trip dei valori di data e ora
In molte applicazioni un valore di data e ora consente di identificare in modo inequivocabile uno specifico determinato momento.  In questo argomento viene illustrato come salvare e ripristinare un valore <xref:System.DateTime>, un valore <xref:System.DateTimeOffset> e un valore di data e ora con informazioni sul fuso orario, in modo che il valore ripristinato identifichi la stessa ora del valore salvato.  
  
### Per eseguire una sequenza di andata e ritorno di un valore DateTime  
  
1.  Convertire il valore <xref:System.DateTime> nella relativa rappresentazione di stringa chiamando il metodo <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> con l'identificatore di formato "o".  
  
2.  Salvare la rappresentazione di stringa del valore <xref:System.DateTime> in un file o passarla a un processo, un dominio applicazione o all'esterno del computer.  
  
3.  Recuperare la stringa che rappresenta il valore <xref:System.DateTime>.  
  
4.  Chiamare il metodo <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=fullName> e passare <xref:System.Globalization.DateTimeStyles?displayProperty=fullName> come valore del parametro `styles`.  
  
 Nell'esempio di codice seguente viene descritto come eseguire una sequenza di andata e ritorno di un valore <xref:System.DateTime>.  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
 [!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]  
  
 Quando si esegue una sequenza di andata e ritorno di un valore <xref:System.DateTime>, questa tecnica consente di mantenere correttamente l'ora per tutte le ore locali e universali.  Ad esempio, se un valore locale <xref:System.DateTime> viene salvato in un sistema nel fuso orario standard del Pacifico \(Stati Uniti\) e viene ripristinato in un sistema nel fuso orario standard degli Stati Uniti Centrali, la data e l'ora ripristinate saranno a due ore rispetto all'ora originale, la quale riflette la differenza di tempo tra i due fusi orari.  Questa tecnica non è tuttavia necessariamente accurata per le ore non specificate.  Tutti i valori <xref:System.DateTime> la cui proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind> vengono gestiti come ore locali.  In caso contrario, <xref:System.DateTime> non identificherà correttamente il momento esatto.  La soluzione alternativa per questa limitazione consiste nell'associare strettamente un valore di data e ora con il fuso orario l'operazione di salvataggio e ripristino.  
  
### Per eseguire una sequenza di andata e ritorno di un valore DateTimeOffset  
  
1.  Convertire il valore <xref:System.DateTimeOffset> nella relativa rappresentazione di stringa chiamando il metodo <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> con l'identificatore di formato "o".  
  
2.  Salvare la rappresentazione di stringa del valore <xref:System.DateTimeOffset> in un file o passarla a un processo, un dominio applicazione o all'esterno del computer.  
  
3.  Recuperare la stringa che rappresenta il valore <xref:System.DateTimeOffset>.  
  
4.  Chiamare il metodo <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=fullName> e passare <xref:System.Globalization.DateTimeStyles?displayProperty=fullName> come valore del parametro `styles`.  
  
 Nell'esempio di codice seguente viene descritto come eseguire una sequenza di andata e ritorno di un valore <xref:System.DateTimeOffset>.  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
 [!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]  
  
 Questa tecnica consente di identificare sempre in modo inequivocabile un valore <xref:System.DateTimeOffset> come uno specifico momento.  Il valore può quindi essere convertito in UTC \(Coordinated Universal Time\) chiamando il metodo <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=fullName> oppure può essere convertito nell'ora di un particolare fuso orario chiamando il metodo <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=fullName> o <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName>.  La limitazione principale di questa tecnica è la possibilità che le operazioni aritmetiche con date e ore, quando vengono eseguite su un valore <xref:System.DateTimeOffset> che rappresenta l'ora un particolare fuso orario, non producano risultati accurati per quel fuso orario.  Ciò è dovuto al fatto che quando si crea un'istanza di un valore <xref:System.DateTimeOffset>, viene annullata l'associazione con il relativo fuso orario.  Pertanto, le regole di rettifica di un fuso orario non possono più essere applicate quando si eseguono calcoli di data e ora.  Per risolvere questo problema, è possibile definire un tipo personalizzato che includa un valore di data e ora e il fuso orario associato.  
  
### Per eseguire una sequenza di andata e ritorno di un valore di data e ora con il relativo fuso orario  
  
1.  Definire una classe o una struttura con due campi.  Il primo campo è un oggetto <xref:System.DateTime> o <xref:System.DateTimeOffset>, mentre il secondo è un oggetto <xref:System.TimeZoneInfo>.  Di seguito è riportato l'esempio di una semplice versione di tale tipo.  
  
     [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
     [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]  
  
2.  Contrassegnare la classe con l'attributo <xref:System.SerializableAttribute>.  
  
3.  Serializzare l'oggetto utilizzando il metodo <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=fullName>.  
  
4.  Ripristinare l'oggetto utilizzando il metodo <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A>.  
  
5.  Eseguire il cast \(in C\#\) o convertire \(in Visual Basic\) l'oggetto deserializzato in un oggetto del tipo adatto.  
  
 Nell'esempio seguente viene illustrato come eseguire una sequenza di andata e ritorno di un oggetto in cui sono archiviati sia la data e l'ora che le informazioni sul fuso orario.  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
 [!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]  
  
 Questa tecnica deve riflettere sempre in modo inequivocabile il momento esatto sia prima che dopo le operazioni di salvataggio e ripristino, a condizione che l'implementazione dell'oggetto data e ora e fuso orario combinato non consenta al valore relativo alla data di perdere la sincronizzazione con il valore del fuso orario.  
  
## Compilazione del codice  
 Requisiti:  
  
-   Gli spazi dei nomi seguenti devono essere importati con istruzioni C\# `using` o istruzioni [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `Imports`:  
  
    -   <xref:System> \(solo C\#\).  
  
    -   <xref:System.Globalization?displayProperty=fullName>.  
  
    -   <xref:System.IO?displayProperty=fullName>.  
  
    -   <xref:System.Runtime.Serialization?displayProperty=fullName>.  
  
    -   <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=fullName>.  
  
-   Riferimento a System.Core.dll.  
  
-   Ogni esempio di codice, tranne la classe `DateInTimeZone`, deve essere incluso in una classe o un modulo di Visual Basic, incapsulato nei metodi e chiamato dal metodo `Main`.  
  
## Vedere anche  
 [Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../ocs/standard/datetime/choosing-between-datetime.md)   
 [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)