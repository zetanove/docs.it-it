---
title: "Procedura: accedere agli oggetti predefiniti dell&#39;ora UTC e del fuso orario locale | Microsoft Docs"
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
  - "fuso orario locale (accesso)"
  - "fusi orari predefiniti"
  - "fusi orari [.NET Framework], locali"
  - "fusi orari [.NET Framework], recupero"
  - "fusi orari [.NET Framework], UTC"
  - "UTC (ora), predefiniti"
ms.assetid: 961fb70b-83f0-4dab-a042-cb5fcd817cf5
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: accedere agli oggetti predefiniti dell&#39;ora UTC e del fuso orario locale
La classe <xref:System.TimeZoneInfo> fornisce due proprietà, <xref:System.TimeZoneInfo.Utc%2A> e <xref:System.TimeZoneInfo.Local%2A>, che forniscono il codice di accesso agli oggetti predefiniti del fuso orario.  In questo argomento viene illustrato come accedere agli oggetti <xref:System.TimeZoneInfo> restituiti da tali proprietà.  
  
### Per accedere all'oggetto TimeZoneInfo dell'ora UTC \(Coordinated Universal Time\)  
  
1.  Utilizzare la proprietà `static` \(`Shared` in Visual Basic\) <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> per accedere all'ora UTC \(Coordinated Universal Time\).  
  
2.  Anziché assegnare l'oggetto <xref:System.TimeZoneInfo> restituito dalla proprietà a una variabile oggetto, continuare ad accedere all'ora UTC \(Coordinated Universal Time\) tramite la proprietà <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName>.  
  
### Per accedere al fuso orario locale  
  
1.  Utilizzare la proprietà `static` \(`Shared` in Visual Basic\) <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> per accedere al fuso orario locale del sistema.  
  
2.  Anziché assegnare l'oggetto <xref:System.TimeZoneInfo> restituito dalla proprietà a una variabile oggetto, continuare ad accedere al fuso orario locale tramite la proprietà <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName>.  
  
## Esempio  
 Il codice seguente utilizza le proprietà <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> e <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> per convertire un orario del fuso orario standard degli Stati Uniti e Canada orientale, nonché per visualizzare il nome del fuso orario nella console.  
  
 [!code-csharp[System.TimeZone2.Concepts#13](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#13)]
 [!code-vb[System.TimeZone2.Concepts#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#13)]  
  
 È necessario accedere sempre al fuso orario locale tramite la proprietà <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> anziché assegnare il fuso orario locale a una variabile oggetto <xref:System.TimeZoneInfo>.  Analogamente, è necessario accedere sempre all'ora UTC \(Coordinated Universal Time\) tramite la proprietà <xref:System.TimeZoneInfo.Utc%2A?displayProperty=fullName> anziché assegnare il fuso UTC a una variabile oggetto <xref:System.TimeZoneInfo>.  In questo modo si evita che la variabile oggetto <xref:System.TimeZoneInfo> venga invalidata da una chiamata al metodo <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName>.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare lo spazio dei nomi <xref:System> con l'istruzione `using` \(richiesto nel codice C\#\).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Ricerca dei fusi orari definiti in un sistema locale](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)   
 [Procedura: creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md)