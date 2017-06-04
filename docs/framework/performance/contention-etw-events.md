---
title: "Contention ETW Events | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contention events [.NET Framework]"
  - "ETW, contention events (CLR)"
ms.assetid: 6933e753-2f2a-425b-ae84-42138c957d76
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Contention ETW Events
Gli eventi di conflitto vengono generati ogni qualvolta si verifica un conflitto per i blocchi <xref:System.Threading.Monitor?displayProperty=fullName> o nativi utilizzati dal runtime.  Il conflitto si verifica quando un thread attende un blocco mentre un altro thread possiede tale blocco.  
  
 Nella tabella riportata di seguito vengono mostrata le parole chiave con cui vengono generati gli eventi e il livello degli eventi. Per ulteriori informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ContentionKeyword` \(0x4000\)|Informational \(4\)|  
  
 Nella tabella riportata di seguito vengono illustrate le informazioni sull'evento.  
  
|Evento|ID evento|Condizione di generazione|  
|------------|---------------|-------------------------------|  
|`ContentionStart_V1`|81|Inizio del conflitto.  Questo evento non include il tempo di rotazione che intercorre prima che un thread attenda l'acquisizione di un blocco; viene generato soltanto quando il thread attende di acquisire un blocco.|  
|`ContentionStop`|81|Fine del conflitto.|  
  
 Nella tabella riportata di seguito vengono illustrati i dati relativi all'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Flag|win:UInt8|0 per gestito, 1 per nativo.|  
|ClrInstanceID|win:UInt16|ID univoco dell'istanza di CLR.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)