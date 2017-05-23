---
title: 'Mitigazione: chiamate al metodo EventSource.WriteEvent | Microsoft Docs'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 327a9fdb-ba8e-40f7-89e5-4c89b46e594f
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: cde809989d89c10caeb97ec853c8649a108cd72d
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-eventsourcewriteevent-method-calls"></a>Mitigazione: chiamate al metodo EventSource.WriteEvent
[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] applica un contratto tra un metodo di evento ETW in una classe derivata da <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> e il metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> della relativa classe di base. Il metodo di evento ETW deve passare al metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> l'ID evento seguito dagli stessi argomenti passati al metodo dell'evento.  
  
## <a name="impact"></a>Impatto  
 Un metodo di evento ETW definito nel modo seguente rompe il contratto:  
  
```  
[Event(2, Level = EventLevel.Informational)]  
public void Info2(string message)  
{  
   base.WriteEvent(2, message, "-");  
}  
```  
  
 In caso di violazione del contratto, viene generata un'eccezione <xref:System.IndexOutOfRangeException> al momento del runtime se un oggetto <xref:System.Diagnostics.Tracing.EventListener> legge i dati <xref:System.Diagnostics.Tracing.EventSource> in esecuzione.  
  
 La definizione del metodo di evento ETW deve seguire un questo modello:  
  
```  
[Event(2, Level = EventLevel.Informational)]  
public void Info2(string message)  
{  
   base.WriteEvent(2, message);  
}  
```  
  
## <a name="mitigation"></a>Attenuazione  
 È necessario modificare il codice esistente per rispettare lo schema richiesto.  
  
 È possibile ridurre la quantità di codice da modificare definendo due metodi per chiamare il metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> come indicato di seguito:  
  
```  
[NonEvent]  
public void Info2(string message)  
{  
   Info2Internal(message, "-");  
}  
  
public void Info2Internal(string message, string prefix)  
{  
   WriteEvent(2, message, prefix);  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)

