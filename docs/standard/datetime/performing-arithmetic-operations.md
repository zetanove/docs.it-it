---
title: "Esecuzione di operazioni aritmetiche con date e ore | Microsoft Docs"
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
  - "operazioni aritmetiche [.NET Framework], date e ore"
  - "date [.NET Framework], operazioni aritmetiche"
  - "date [.NET Framework], confronto"
  - "DateTime (struttura), operazioni aritmetiche"
  - "struttura DateTimeOffset, operazioni aritmetiche"
  - "fusi orari [.NET Framework], operazioni aritmetiche"
  - "ore [.NET Framework], operazioni aritmetiche"
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Esecuzione di operazioni aritmetiche con date e ore
Anche se entrambe le strutture <xref:System.DateTime> e <xref:System.DateTimeOffset> forniscono membri che eseguono operazioni aritmetiche sui relativi valori, i risultati di tali operazioni sono molto diversi.  In questo argomento vengono esaminate tali differenze, messe in relazione ai gradi di dipendenza dal fuso orario nei valori di data e ora e viene descritto come eseguire operazioni completamente dipendenti dal fuso orario utilizzando i valori di data e ora.  
  
## Confronti e operazioni aritmetiche con i valori DateTime  
 A partire da .NET Framework versione 2.0, i valori <xref:System.DateTime> possiedono un grado limitato di dipendenza dal fuso orario.  La proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> consente l'assegnazione di un valore <xref:System.DateTimeKind> alla data e all'ora per indicare se rappresenta l'ora locale, l'ora UTC \(Coordinated Universal Time\) o l'ora di un fuso orario non specificato.  Tuttavia, queste limitate informazioni sul fuso orario vengono ignorate quando viene eseguito il confronto oppure operazioni aritmetiche con date e ore su valori <xref:System.DateTime>.  Nell'esempio seguente, in cui si confronta l'ora locale corrente con l'ora UTC corrente, viene illustrata questa situazione.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]  
  
 Il metodo <xref:System.DateTime.CompareTo%28System.DateTime%29> indica che l'ora locale è precedente, o in altri termini, minore dell'ora UTC e l'operazione di sottrazione indica che la differenza tra l'ora UTC e l'ora locale per un sistema nel fuso orario del Pacifico \(Stati Uniti\) è di sette ore.  Ma poiché questi due valori forniscono rappresentazioni diverse di un solo determinato momento, è chiaro in questo caso che tale intervallo di tempo è completamente attribuibile all'offset del fuso orario locale rispetto all'ora UTC.  
  
 Più in generale, la proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> non influisce sui risultati restituiti dai metodi di confronto e aritmetici <xref:System.DateTime> \(come indica il confronto tra due identici momenti\), anche se può influire sull'interpretazione di tali risultati.  Di seguito è riportato un esempio.  
  
-   Il risultato di qualsiasi operazione aritmetica eseguita su due valori di data e ora le cui proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> sono uguali a <xref:System.DateTimeKind> riflette l'intervallo di tempo effettivo tra i due valori.  Allo stesso modo, il confronto tra due valori di data e ora con queste caratteristiche riflette esattamente la relazione tra i due tempi.  
  
-   Il risultato di qualsiasi operazione di confronto o aritmetica eseguita su due valori di data e ora le cui proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> sono uguali a <xref:System.DateTimeKind> o su due valori di data e ora con valori diversi della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName> riflette la differenza di orario tra i due valori.  
  
-   Le operazioni aritmetiche o di confronto sui valori di data e ora locali non considerano se un particolare valore è ambiguo o non valido, né tengono conto dell'effetto di eventuali regole di rettifica risultanti dalla transizione del fuso orario locale da o all'ora legale.  
  
-   Qualsiasi operazione che confronta o calcola la differenza tra l'ora UTC e un'ora locale include nel risultato un intervallo di tempo uguale all'offset del fuso orario locale rispetto all'ora UTC.  
  
-   Qualsiasi operazione che confronta o calcola la differenza tra un'ora non specificata e l'ora UTC o l'ora locale riflette l'orario semplice.  Le differenze di fuso orario non vengono considerate e il risultato non riflette l'applicazione di regole di rettifica del fuso orario.  
  
-   Qualsiasi operazione che confronta o calcola la differenza tra due ore non specificate può includere un intervallo sconosciuto che riflette la differenza tra l'ora di due fusi orari diversi.  
  
 In molti scenari le differenze di fuso orario non influiscono sui calcoli di data e ora \(per informazioni su alcuni di questi, vedere [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md)\) o il contesto dei valori di data e ora definisce il significato delle operazioni di confronto o aritmetiche.  
  
## Confronti e operazioni aritmetiche con i valori DateTimeOffset  
 Un valore <xref:System.DateTimeOffset> include non solo una data e un'ora, ma anche un offset che definisce in modo univoco tali data e ora rispetto all'ora UTC.  In questo modo è possibile definire l'uguaglianza in modo diverso rispetto ai valori <xref:System.DateTime>.  Mentre i valori <xref:System.DateTime> sono uguali se hanno lo stesso valore di data e ora, i valori <xref:System.DateTimeOffset> sono uguali se entrambi si riferiscono allo stesso momento.  Ciò rende un valore <xref:System.DateTimeOffset> più preciso e meno soggetto a interpretazione quando viene utilizzato nei confronti e nella maggior parte delle operazioni aritmetiche che determinano l'intervallo tra due date e ore.  Nell'esempio seguente, che è l'equivalente <xref:System.DateTimeOffset> dell'esempio precedente in cui sono stati confrontati i valori <xref:System.DateTime> locale e UTC, viene illustrata questa differenza nel comportamento.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]  
  
 In questo esempio, il metodo <xref:System.DateTimeOffset.CompareTo%2A> indica che l'ora locale corrente e l'ora UTC corrente sono uguali e la sottrazione dei valori <xref:System.DateTimeOffset> indica che la differenza tra i due orari è <xref:System.TimeSpan.Zero?displayProperty=fullName>.  
  
 La limitazione principale dell'utilizzo di valori <xref:System.DateTimeOffset> nelle operazioni aritmetiche con date e ora consiste nel fatto che, anche se i valori <xref:System.DateTimeOffset> dipendono parzialmente dal fuso orario, in realtà non ne sono completamente dipendenti.  Anche se l'offset del valore <xref:System.DateTimeOffset> riflette l'offset di un fuso orario rispetto all'ora UTC quando a una variabile <xref:System.DateTimeOffset> viene assegnato un valore, l'associazione al fuso orario viene successivamente annullata.  Poiché non è più associato direttamente a un'ora identificabile, l'addizione e la sottrazione di intervalli di data e ora non considerano le regole di rettifica di un fuso orario.  
  
 A titolo illustrativo, la transizione all'ora legale nel fuso orario degli Stati Uniti Centrali si verifica alle 2:00 A.M. del 9 marzo 2008.  Ciò significa che aggiungere un intervallo di due ore e mezzo alle 1:30 AM il 9 marzo 2008 nel fuso orario standard degli Stati Uniti Centrali, deve produrre una data e un'ora equivalente a le 5:00 AM il 9 marzo 2008.  Tuttavia, come mostrato nell'esempio, l'addizione dà come risultato le 4.00 AM del 9 Marzo, 2008.  Si noti che il risultato di questa operazione rappresenta il momento corretto, anche se non corrisponde all'ora del fuso orario di interesse \(ovvero non include l'offset dal fuso orario previsto\).  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]  
  
## Operazioni aritmetiche con ore nei fusi orari  
 La classe <xref:System.TimeZoneInfo> include diversi metodi di conversione che applicano automaticamente le rettifiche quando convertono le ore da un fuso orario all'altro,  tra cui:  
  
-   I metodi <xref:System.TimeZoneInfo.ConvertTime%2A> e <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>, che convertono le ore tra due fusi orari.  
  
-   I metodi <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> e <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A>, che convertono l'ora di un determinato fuso orario nell'ora UTC o convertono l'ora UTC nell'ora di un determinato fuso orario.  
  
 Per informazioni dettagliate, vedere [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md).  
  
 La classe <xref:System.TimeZoneInfo> non fornisce metodi che applicano automaticamente regole di rettifica quando si eseguono operazioni aritmetiche con date e ore.  Tuttavia, è possibile ottenere il risultato desiderato convertendo l'ora di un fuso orario in un'ora UTC, eseguendo l'operazione aritmetica ed eseguendo nuovamente la conversione dall'ora UTC all'ora del fuso orario.  Per informazioni dettagliate, vedere [Procedura: utilizzare fusi orari nell'aritmetica di data e ora](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md).  
  
 Ad esempio, il codice seguente è simile al codice precedente, in cui sono state aggiunte due ore e mezzo alle 2.00 AM del 9 Marzo, 2008.  Tuttavia, poiché in questo caso si converte un'ora solare fuso centrale nell'ora UTC prima di eseguire l'operazione aritmetica con data e ora, e quindi si converte di nuovo il risultato dall'ora UTC all'ora solare fuso centrale, l'ora risultante riflette la transizione del fuso Ora solare fuso centrale all'ora legale.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Procedura: utilizzare fusi orari nell'aritmetica di data e ora](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)