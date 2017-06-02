---
title: "Runtime Information ETW Events | Microsoft Docs"
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
  - "runtime information events [.NET Framework]"
  - "ETW, runtime information events"
ms.assetid: 68b4edbc-7f3b-45f6-ab75-4fd066d6af9a
caps.latest.revision: 6
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 6
---
# Runtime Information ETW Events
Questi eventi ETW registrano le informazioni sul runtime, inclusi la SKU, il numero di versione, la modalità di attivazione del runtime, i parametri della riga di comando con i quali è stato avviato, il GUID \(se applicabile\) e altre informazioni pertinenti.  Se all'interno di un processo vengono eseguiti più runtime, le informazioni fornite da questi eventi \(ClrInstanceID\) consentono di distinguere i vari runtime.  
  
 Nella tabella riportata di seguito vengono illustrati i due eventi di informazione di runtime.  Gli eventi possono essere generati con qualsiasi parola chiave o maschera. Per ulteriori informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Evento|ID evento|Provider|Descrizione|  
|------------|---------------|--------------|-----------------|  
|`RuntimeInformationEvent`|187|CLRRuntime|Generato in seguito al caricamento di un runtime.|  
|`RuntimeInformationDCStart`|187|CLRRundown|Enumera i runtime caricati.|  
  
 Nella tabella riportata di seguito vengono illustrati i dati relativi all'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|ClrInstanceID|win:UInt16|ID univoco dell'istanza di CLR o CoreCLR.|  
|Sku|win:UInt16|1 – CLR desktop.<br /><br /> 2 – CoreCLR.|  
|BclVersion – Major Version|win:UInt16|Versione principale di mscorlib.dll.|  
|BclVersion – Minor Version|win:UInt16|Numero di versione secondaria di mscorlib.dll.|  
|BclVersion – Build Number|win:UInt16|Numero di build di mscorlib.dll.|  
|BclVersion – QFE|win:UInt16|Numero di versione dell'aggiornamento rapido di mscorlib.dll.|  
|VMVersion – Major Version|win:UInt16|Versione di clr.dll o coreclr.dll in base alla SKU.|  
|VMVersion – Minor Version|win:UInt16|Versione secondaria di clr.dll o coreclr.dll in base alla SKU.|  
|VMVersion – Build Number|win:UInt16|Numero di build di clr.dll o coreclr.dll.|  
|VMVersion – QFE|win:UInt16|Numero di versione dell'aggiornamento rapido di clr.dll o coreclr.dll.|  
|StartupFlags|win:UInt32|Contrassegni di avvio definiti in mscoree.h.|  
|StartupMode|win:UInt8|0x01 \- Eseguibile gestito.<br /><br /> 0x02 \- CLR ospitato.<br /><br /> 0x04 \- C\+\+ gestito di interoperabilità.<br /><br /> 0x08 \- Attivato da COM.<br /><br /> 0x10 \- Altro.|  
|CommandLine|win:UnicodeString|Diverso da null solo se StartupMode\=0x01.|  
|ComObjectGUID|win:GUID|Diverso da null solo se StartupMode\=0x08.|  
|RuntimeDLLPath|win:UnicodeString|Percorso del file con estensione dll di CLR caricato nel processo.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)