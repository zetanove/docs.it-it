---
title: "Stack ETW Event | Microsoft Docs"
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
  - "stack event [.NET Framework]"
  - "ETW, stack event (CLR)"
ms.assetid: f612fa5b-4b62-4593-a19e-85c9b1018dce
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# Stack ETW Event
L'evento di stack deve essere utilizzato con gli altri eventi per generare tracce dello stack dopo che è stato generato un evento.  Viene registrato quando il provider di runtime è abilitato.  Si tratta di un evento a frequenza molto elevata in quanto viene generato a ogni generazione di un altro evento di runtime.  Per questo motivo si consiglia di utilizzare l'evento con cautela.  
  
 Nella tabella seguente vengono riportate le parole chiave e il livello. Per ulteriori informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`StackKeyword` \(0x40000000\)|LogAlways\(0\)|  
  
 Nella tabella riportata di seguito vengono illustrate le informazioni sull'evento.  
  
|Evento|ID evento|Condizione di generazione|  
|------------|---------------|-------------------------------|  
|`CLRStackWalk`|82|Insieme ad altri eventi per generare tracce dello stack successive a un evento.|  
  
 Nella tabella riportata di seguito vengono illustrati i dati relativi all'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|ClrInstanceID|win:Uint16|Identificatore di runtime univoco.|  
|Reserved1|win:UInt8|Riservato.|  
|Reserved2|win:UInt8|Riservato.|  
|FrameCount|win:UInt32|Numero di frame nella traccia dello stack.|  
|Stack|win:Pointer|Colonne di puntatori all'istruzione.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)