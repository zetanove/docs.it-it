---
title: "Eventi ETW nella libreria TPL (Task Parallel Library) e PLINQ | Microsoft Docs"
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
  - "attività, eventi ETW"
ms.assetid: 87a9cff5-d86f-4e44-a06e-d12764d0dce2
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Eventi ETW nella libreria TPL (Task Parallel Library) e PLINQ
La libreria TPL \(Task Parallel Library\) e PLINQ generano entrambi eventi ETW \(Event Trace for Windows\) che è possibile utilizzare per profilare e risolvere i problemi relativi ad applicazioni tramite strumenti quale l'Analizzatore prestazioni Windows.  Tuttavia, nella maggior parte degli scenari, il modo migliore per profilare il codice dell'applicazione parallela consiste nell'utilizzo di [Visualizzatore di concorrenze](../Topic/Concurrency%20Visualizer.md) in [!INCLUDE[vsUltShort](../../../includes/vsultshort-md.md)].  
  
## Eventi ETW della libreria TPL \(Task Parallel Library\)  
 Nella struttura EVENT\_HEADER, il GUID di ProviderId per gli eventi generati da <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>, <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=fullName> è:  
  
```  
0x2e5dba47, 0xa3d2, 0x4d16, 0x8e, 0xe0, 0x66, 0x71, 0xff, 0xdc, 0xd7, 0xb5  
```  
  
### Inizio del ciclo parallelo  
 EVENT\_DESCRIPTOR.Task \= 1  
  
 EVENT\_DESCRIPTOR.Id \= 1  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Identificatore univoco utilizzato per indicare l'annidamento e coppie per gli eventi con semantica di divisione\/unione.|  
|OperationType|<xref:System.Int32?displayProperty=fullName>|Indica il tipo di ciclo:<br /><br /> 1 \= ParallelInvoke<br /><br /> 2 \= ParallelFor<br /><br /> 3 \= ParallelForEach|  
|InclusiveFrom|<xref:System.Int64?displayProperty=fullName>|Valore iniziale del contatore di cicli.|  
|ExclusiveTo|<xref:System.Int64?displayProperty=fullName>|Valore finale del contatore di cicli.|  
  
### Fine del ciclo parallelo  
 EVENT\_DESCRIPTOR.Task \= 2  
  
 EVENT\_DESCRIPTOR.Id \= 2  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Identificatore univoco utilizzato per indicare l'annidamento e coppie per gli eventi con semantica di divisione\/unione.|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|Numero totale di iterazioni.|  
  
### Inizio della chiamata parallela  
 EVENT\_DESCRIPTOR.Task \= 3  
  
 EVENT\_DESCRIPTOR.Id \= 3  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Identificatore univoco utilizzato per indicare l'annidamento e coppie per gli eventi con semantica di divisione\/unione.|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|Numero totale di iterazioni.|  
|operationType|<xref:System.Int32?displayProperty=fullName>|Indica il tipo di ciclo:<br /><br /> 1 \= ParallelInvoke<br /><br /> 2 \= ParallelFor<br /><br /> 3 \= ParallelForEach|  
|ActionCount|<xref:System.Int32?displayProperty=fullName>|Numero di azioni che saranno eseguite nella chiamata parallela.|  
  
### Fine della chiamata parallela  
 EVENT\_DESCRIPTOR.Task \= 4  
  
 EVENT\_DESCRIPTOR.Id \= 4  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|Identificatore univoco utilizzato per indicare l'annidamento e coppie per gli eventi con semantica di divisione\/unione.|  
  
## Eventi ETW di PLINQ  
 Il GUID di EVENT\_HEADER.ProviderId per PLINQ è:  
  
```  
0x159eeeec, 0x4a14, 0x4418, 0xa8, 0xfe, 0xfa, 0xab, 0xcd, 0x98, 0x78, 0x87  
```  
  
### Inizio della query parallela  
 EVENT\_DESCRIPTOR.Task \= 1  
  
 EVENT\_DESCRIPTOR.Id \= 1  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|Identificatore di query univoco.|  
  
### Fine della query parallela  
 EVENT\_DESCRIPTOR.Task \= 2  
  
 EVENT\_DESCRIPTOR.Id \= 2  
  
#### User Data  
  
|**Nome**|**Type**|**Descrizione**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|ID dell'oggetto TaskScheduler che ha avviato il ciclo.|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|ID dell'attività che ha avviato il ciclo.|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|Identificatore di query univoco.|  
  
## Vedere anche  
 [ETW Events in the .NET Framework](../../../docs/framework/performance/etw-events.md)   
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)