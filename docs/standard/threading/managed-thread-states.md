---
title: "Stati dei thread gestiti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "threading [.NET Framework], stati"
ms.assetid: 63890d5e-6025-4a7c-aaf0-d8bfd54b455f
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Stati dei thread gestiti
La proprietà <xref:System.Threading.Thread.ThreadState%2A?displayProperty=fullName> fornisce una maschera di bit che indica lo stato corrente del thread. Un thread si trova sempre in almeno uno degli stati possibili nell'enumerazione <xref:System.Threading.ThreadState> e può essere contemporaneamente in più stati.  
  
> [!IMPORTANT]
>  Lo stato del thread è importante solo in alcuni scenari di debug. Il codice non deve mai usare lo stato del thread per sincronizzare le attività dei thread.  
  
 Quando si crea un thread gestito, viene visualizzato in stato <xref:System.Threading.ThreadState>. Il thread rimane in stato <xref:System.Threading.ThreadState> fino a quando il sistema operativo non lo sposta in stato avviato. La chiamata <xref:System.Threading.Thread.Start%2A> informa il sistema operativo che può essere avviato il thread. Lo stato del thread non viene modificato.  
  
 I thread non gestiti che accedono all'ambiente gestito si trovano già in stato avviato. Quando un thread è in stato avviato, diverse azioni possono modificarne lo stato. La tabella seguente elenca le azioni che causano una modifica di stato e il nuovo stato corrispondente.  
  
|Operazione|Nuovo stato risultante|  
|----------------|----------------------------|  
|Viene chiamato il costruttore per la classe <xref:System.Threading.Thread>.|<xref:System.Threading.ThreadState>|  
|<xref:System.Threading.Thread.Start%2A?displayProperty=fullName> viene chiamato da un altro thread.|<xref:System.Threading.ThreadState>|  
|Il thread risponde a <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> e avvia l'esecuzione.|<xref:System.Threading.ThreadState>|  
|Il thread chiama <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>.|<xref:System.Threading.ThreadState>|  
|Il thread chiama <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName> in un altro oggetto.|<xref:System.Threading.ThreadState>|  
|Il thread chiama <xref:System.Threading.Thread.Join%2A?displayProperty=fullName> in un altro thread.|<xref:System.Threading.ThreadState>|  
|<xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> viene chiamato da un altro thread.|<xref:System.Threading.ThreadState>|  
|Il thread risponde a una richiesta <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>.|<xref:System.Threading.ThreadState>|  
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> viene chiamato da un altro thread.|<xref:System.Threading.ThreadState>|  
|<xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> viene chiamato da un altro thread.|<xref:System.Threading.ThreadState>|  
|Il thread risponde a <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>.|<xref:System.Threading.ThreadState>, quindi <xref:System.Threading.ThreadState>|  
  
 Poiché lo stato <xref:System.Threading.ThreadState> ha un valore 0, non è possibile eseguire un test dei bit per individuare lo stato. Al suo posto, usare il test seguente \(in pseudocodice\):  
  
```  
if ((state & (Unstarted | Stopped)) == 0)   // implies Running     
```  
  
 In uno specifico momento, i thread spesso sono in più di uno stato. Ad esempio, se un thread è bloccato in una chiamata <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName> e un altro thread chiama <xref:System.Threading.Thread.Abort%2A> nello stesso thread, il thread sarà contemporaneamente nello stato <xref:System.Threading.ThreadState> e <xref:System.Threading.ThreadState>. In tal caso, non appena il thread viene restituito dalla chiamata a <xref:System.Threading.Monitor.Wait%2A> o viene interrotto, riceve <xref:System.Threading.ThreadAbortException>.  
  
 Quando un thread lascia lo stato <xref:System.Threading.ThreadState> in seguito a una chiamata a <xref:System.Threading.Thread.Start%2A>, non può più tornare allo stato <xref:System.Threading.ThreadState>. Un thread non può mai lasciare lo stato <xref:System.Threading.ThreadState>.  
  
## Vedere anche  
 <xref:System.Threading.ThreadAbortException>   
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadState>   
 [Threading](../../../docs/standard/threading/index.md)