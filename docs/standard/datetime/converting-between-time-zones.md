---
title: "Conversione degli orari tra fusi orari | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conversione di ore"
  - "conversioni di ora locale"
  - "fusi orari [.NET Framework], conversioni"
  - "ore [.NET Framework], conversione"
  - "UTC (ora), conversione"
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Conversione degli orari tra fusi orari
La gestione delle differenze tra fusi orari sta divenendo sempre più importante per le applicazioni che utilizzano date e ore.  Non è più possibile presupporre che tutti gli orari possano essere espressi su base locale, ovvero in base all'orario disponibile dalla struttura <xref:System.DateTime>.  Ad esempio, una pagina Web che visualizza l'orario corrente della parte orientale degli Stati Uniti risulterà non attendibile per un cliente dell'Asia orientale.  In questo argomento viene illustrato come convertire gli orari da un fuso orario all'altro, nonché come convertire i valori <xref:System.DateTimeOffset> che dipendono in parte dal fuso orario.  
  
## Conversione nel formato UTC  
 UTC \(Coordinated Universal Time\) è uno standard di alta precisione basato sul tempo atomico.  I fusi orari del mondo sono espressi come offset positivi o negativi dall'ora UTC.  L'orario espresso in UTC è quindi indipendente dal fuso orario.  L'utilizzo dell'ora UTC è consigliato quando la portabilità di data e ora tra i computer è importante. \(Per informazioni dettagliate e altre procedure consigliate sull'utilizzo di date e ore, vedere [Coding Best Practices Using DateTime in the .NET Framework](http://go.microsoft.com/fwlink/?LinkId=92342).\) La conversione di singoli fusi orari in ore UTC semplifica i confronti tra gli orari.  
  
> [!NOTE]
>  È inoltre possibile serializzare una struttura <xref:System.DateTimeOffset> per rappresentare in modo non ambiguo un determinato momento.  Poiché gli oggetti <xref:System.DateTimeOffset> archiviano un valore di data e ora insieme all'offset dall'ora UTC, rappresentano sempre un determinato momento in relazione all'ora UTC.  
  
 Il modo più semplice per convertire un orario in ora UTC è chiamare il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> `static`, ovvero `Shared` in Visual Basic.  Il tipo specifico di conversione eseguita dal metodo dipende dal valore della proprietà <xref:System.DateTime.Kind%2A> del parametro `dateTime`, come mostrato nella tabella seguente.  
  
|Proprietà DateTime.Kind|Conversion|  
|-----------------------------|----------------|  
|<xref:System.DateTimeKind?displayProperty=fullName>|Converte l'ora locale in ora UTC.|  
|<xref:System.DateTimeKind?displayProperty=fullName>|Presuppone che il parametro `dateTime` sia l'ora locale e converte l'ora locale in ora UTC.|  
|<xref:System.DateTimeKind?displayProperty=fullName>|Restituisce il parametro `dateTime` invariato.|  
  
 Nel codice seguente l'ora locale corrente viene convertita in ora UTC e il risultato viene visualizzato nella console.  
  
 [!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
 [!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]  
  
> [!NOTE]
>  Il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> non comporta necessariamente risultati identici a quelli forniti dai metodi <xref:System.TimeZone.ToUniversalTime%2A?displayProperty=fullName> e <xref:System.DateTime.ToUniversalTime%2A?displayProperty=fullName>.  Se il fuso orario locale del sistema host comprende più regole di modifica, il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> applica la regola appropriata a una data e un'ora specifici.  Gli altri due metodi vengono sempre applicati alla regola di modifica più recente.  
  
 Se il valore di data e ora non rappresenta l'ora locale o l'ora UTC, il metodo <xref:System.DateTime.ToUniversalTime%2A> restituirà probabilmente un risultato errato.  È tuttavia possibile utilizzare il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=fullName> per convertire la data e ora da un fuso orario specificato. Per informazioni dettagliate sul recupero di un oggetto <xref:System.TimeZoneInfo> che rappresenta il fuso orario di destinazione, vedere [Ricerca dei fusi orari definiti in un sistema locale](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md). Nel codice seguente viene utilizzato il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=fullName> per convertire l'ora solare fuso orientale in ora UTC.  
  
 [!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
 [!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]  
  
 Notare che questo metodo genera un'eccezione <xref:System.ArgumentException> se la proprietà <xref:System.DateTime.Kind%2A> dell'oggetto <xref:System.DateTime> e il fuso orario non corrispondono.  Una mancata corrispondenza viene rilevata se la proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind?displayProperty=fullName> ma l'oggetto <xref:System.TimeZoneInfo> non rappresenta il fuso orario locale oppure se la proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind?displayProperty=fullName> ma l'oggetto <xref:System.TimeZoneInfo> non è uguale a <xref:System.DateTimeKind?displayProperty=fullName>.  
  
 Tutti questi metodi accettano valori <xref:System.DateTime> come parametri e restituiscono un valore <xref:System.DateTime>.  Per i valori <xref:System.DateTimeOffset>, la struttura <xref:System.DateTimeOffset> presenta un metodo di istanza <xref:System.DateTimeOffset.ToUniversalTime%2A> che converte la data e ora dell'istanza corrente in ora UTC.  Nell'esempio seguente viene chiamato il metodo <xref:System.DateTimeOffset.ToUniversalTime%2A> per convertire l'ora locale e diversi altri orari nell'ora UTC \(Coordinated Universal Time\).  
  
 [!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
 [!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]  
  
## Conversione dell'ora UTC in un determinato fuso orario  
 Per convertire l'ora UTC nell'ora locale, vedere la sezione "Conversione dell'ora UTC nell'ora locale" riportata di seguito.  Per convertire l'ora UTC nell'ora di un determinato fuso orario, chiamare il metodo <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>.  Questo metodo accetta due parametri:  
  
-   L'ora UTC da convertire.  Deve essere un valore <xref:System.DateTime> la cui proprietà <xref:System.DateTime.Kind%2A> è impostata su <xref:System.DateTimeKind?displayProperty=fullName> o <xref:System.DateTimeKind?displayProperty=fullName>.  
  
-   Il fuso orario nel quale convertire l'ora UTC.  
  
 Nel codice seguente l'ora UTC viene convertita nell'ora solare fuso centrale.  
  
 [!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
 [!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]  
  
## Conversione dell'ora UTC nell'ora locale  
 Per convertire l'ora UTC nell'ora locale, chiamare il metodo <xref:System.DateTime.ToLocalTime%2A> dell'oggetto <xref:System.DateTime> di cui si desidera convertire l'orario.  Il comportamento esatto del metodo dipende dal valore della proprietà <xref:System.DateTime.Kind%2A> dell'oggetto, come illustrato nella tabella riportata di seguito.  
  
|Proprietà `DateTime.Kind`|Conversion|  
|-------------------------------|----------------|  
|`DateTimeKind.Local`|Restituisce il valore <xref:System.DateTime> invariato.|  
|`DateTimeKind.Unspecified`|Presuppone che il valore <xref:System.DateTime> sia UTC e converte l'ora UTC nell'ora locale.|  
|`DateTimeKind.Utc`|Converte il valore <xref:System.DateTime> nell'ora locale.|  
  
 **Nota** Il metodo <xref:System.TimeZone.ToLocalTime%2A?displayProperty=fullName> si comporta in modo identico al metodo `DateTime.ToLocalTime`.  Accetta un solo parametro, ovvero il valore di data e ora da convertire.  
  
 È inoltre possibile convertire l'ora di un determinato fuso orario nell'ora locale utilizzando il metodo <xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=fullName> `static` \(`Shared` in Visual Basic\).  Questa tecnica viene illustrata nella sezione seguente.  
  
## Conversione tra due fusi orari  
 È possibile eseguire la conversione tra due fusi orari utilizzando uno dei due metodi seguenti `static` \(`Shared` in Visual Basic\) della classe <xref:System.TimeZoneInfo>:  
  
-   <xref:System.TimeZoneInfo.ConvertTime%2A>  
  
     I parametri di questo metodo sono il valore di data e ora da convertire, un oggetto `TimeZoneInfo` che rappresenta il fuso orario del valore di data e ora e un oggetto `TimeZoneInfo` che rappresenta il fuso orario in cui convertire il valore di data e ora.  
  
-   <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>  
  
     I parametri di questo metodo sono il valore di data e ora da convertire, l'identificatore del fuso orario del valore di data e ora e l'identificatore del fuso orario in cui convertire il valore di data e ora.  
  
 Entrambi i metodi richiedono che la proprietà <xref:System.DateTime.Kind%2A> del valore di data e ora da convertire e l'oggetto <xref:System.TimeZoneInfo> o l'identificatore del fuso orario che rappresenta il relativo fuso orario corrispondano tra loro.  In caso contrario, verrà generata un'eccezione <xref:System.ArgumentException>.  Se, ad esempio, la proprietà `Kind` del valore di data e ora è `DateTimeKind.Local`, viene generata un'eccezione se l'oggetto `TimeZoneInfo` passato come parametro al metodo non è uguale a `TimeZoneInfo.Local`.  Un'eccezione viene inoltre generata se l'identificatore passato come parametro al metodo non è uguale a `TimeZoneInfo.Local.Id`.  
  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.TimeZoneInfo.ConvertTime%2A> per eseguire la conversione dall'ora solare Hawaii all'ora locale.  
  
 [!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
 [!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]  
  
## Conversione dei valori DateTimeOffset  
 I valori di data e ora rappresentati dagli oggetti <xref:System.DateTimeOffset> non dipendono completamente dal fuso orario poiché è stata annullata l'associazione dell'oggetto al relativo fuso orario durante la creazione di un'istanza di tale oggetto.  In molti casi è tuttavia necessario convertire semplicemente una data e ora in base a due diversi offset dall'ora UTC anziché in base all'ora di determinati fusi orari.  Per eseguire questa conversione, è possibile chiamare il metodo <xref:System.DateTimeOffset.ToOffset%2A> dell'istanza corrente.  L'unico parametro del metodo è l'offset del nuovo valore di data e ora restituito dal metodo.  
  
 Se, ad esempio, la data e ora di una richiesta dell'utente per una pagina Web è nota e serializzata come stringa nel formato MM\/dd\/yyyy hh:mm:ss zzzz, il metodo `ReturnTimeOnServer` seguente converte questo valore di data e ora nella data e ora del server Web.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
 [!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)]  
  
 Se al metodo viene passata la stringa "9\/1\/2007 5:32:07 \-05:00" che rappresenta la data e l'ora in un fuso orario indietro di cinque ore rispetto all'ora UTC, viene restituito 9\/1\/2007 3:32:07 AM \-07:00 per un server situato nel fuso orario standard del Pacifico \(Stati Uniti\).  
  
 La classe <xref:System.TimeZoneInfo> include anche un overload del metodo <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName> che esegue le conversioni del fuso orario con i valori <xref:System.DateTimeOffset>.  I parametri del metodo sono un valore <xref:System.DateTimeOffset> e un riferimento al fuso orario in cui convertire l'ora.  La chiamata al metodo restituisce un valore <xref:System.DateTimeOffset>.  Ad esempio, il metodo `ReturnTimeOnServer` dell'esempio precedente potrebbe essere riscritto come segue per chiamare il metodo <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]  
  
## Vedere anche  
 <xref:System.TimeZoneInfo>   
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Ricerca dei fusi orari definiti in un sistema locale](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)