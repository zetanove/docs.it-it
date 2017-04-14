---
title: "Procedura: creare fusi orari senza regole di regolazione | Microsoft Docs"
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
  - "regolazione (regola) [.NET Framework]"
  - "fusi orari [.NET Framework], regola di regolazione"
  - "fusi orari [.NET Framework], creazione"
ms.assetid: a6af8647-7893-4f29-95a9-d94c65a6e8dd
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare fusi orari senza regole di regolazione
Le informazioni precise del fuso orario richieste da un'applicazione possono non essere presenti in un determinato sistema per molte ragioni:  
  
-   Il fuso orario non è mai stato definito nel Registro di sistema locale.  
  
-   I dati sul fuso orario sono stati modificati o rimossi dal Registro di sistema.  
  
-   Il fuso orario esiste ma non ha informazioni accurate sulle regolazioni del fuso orario per un determinato periodo storico.  
  
 In questi casi, è possibile chiamare il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> per definire il fuso orario richiesto dall'applicazione.  È possibile utilizzare gli overload di questo metodo per creare un fuso orario con o senza regole di regolazione.  Se il fuso orario supporta l'ora legale, è possibile definire le regolazioni con regole di regolazione fisse o mobili. Per le definizioni di questi termini, vedere la sezione "Terminologia relativa al fuso orario" in [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).  
  
> [!IMPORTANT]
>  I fusi orari personalizzati creati chiamando il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> non vengono aggiunti al Registro di sistema,  ma è possibile accedervi solo tramite il riferimento all'oggetto restituito dalla chiamata al metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>.  
  
 In questo argomento viene illustrato come creare un fuso orario senza regole di regolazione.  Per creare un fuso orario che supporti le regole di regolazione dell'ora legale, vedere [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md).  
  
### Per creare un fuso orario senza regole di regolazione  
  
1.  Definire il nome visualizzato del fuso orario.  
  
     Il nome visualizzato segue un formato quasi standard in cui l'offset del fuso orario dall'ora UTC \(Coordinated Universal Time\) viene racchiuso tra parentesi e seguito da una stringa che identifica il fuso orario, una o più città del fuso orario o uno o più paesi o regioni del fuso orario.  
  
2.  Definire il nome dell'ora solare del fuso orario.  In genere questa stringa viene utilizzata anche come identificatore del fuso orario.  
  
3.  Se si desidera utilizzare un identificatore diverso dal nome standard del fuso orario, definire l'identificatore del fuso orario.  
  
4.  Creare un'istanza di un oggetto <xref:System.TimeSpan> che definisce l'offset del fuso orario dall'ora UTC.  I fusi orari con ore in avanti rispetto all'ora UTC hanno un offset positivo.  I fusi orari con ore indietro rispetto all'ora UTC hanno un offset negativo.  
  
5.  Chiamare il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%29?displayProperty=fullName> per creare un'istanza del nuovo fuso orario.  
  
## Esempio  
 Nell'esempio seguente viene definito un fuso orario personalizzato per Mawson, Antartide senza regole di regolazione.  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#1)]
 [!code-vb[System.TimeZone2.CreateTimeZone#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#1)]  
  
 La stringa assegnata alla proprietà <xref:System.TimeZoneInfo.DisplayName%2A> segue un formato standard in cui l'offset del fuso orario dall'ora UTC è seguito da una semplice descrizione del fuso orario.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare gli spazi dei nomi seguenti:  
  
     [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
     [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md)   
 [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)