---
title: "Attenuazione: chiamate al metodo EventSource.WriteEvent | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 327a9fdb-ba8e-40f7-89e5-4c89b46e594f
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Attenuazione: chiamate al metodo EventSource.WriteEvent
[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] applica un contratto tra un metodo di evento ETW in una classe derivata da <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> e il metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> della relativa classe di base. Il metodo di evento ETW deve passare al metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> l'ID evento seguito dagli stessi argomenti passati al metodo di evento.  
  
## Impatto  
 Un metodo di evento ETW definito nel modo seguente rompe il contratto:  
  
```  
  
[Event(2, Level = EventLevel.Informational)] public void Info2(string message) { base.WriteEvent(2, message, "-"); }  
  
```  
  
 Quando questo contratto viene violato, viene generata un’eccezione <xref:System.IndexOutOfRangeException> se un oggetto <xref:System.Diagnostics.Tracing.EventListener> legge i dati nel processo <xref:System.Diagnostics.Tracing.EventSource>.  
  
 La definizione del metodo di evento ETW deve seguire un questo modello:  
  
```  
  
[Event(2, Level = EventLevel.Informational)] public void Info2(string message) { base.WriteEvent(2, message); }  
  
```  
  
## Attenuazione  
 È necessario modificare il codice esistente per rispettare lo schema richiesto.  
  
 È possibile ridurre la quantità di codice che è necessario modificare definendo due metodi per chiamare il metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A>, come indicato di seguito:  
  
```  
  
[NonEvent] public void Info2(string message) { Info2Internal(message, "-"); } public void Info2Internal(string message, string prefix) { WriteEvent(2, message, prefix); }  
  
```  
  
## Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)