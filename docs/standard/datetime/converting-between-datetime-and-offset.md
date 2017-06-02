---
title: "Conversione tra DateTime e DateTimeOffset | Microsoft Docs"
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
  - "conversione di valori DateTimeOffset e DateTime"
  - "conversione di ore"
  - "Date (tipo di dati), conversione"
  - "date [.NET Framework], conversione"
  - "DateTime (struttura), conversione"
  - "struttura DateTimeOffset, conversione"
  - "conversioni di ora locale"
  - "fusi orari [.NET Framework], conversioni"
  - "UTC (ora), conversione"
ms.assetid: b605ff97-0c45-4c24-833f-4c6a3e8be64c
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Conversione tra DateTime e DateTimeOffset
Anche se la struttura <xref:System.DateTimeOffset> offre una maggiore chiarezza sui fusi orari rispetto alla struttura <xref:System.DateTime>, i parametri <xref:System.DateTime> sono utilizzati più comunemente per le chiamate al metodo.  Per questo motivo la possibilità di convertire valori <xref:System.DateTimeOffset> in valori <xref:System.DateTime> e viceversa è particolarmente importante.  In questo argomento viene illustrato come eseguire tali conversioni in una modalità che consente di mantenere il maggior numero possibile di informazioni sul fuso orario.  
  
> [!NOTE]
>  I tipi <xref:System.DateTime> e <xref:System.DateTimeOffset> presentano alcune limitazioni in caso di rappresentazione delle ore nei fusi orari.  Con la proprietà <xref:System.DateTime.Kind%2A>, <xref:System.DateTime> è in grado di riflettere solo l'UTC \(Coordinated Universal Time\) e il fuso orario locale di sistema.  <xref:System.DateTimeOffset> riflette l'offset di un'ora rispetto all'UTC, ma non riflette il fuso orario effettivo al quale appartiene tale offset.  Per dettagli sui valori orari e il supporto dei fusi orari, vedere [Scelta tra DateTime, DateTimeOffset, TimeSpan e TimeZoneInfo](../../../docs/standard/datetime/choosing-between-datetime.md).  
  
## Conversioni da DateTime a DateTimeOffset  
 La struttura <xref:System.DateTimeOffset> fornisce due modalità equivalenti per eseguire la conversione da <xref:System.DateTime> a <xref:System.DateTimeOffset> adatte per la maggior parte delle conversioni:  
  
-   Il costruttore <xref:System.DateTimeOffset.%23ctor%2A> che crea un nuovo oggetto <xref:System.DateTimeOffset> in base a un valore <xref:System.DateTime>.  
  
-   L'operatore di conversione implicito che consente di assegnare un valore <xref:System.DateTime> a un oggetto <xref:System.DateTimeOffset>.  
  
 Per i valori UTC e locali di <xref:System.DateTime>, la proprietà <xref:System.DateTimeOffset.Offset%2A> del valore risultante <xref:System.DateTimeOffset> riflette accuratamente l'offset UTC o del fuso orario locale.  Nel codice riportato di seguito, ad esempio, viene convertito un orario UTC al valore <xref:System.DateTimeOffset> equivalente.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#1)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#1)]  
  
 In questo caso, l'offset della variabile `utcTime2` è 00.00.  Similmente, nel codice seguente viene convertita l'ora locale nel valore <xref:System.DateTimeOffset> equivalente.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#2)]  
  
 Per valori <xref:System.DateTime> la cui proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind?displayProperty=fullName>, questi due metodi di conversione producono tuttavia un valore <xref:System.DateTimeOffset> il cui offset è quello del fuso orario locale,  Questo viene illustrato nell'esempio seguente, che viene eseguito nel fuso orario standard del Pacifico \(Stati Uniti\).  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#3)]  
  
 Se il valore <xref:System.DateTime> riflette la data e l'ora in modo diverso dal fuso orario locale o UTC, è possibile convertirlo in un valore <xref:System.DateTimeOffset> e mantenere le informazioni sul fuso orario chiamando il costruttore <xref:System.DateTimeOffset.%23ctor%2A> di overload.  Nell'esempio riportato di seguito viene creata un'istanza di un oggetto <xref:System.DateTimeOffset> che riflette l'ora solare fuso centrale.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#4)]  
  
 Il secondo parametro per questo overload del costruttore, un oggetto <xref:System.TimeSpan> che rappresenta l'offset dell'ora rispetto a UTC, deve essere recuperato chiamando il metodo <xref:System.TimeZoneInfo.GetUtcOffset%28System.DateTime%29?displayProperty=fullName> del fuso orario corrispondente all'ora.  L'unico parametro del metodo è il valore <xref:System.DateTime> che rappresenta la data e l'ora da convertire.  Se il fuso orario supporta l'ora legale, questo parametro consente al metodo di determinare l'offset adatto per la data e l'ora specifici.  
  
## Conversioni da DateTimeOffset a DateTime  
 La proprietà <xref:System.DateTimeOffset.DateTime%2A> è nella maggior parte dei casi utilizzata per eseguire <xref:System.DateTimeOffset> per la conversione di <xref:System.DateTime>.  Tuttavia, restituisce un valore <xref:System.DateTime> la cui proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind>, come illustrato nell'esempio seguente.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#5)]  
  
 Qualsiasi informazione sulla relazione tra il valore <xref:System.DateTimeOffset> e UTC viene persa durante la conversione quando viene utilizzata la proprietà <xref:System.DateTimeOffset.DateTime%2A>.  Ciò influisce sui valori <xref:System.DateTimeOffset> che corrispondono all'ora UTC o all'ora locale del sistema perché la struttura <xref:System.DateTimeOffset.DateTime%2A> riflette solo questi due fusi orari nella proprietà <xref:System.DateTime.Kind%2A>.  
  
 Per mantenere il maggior numero possibile di informazioni sul fuso orario durante la conversione di <xref:System.DateTimeOffset> in un valore <xref:System.DateTime>, è possibile utilizzare le proprietà <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName> e <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName>  
  
### Conversione di un'ora UTC  
 Per indicare che un valore <xref:System.DateTimeOffset.DateTime%2A> convertito corrisponde all'ora UTC, è possibile recuperare il valore della proprietà <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName>.  Tale proprietà è diversa dalla proprietà <xref:System.DateTimeOffset.DateTime%2A> per due ragioni:  
  
-   Restituisce un valore <xref:System.DateTime> la cui proprietà <xref:System.DateTime.Kind%2A> è <xref:System.DateTimeKind>.  
  
-   Se il valore della proprietà <xref:System.DateTimeOffset.Offset%2A> non è uguale a <xref:System.TimeSpan.Zero?displayProperty=fullName>, l'ora viene convertita in UTC.  
  
> [!NOTE]
>  Se l'applicazione richiede che i valori convertiti <xref:System.DateTime> identifichino in modo non ambiguo un solo momento, è necessario utilizzare la proprietà <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName> per gestire tutte le conversioni da <xref:System.DateTimeOffset> a <xref:System.DateTime>.  
  
 Nell'esempio di codice riportato di seguito viene utilizzata la proprietà <xref:System.DateTimeOffset.UtcDateTime%2A> per convertire un valore <xref:System.DateTimeOffset> il cui offset equivale a <xref:System.TimeSpan.Zero?displayProperty=fullName> in un valore <xref:System.DateTime>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#6)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#6)]  
  
 Nel codice seguente viene utilizzata la proprietà <xref:System.DateTimeOffset.UtcDateTime%2A> per eseguire una conversione del fuso orario e del tipo su un valore <xref:System.DateTimeOffset>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#12)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#12)]  
  
### Conversione dell'ora locale  
 Per indicare che un valore <xref:System.DateTimeOffset> rappresenta l'ora locale, è possibile passare il valore <xref:System.DateTime> restituito dalla proprietà <xref:System.DateTimeOffset.DateTime%2A?displayProperty=fullName> al metodo `static` \(`Shared` in Visual Basic\) <xref:System.DateTime.SpecifyKind%2A>.  Il metodo restituisce la data e l'ora passate come primo parametro, ma imposta la proprietà <xref:System.DateTime.Kind%2A> sul valore specificato dal secondo parametro.  Nel codice seguente viene utilizzato il metodo <xref:System.DateTime.SpecifyKind%2A> in caso di conversione di un valore <xref:System.DateTimeOffset> il cui offset corrisponde a quello del fuso orario locale.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#7)]  
  
 È possibile anche utilizzare la proprietà <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> per convertire un valore <xref:System.DateTimeOffset> in un valore locale <xref:System.DateTime>.  La proprietà <xref:System.DateTime.Kind%2A> del valore <xref:System.DateTime> restituito è <xref:System.DateTimeKind>.  Nel codice seguente viene utilizzata la proprietà <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> in caso di conversione di un valore <xref:System.DateTimeOffset> il cui offset corrisponde a quello del fuso orario locale.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#10)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#10)]  
  
 Quando si recupera un valore <xref:System.DateTime> utilizzando la proprietà <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName>, la funzione di accesso della proprietà `get` converte dapprima il valore <xref:System.DateTimeOffset> in UTC, quindi lo converte in ora locale chiamando il metodo <xref:System.DateTimeOffset.ToLocalTime%2A>.  È pertanto possibile recuperare un valore dalla proprietà <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> per eseguire una conversione del fuso orario contemporaneamente all'esecuzione della conversione di un tipo.  Inoltre vengono applicate le regole di rettifica del fuso orario nell'esecuzione della conversione.  Nel codice seguente viene illustrato l'utilizzo della proprietà <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> per eseguire una conversione del fuso orario e del tipo.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#11)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#11)]  
  
### Metodo di conversione generale  
 Nell'esempio riportato di seguito viene definito un metodo denominato `ConvertFromDateTimeOffset` che converte valori <xref:System.DateTimeOffset> in valori <xref:System.DateTime>.  In base all'offset, determina se il valore <xref:System.DateTimeOffset> si riferisce a un'ora UTC, un'ora locale, o altro, e definisce di conseguenza la proprietà <xref:System.DateTime.Kind%2A> del valore restituito di data e ora.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#8)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#8)]  
  
 Nell'esempio riportato di seguito viene chiamato il metodo `ConvertFromDateTimeOffset` per convertire i valori <xref:System.DateTimeOffset> che rappresentano un'ora UTC, un'ora locale e un'ora nel fuso orario standard degli Stati Uniti Centrali.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#9)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#9)]  
  
 Questo codice si basa su due presupposti che, a seconda dell'applicazione e dell'origine dei valori di data e ora, potrebbero non essere sempre validi:  
  
-   Il presupposto che un valore di data e ora il cui offset è <xref:System.TimeSpan.Zero?displayProperty=fullName> rappresenti il fuso orario UTC.  Infatti, UTC non rappresenta un'ora in un particolare fuso orario, ma l'ora in relazione alla quale vengono regolati i fusi orari di tutto il mondo.  I fusi orari possono presentare anche un offset di <xref:System.TimeSpan.Zero>.  
  
-   Il presupposto che valori di data e ora il cui offset è uguale a quelli del fuso orario locale rappresentino il fuso orario locale.  Poiché l'associazione dei valori di data e ora al fuso orario originale è annullata, potrebbe non essere questo il caso; la data e l'ora potrebbero essere state originate in un altro fuso orario con lo stesso offset.  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)