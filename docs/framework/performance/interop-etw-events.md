---
title: "Interop ETW Events | Microsoft Docs"
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
  - "interop events [.NET Framework]"
  - "ETW, interop events (CLR)"
ms.assetid: eb6eac2e-45f4-4923-a32c-38f203da66df
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Interop ETW Events
<a name="top"></a> Gli eventi di interoperabilità acquisiscono informazioni sulla generazione di stub e la memorizzazione nella cache di Microsoft Intermediate Language \(MSIL\).  
  
 Questa categoria include i seguenti eventi:  
  
-   [Evento ILStubGenerated](#ilstubgenerated_event)  
  
-   [Evento ILStubCacheHit](#ilstubcachehit_event)  
  
<a name="ilstubgenerated_event"></a>   
## Evento ILStubGenerated  
 La tabella seguente illustra la parola chiave e il livello Per altre informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`InteropKeyword` \(0x2000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`ILStubGenerated`|88|È stato generato lo stub MSIL.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|ModuleID|win:UInt16|L’identificatore del modulo.|  
|StubMethodID|win:UInt64|L’identificatore del metodo stub.|  
|StubFlags|win:UInt64|Flag per lo stub:<br /><br /> 0x1 \- Interoperabilità inversa.<br /><br /> 0x2 \- interoperabilità COM.<br /><br /> 0x4 \- stub generato da NGen.exe.<br /><br /> 0x8 \- Delegato.<br /><br /> 0x10 \- Argomento variabile.<br /><br /> 0x20 \- Computer chiamato non gestito.|  
|ManagedInteropMethodToken|win:UInt32|Il token per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodNameSpace|win:UnicodeString|Lo spazio dei nomi per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodName|win:UnicodeString|Il nome per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodSignature|win:UnicodeString|La firma per il metodo di interoperabilità gestito.|  
|NativeMethodSignature|win:UnicodeString|La firma del metodo nativo.|  
|StubMethodSignature|win:UnicodeString|La firma del metodo stub.|  
|StubMethodILCode|win:UnicodeString|Il codice MSIL per il metodo stub.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="ilstubcachehit_event"></a>   
## Evento ILStubCacheHit  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`InteropKeyword` \(0x2000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`ILStubCacheHit`|89|La cache MSIL ha avuto accesso.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|ModuleID|win:UInt16|L’identificatore del modulo.|  
|StubMethodID|win:UInt64|L’identificatore del metodo stub.|  
|ManagedInteropMethodToken|win:UInt32|Il token per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodNameSpace|win:UnicodeString|Lo spazio dei nomi per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodName|win:UnicodeString|Il nome per il metodo di interoperabilità gestito.|  
|ManagedInteropMethodSignature|win:UnicodeString|La firma per il metodo di interoperabilità gestito.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)