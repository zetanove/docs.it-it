---
title: "Procedura: risolvere orari ambigui | Microsoft Docs"
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
  - "ora ambigua [.NET Framework]"
  - "fusi orari [.NET Framework], ora ambigua"
ms.assetid: 2cf5fb25-492c-4875-9245-98cac8348e97
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: risolvere orari ambigui
Un'ora ambigua è un'ora associata a più ore UTC \(Coordinated Universal Time\).  Si verifica quando l'orario viene portato indietro, ad esempio durante la transizione da ora legale a ora solare di un fuso orario.  Quando si gestisce un'ora ambigua, è possibile effettuare una delle operazioni seguenti:  
  
-   Fare una supposizione sul modo in cui l'ora viene associata all'ora UTC.  Ad esempio, è possibile presupporre che un'ora ambigua sia sempre espressa nell'ora solare del fuso orario.  
  
-   Se l'ora ambigua è un elemento di dati immesso dall'utente, sarà l'utente a risolvere l'ambiguità.  
  
 In questo argomento viene descritto come risolvere un'ora ambigua presupponendo che rappresenti l'ora solare del fuso orario.  
  
### Per associare un'ora ambigua all'ora solare del fuso orario  
  
1.  Chiamare il metodo <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> per determinare se l'ora è ambigua.  
  
2.  Se l'ora è ambigua, sottrarre l'ora dall'oggetto <xref:System.TimeSpan> restituito dalla proprietà <xref:System.TimeZoneInfo.BaseUtcOffset%2A> del fuso orario.  
  
3.  Chiamare il metodo <xref:System.DateTime.SpecifyKind%2A> `static` \(`Shared` in Visual Basic .NET\) per impostare la proprietà <xref:System.DateTime.Kind%2A> del valore di data e ora UTC su <xref:System.DateTimeKind?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come convertire un'ora ambigua in un'ora UTC presupponendo che rappresenti l'ora solare del fuso orario locale.  
  
 [!code-csharp[System.TimeZone2.Concepts#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#10)]
 [!code-vb[System.TimeZone2.Concepts#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#10)]  
  
 L'esempio è costituito da un metodo denominato `ResolveAmbiguousTime` che determina se il valore <xref:System.DateTime> passato è ambiguo.  Se il valore è ambiguo, il metodo restituisce un valore <xref:System.DateTime> che rappresenta l'ora UTC corrispondente.  Il metodo gestisce questa conversione sottraendo il valore della proprietà <xref:System.TimeZoneInfo.BaseUtcOffset%2A> del fuso orario locale dall'ora locale.  
  
 In genere, un'ora ambigua viene gestita chiamando il metodo <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> per recuperare una matrice di oggetti <xref:System.TimeSpan> contenente i possibili offset UTC dell'ora ambigua.  In questo esempio si presuppone che un'ora ambigua sia sempre associata all'ora solare del fuso orario.  La proprietà <xref:System.TimeZoneInfo.BaseUtcOffset%2A> restituisce l'offset tra l'ora UTC e l'ora solare del fuso orario.  
  
 In questo esempio, tutti i riferimenti al fuso orario locale vengono eseguiti tramite la proprietà <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName>. Il fuso orario locale non viene mai assegnato a una variabile oggetto.  È una procedura consigliata poiché una chiamata al metodo <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName> invalida tutti gli oggetti assegnati al fuso orario locale.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare lo spazio dei nomi <xref:System> con l'istruzione `using` \(richiesto nel codice C\#\).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Procedura: consentire agli utenti di risolvere orari ambigui](../../../docs/standard/datetime/let-users-resolve-ambiguous-times.md)