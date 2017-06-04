---
title: "Exception Thrown_V1 ETW Event | Microsoft Docs"
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
  - "ExceptionThrown_V1 event [.NET Framework]"
  - "ETW, ExceptionThrown_V1 event (CLR)"
ms.assetid: 0d3da389-6b7b-40f6-a877-fac546d6019c
caps.latest.revision: 6
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 6
---
# Exception Thrown_V1 ETW Event
Questo evento acquisisce le informazioni sulle eccezioni generate.  
  
 Nella tabella riportata di seguito vengono mostrate le parole chiave con cui viene generato l'evento e il livello dell'evento. Per ulteriori informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ExceptionKeyword` \(0x8000\)|Warning \(2\)|  
  
 Nella tabella riportata di seguito vengono illustrate le informazioni sull'evento.  
  
|Evento|ID evento|Condizione di generazione|  
|------------|---------------|-------------------------------|  
|`ExceptionThrown_V1`|80|Viene generata un'eccezione gestita.|  
  
 Nella tabella riportata di seguito vengono illustrati i dati relativi all'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Tipo di eccezione|win:UnicodeString|Tipo dell'eccezione, ad esempio `System.NullReferenceException`.|  
|Exception Message|win:UnicodeString|Messaggio effettivo dell'eccezione.|  
|EIPCodeThrow|win:Pointer|Puntatore all'istruzione in cui si è verificata l'eccezione.|  
|ExceptionHR|win:UInt32|Eccezione [HRESULT](http://go.microsoft.com/fwlink/?LinkId=179679).|  
|ExceptionFlags|win:UInt16|0x01: HasInnerException \(vedere [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md) nella documentazione di Visual Basic\).<br /><br /> 0x02: IsNestedException.<br /><br /> 0x04: IsRethrownException.<br /><br /> 0x08: IsCorruptedStateException \(indica che lo stato di processo è danneggiato; vedere [Gestione di eccezioni di stato danneggiato](http://go.microsoft.com/fwlink/?LinkId=179681) su MSDN\).<br /><br /> 0x10: IsCLSCompliant \(un'eccezione derivante da <xref:System.Exception> è conforme a CLS; in caso contrario, non è conforme a CLS\).|  
|ClrInstanceID|win:UInt16|ID univoco dell'istanza di CLR o CoreCLR.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)