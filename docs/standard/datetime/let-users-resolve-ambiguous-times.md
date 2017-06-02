---
title: "Procedura: consentire agli utenti di risolvere orari ambigui | Microsoft Docs"
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
ms.assetid: bca874ee-5b68-4654-8bbd-3711220ef332
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: consentire agli utenti di risolvere orari ambigui
Un'ora ambigua è un'ora associata a più ore UTC \(Coordinated Universal Time\).  Si verifica quando l'orario viene portato indietro, ad esempio durante la transizione da ora legale a ora solare di un fuso orario.  Quando si gestisce un'ora ambigua, è possibile effettuare una delle operazioni seguenti:  
  
-   Se l'ora ambigua è un elemento di dati immesso dall'utente, sarà l'utente a risolvere l'ambiguità.  
  
-   Fare una supposizione sul modo in cui l'ora viene associata all'ora UTC.  Ad esempio, è possibile presupporre che un'ora ambigua sia sempre espressa nell'ora solare del fuso orario.  
  
 In questo argomento viene illustrato come consentire a un utente di risolvere un'ora ambigua.  
  
### Per consentire a un utente di risolvere un'ora ambigua  
  
1.  Ottenere l'input di data e ora dall'utente.  
  
2.  Chiamare il metodo <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> per determinare se l'ora è ambigua.  
  
3.  Se l'ora è ambigua, chiamare il metodo <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> per recuperare una matrice di oggetti <xref:System.TimeSpan>.  Ogni elemento della matrice contiene un offset UTC a cui è possibile associare l'ora ambigua.  
  
4.  Consentire all'utente di selezionare l'offset desiderato.  
  
5.  Ottenere la data e ora UTC sottraendo l'offset selezionato dall'utente dall'ora locale.  
  
6.  Chiamare il metodo <xref:System.DateTime.SpecifyKind%2A> `static` \(`Shared` in Visual Basic .NET\) per impostare la proprietà <xref:System.DateTime.Kind%2A> del valore di data e ora UTC su <xref:System.DateTimeKind?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio seguente viene richiesto all'utente di immettere una data e ora e, se è ambigua, consente all'utente di selezionare l'ora UTC alla quale è associata l'ora ambigua.  
  
 [!code-csharp[System.TimeZone2.Concepts#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#11)]
 [!code-vb[System.TimeZone2.Concepts#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#11)]  
  
 Nel codice di esempio viene utilizzata una matrice di oggetti <xref:System.TimeSpan> per indicare i possibili offset dell'ora ambigua dall'ora UTC.  Questi offset non saranno però significativi per l'utente.  Per chiarificare il significato di offset, nel codice viene anche indicato se un offset rappresenta l'ora solare o l'ora legale del fuso orario locale.  Dal confronto dell'offset con il valore della proprietà <xref:System.TimeZoneInfo.BaseUtcOffset%2A> è possibile stabilire quale sia l'ora solare e quale l'ora legale.  Questa proprietà indica la differenza tra l'ora UTC e l'ora solare del fuso orario.  
  
 In questo esempio, tutti i riferimenti al fuso orario locale vengono eseguiti tramite la proprietà <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName>. Il fuso orario locale non viene mai assegnato a una variabile oggetto.  È una procedura consigliata poiché una chiamata al metodo <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName> invalida tutti gli oggetti assegnati al fuso orario locale.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare lo spazio dei nomi <xref:System> con l'istruzione `using` \(richiesto nel codice C\#\).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Procedura: risolvere orari ambigui](../../../docs/standard/datetime/resolve-ambiguous-times.md)