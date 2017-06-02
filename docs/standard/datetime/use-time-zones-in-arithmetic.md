---
title: "Procedura: utilizzare fusi orari nell&#39;aritmetica di data e ora | Microsoft Docs"
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
  - "date [.NET Framework], aggiunta e sottrazione"
  - "fusi orari [.NET Framework], operazioni aritmetiche"
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: utilizzare fusi orari nell&#39;aritmetica di data e ora
In genere, quando si esegue l'aritmetica di data e ora utilizzando i valori <xref:System.DateTime> o <xref:System.DateTimeOffset>, il risultato non riflette le regole di regolazione dei fusi orari.  Questo vale anche quando il fuso orario del valore di data e ora è chiaramente identificabile, ad esempio quando la proprietà <xref:System.DateTime.Kind%2A> è impostata su <xref:System.DateTimeKind>.  In questo argomento viene illustrato come eseguire operazioni aritmetiche su valori di data e ora appartenenti a un determinato fuso orario.  I risultati delle operazioni aritmetiche rifletteranno le regole di regolazione del fuso orario.  
  
### Per applicare le regole di regolazione all'aritmetica di data e ora  
  
1.  Implementare un metodo in base al quale un valore di data e ora è strettamente collegato al fuso orario al quale appartiene.  Ad esempio, dichiarare una struttura che includa il valore di data e ora e il relativo fuso orario.  Nell'esempio seguente viene utilizzato tale approccio per collegare un valore <xref:System.DateTime> al relativo fuso orario.  
  
     [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
     [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]  
  
2.  Convertire un'ora nell'ora UTC \(Coordinated Universal Time\) chiamando il metodo <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> o il metodo <xref:System.TimeZoneInfo.ConvertTime%2A>.  
  
3.  Eseguire l'operazione aritmetica sull'ora UTC.  
  
4.  Convertire l'ora dall'ora UTC al fuso orario dell'ora originale chiamando il metodo <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio seguente vengono aggiunti due ore e trenta minuti al 9 marzo 2008, 1.30 Ora solare fuso centrale.  La transizione del fuso orario all'ora legale si verifica trenta minuti dopo, alle 2:00 A.M. del 9 Marzo, 2008.  Poiché nell'esempio vengono seguiti i quattro passaggi riportati nella sezione precedente, l'orario corretto risultante corrisponderà alle 5.00 A.M. il 9 Marzo, 2008.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
 [!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]  
  
 L'associazione di entrambi i valori <xref:System.DateTime> e <xref:System.DateTimeOffset> a un fuso orario al quale potrebbero appartenere viene annullata.  Per eseguire l'aritmetica di data e ora in modo da applicare automaticamente le regole di regolazione di un fuso orario, è necessario che il fuso orario a cui appartiene il valore di data e ora sia immediatamente identificabile,  ovvero che la data e ora e il relativo fuso orario associato siano strettamente collegati.  Sono disponibili diversi modi per eseguire tale operazione, tra cui:  
  
-   Presupporre che tutti gli orari utilizzati in un'applicazione appartengano a un determinato fuso orario.  Sebbene adatto in alcuni casi, questo approccio ha una flessibilità limitata e talvolta anche una portabilità limitata.  
  
-   Definire un tipo in base al quale una data e ora siano strettamente collegate al relativo fuso orario associato includendo entrambi i valori come campi del tipo.  Questo approccio viene utilizzato nell'esempio di codice definendo una struttura per archiviare la data e ora e il fuso orario in due campi membro.  
  
 Nell'esempio viene illustrato come eseguire operazioni aritmetiche sui valori <xref:System.DateTime> in modo da applicare le regole di regolazione del fuso orario al risultato.  È possibile eventualmente utilizzare i valori <xref:System.DateTimeOffset> altrettanto facilmente.  Nell'esempio seguente viene illustrato come modificare il codice dell'esempio originale per l'utilizzo di <xref:System.DateTimeOffset> anziché dei valori <xref:System.DateTime>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]  
  
 Notare che se questa somma viene eseguita semplicemente sul valore <xref:System.DateTimeOffset> senza prima convertirlo nell'ora UTC, il risultato rifletterà il momento esatto mentre l'offset relativo non rifletterà quello del fuso orario definito per tale orario.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare lo spazio dei nomi <xref:System> con l'istruzione `using` \(richiesto nel codice C\#\).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Esecuzione di operazioni aritmetiche con date e ore](../../../docs/standard/datetime/performing-arithmetic-operations.md)