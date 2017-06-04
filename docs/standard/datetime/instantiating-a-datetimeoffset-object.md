---
title: "Creazione di un&#39;istanza di un oggetto DateTimeOffset | Microsoft Docs"
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
  - "creazione di istanze di oggetti fuso orario"
  - "fusi orari (oggetti) [.NET Framework], creazione di istanze"
  - "struttura DateTimeOffset, conversione in DateTime"
  - "struttura DateTimeOffset, creazione di un'istanza"
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Creazione di un&#39;istanza di un oggetto DateTimeOffset
La classe <xref:System.DateTimeOffset> offre vari modi di creare nuovi valori <xref:System.DateTimeOffset>.  Molti corrispondono direttamente ai metodi disponibili per la creazione un'istanza di nuovi valori <xref:System.DateTime>, con miglioramenti che consentono di specificare l'offset del valore di data e ora dall'ora UTC \(Coordinated Universal Time\).  In particolare, è possibile creare un'istanza di un valore <xref:System.DateTimeOffset> nei modi seguenti:  
  
-   Utilizzando un valore letterale data e ora.  
  
-   Chiamando un costruttore <xref:System.DateTimeOffset>.  
  
-   Convertendo implicitamente un valore nel valore <xref:System.DateTimeOffset>.  
  
-   Analizzando la rappresentazione di stringa di una data e ora.  
  
 In questo argomento vengono forniti maggiori dettagli ed esempi di codice che illustrano questi metodi di creazione di un'istanza di nuovi valori <xref:System.DateTimeOffset>.  
  
## Valori letterali data e ora  
 Per linguaggi che supportano questa opzione, uno dei modi più comuni per creare un'istanza di un valore <xref:System.DateTime> è fornire la data e l'ora come valore letterale specificato a livello di codice \(hard\-coded\).  Ad esempio, con il seguente codice Visual Basic viene creato un oggetto <xref:System.DateTime> il cui valore corrisponde al 1 gennaio 2008, alle 10.00.  
  
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]  
  
 I valori <xref:System.DateTimeOffset> possono essere inizializzati anche con valori letterali data e ora, in caso di utilizzo di linguaggi che supportano i valori letterali <xref:System.DateTime>.  Nel seguente codice Visual Basic, ad esempio, viene creato un oggetto <xref:System.DateTimeOffset>.  
  
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]  
  
 Come mostrato nell'output della console, al valore <xref:System.DateTimeOffset> così creato viene assegnato l'offset del fuso orario locale.  Questo esempio dimostra che un valore <xref:System.DateTimeOffset> assegnato utilizzando un valore letterale carattere non identifica uno specifico momento se il codice viene eseguito su computer diversi.  
  
## Costruttori DateTimeOffset  
 Il tipo <xref:System.DateTimeOffset> definisce sei costruttori.  Quattro corrispondono direttamente a costruttori <xref:System.DateTime>, con un parametro aggiuntivo di tipo <xref:System.TimeSpan> che definisce l'offset di data e ora dall'ora UTC.  Questi consentono di definire un valore <xref:System.DateTimeOffset> in base al valore dei singoli componenti di data e ora.  Ad esempio, nel codice seguente vengono utilizzati questi quattro costruttori per creare un'istanza di oggetti <xref:System.DateTimeOffset> con valori identici di 7\/1\/2008 12:05 AM \+01:00.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]  
  
 Notare che, quando il valore dell'oggetto <xref:System.DateTimeOffset>, di cui si è creata un'istanza utilizzando un oggetto <xref:System.Globalization.PersianCalendar> come uno degli argomenti per il relativo costruttore, viene visualizzato sulla console, viene espresso come data del calendario gregoriano anziché persiano.  Per restituire una data utilizzando il calendario persiano, vedere l'esempio nell'argomento <xref:System.Globalization.PersianCalendar>.  
  
 Gli altri due costruttori creano un oggetto <xref:System.DateTimeOffset> da un valore <xref:System.DateTime>.  Il primo dispone di un solo parametro, il valore <xref:System.DateTime> da convertire in un valore <xref:System.DateTimeOffset>.  L'offset del valore <xref:System.DateTimeOffset> risultante dipende dalla proprietà <xref:System.DateTime.Kind%2A> del solo parametro del costruttore.  Se il valore è <xref:System.DateTimeKind?displayProperty=fullName>, l'offset viene impostato uguale a <xref:System.TimeSpan.Zero?displayProperty=fullName>.  In caso contrario, l'offset viene impostato uguale all'offset del fuso orario locale.  Nell'esempio seguente viene illustrato l'utilizzo di questo costruttore per creare un'istanza di oggetti <xref:System.DateTimeOffset> che rappresentano l'ora UTC e il fuso orario locale:  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]  
  
> [!NOTE]
>  La chiamata dell'overload del costruttore <xref:System.DateTimeOffset> che ha un solo parametro <xref:System.DateTime> è equivalente all'esecuzione di una conversione implicita di un valore <xref:System.DateTime> in un valore <xref:System.DateTimeOffset>.  
  
 Il secondo costruttore che crea un oggetto <xref:System.DateTimeOffset> da un valore <xref:System.DateTime> dispone di due parametri: il valore <xref:System.DateTime> da convertire e un valore <xref:System.TimeSpan> che rappresenta l'offset di data e ora dall'ora UTC.  Tale valore dell'offset deve corrispondere alla proprietà <xref:System.DateTime.Kind%2A> del primo parametro del costruttore oppure viene generato un oggetto <xref:System.ArgumentException>.  Se la proprietà <xref:System.DateTime.Kind%2A> del primo parametro è <xref:System.DateTimeKind?displayProperty=fullName>, il valore del secondo parametro deve essere <xref:System.TimeSpan.Zero?displayProperty=fullName>.  Se la proprietà <xref:System.DateTime.Kind%2A> del primo parametro è <xref:System.DateTimeKind?displayProperty=fullName>, il valore del secondo parametro deve essere l'offset del fuso orario del sistema locale.  Se la proprietà <xref:System.DateTime.Kind%2A> del primo parametro è <xref:System.DateTimeKind?displayProperty=fullName>, l'offset può essere qualsiasi valore valido.  Nel codice seguente sono illustrate le chiamate a questo costruttore per convertire <xref:System.DateTime> nei valori <xref:System.DateTimeOffset>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]  
  
## Conversione implicita di tipi  
 Il tipo <xref:System.DateTimeOffset> supporta una conversione implicita di tipi da un valore <xref:System.DateTime> in un valore <xref:System.DateTimeOffset>. Una conversione implicita di tipi è una conversione da un tipo a un altro che non richiede un cast esplicito \(in C\#\) o una conversione esplicita \(in Visual Basic\) e nella quale non vengono perse informazioni.  Rende possibile la scrittura di codice come il seguente.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]  
  
 L'offset del valore <xref:System.DateTimeOffset> risultante dipende dal valore della proprietà <xref:System.DateTime.Kind%2A?displayProperty=fullName>.  Se il valore è <xref:System.DateTimeKind?displayProperty=fullName>, l'offset viene impostato uguale a <xref:System.TimeSpan.Zero?displayProperty=fullName>.  Se il valore è <xref:System.DateTimeKind?displayProperty=fullName> o <xref:System.DateTimeKind?displayProperty=fullName>, l'offset viene impostato uguale all'offset del fuso orario locale.  
  
## Analisi della rappresentazione di stringa di una data e ora  
 Il tipo <xref:System.DateTimeOffset> supporta quattro metodi che consentono di convertire la rappresentazione di stringa di una data e ora in un valore <xref:System.DateTimeOffset>:  
  
-   <xref:System.DateTimeOffset.Parse%2A>che tenta di convertire la rappresentazione di stringa di una data e ora in un valore <xref:System.DateTimeOffset> e genera un'eccezione se la conversione non riesce.  
  
-   <xref:System.DateTimeOffset.TryParse%2A>che tenta di convertire la rappresentazione di stringa di una data e ora in un valore <xref:System.DateTimeOffset> e restituisce `false` se la conversione non riesce.  
  
-   <xref:System.DateTimeOffset.ParseExact%2A>che tenta di convertire la rappresentazione di stringa di una data e ora con uno specifico formato in un valore <xref:System.DateTimeOffset>.  Il metodo genera un'eccezione se la conversione non riesce.  
  
-   <xref:System.DateTimeOffset.TryParseExact%2A>che tenta di convertire la rappresentazione di stringa di una data e ora con uno specifico formato in un valore <xref:System.DateTimeOffset>.  Il metodo restituisce `false` se la conversione non riesce.  
  
 Nell'esempio seguente sono illustrate le chiamate a ognuno di questi quattro metodi di conversione di stringhe per la creazione di un'istanza di un valore <xref:System.DateTimeOffset>.  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)