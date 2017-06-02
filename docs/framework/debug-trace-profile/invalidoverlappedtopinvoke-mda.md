---
title: "invalidOverlappedToPinvoke MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "overlapped pointers"
  - "managed debugging assistants (MDAs), overlapped pointers"
  - "invalid overlapped pointer to platform invoke"
  - "InvalidOverlappedToPinvoke MDA"
  - "MDAs (managed debugging assistants), overlapped pointers"
  - "pointers, overlapped"
ms.assetid: 28876047-58bd-4fed-9452-c7da346d67c0
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# invalidOverlappedToPinvoke MDA
L'assistente al debug gestito \(MDA, Managed Debugging Assistant\) `invalidOverlappedToPinvoke` viene attivato quando un puntatore sovrapposto non creato nell'heap del Garbage Collection viene passato a specifiche funzioni Win32.  
  
> [!NOTE]
>  Per impostazione predefinita, questo MDA viene attivato solo se la chiamata platform invoke è definita nel codice e il debugger visualizza lo stato JustMyCode di ciascun metodo.  Questo assistente al debug gestito non viene attivato dai debugger che non sono in grado di comprendere JustMyCode, ad esempio MDbg.exe senza estensioni.  L'assistente al debug gestito può essere abilitato per i debugger utilizzando un file di configurazione e impostando in modo esplicito `justMyCode="false"` nel file .mda.config `(<invalidOverlappedToPinvoke enable="true" justMyCode="false"/>`\).  
  
## Sintomi  
 Blocco del sistema o danneggiamento inspiegabile dell'heap.  
  
## Causa  
 Un puntatore sovrapposto non creato nell'heap del Garbage Collection viene passato a specifiche funzioni del sistema operativo.  
  
 Nella tabella riportata di seguito sono elencate le funzioni controllate da questo assistente al debug gestito.  
  
|Modulo|Funzione|  
|------------|--------------|  
|HttpApi.dll|`HttpReceiveHttpRequest`|  
|IpHlpApi.dll|`NotifyAddrChange`|  
|kernel32.dll|`ReadFile`|  
|kernel32.dll|`ReadFileEx`|  
|kernel32.dll|`WriteFile`|  
|kernel32.dll|`WriteFileEx`|  
|kernel32.dll|`ReadDirectoryChangesW`|  
|kernel32.dll|`PostQueuedCompletionStatus`|  
|MSWSock.dll|`ConnectEx`|  
|WS2\_32.dll|`WSASend`|  
|WS2\_32.dll|`WSASendTo`|  
|WS2\_32.dll|`WSARecv`|  
|WS2\_32.dll|`WSARecvFrom`|  
|MQRT.dll|`MQReceiveMessage`|  
  
 La possibilità di danneggiamento dell'heap è elevata poiché la classe <xref:System.AppDomain> che esegue la chiamata potrebbe essere scaricata.  Se <xref:System.AppDomain> scarica, il codice dell'applicazione libererà la memoria per il puntatore sovrapposto, causando il danneggiamento al termine dell'operazione, oppure perderà la memoria, generando problemi in un secondo momento.  
  
## Risoluzione  
 Utilizzare un oggetto <xref:System.Threading.Overlapped>, chiamando il metodo <xref:System.Threading.Overlapped.Pack%2A> per ottenere una struttura <xref:System.Threading.NativeOverlapped> da passare alla funzione.  Se la classe <xref:System.AppDomain> viene scaricata, il puntatore verrà liberato solo al termine dell'operazione asincrona.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non ha alcun effetto su Common Language Runtime \(CLR\).  
  
## Output  
 Di seguito è riportato un esempio di output generato da questo assistente al debug gestito.  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the Win32 function 'WriteFile' in module 'KERNEL32.DLL'.  If the AppDomain is shut down, this can cause heap corruption when the async I/O completes.  The best solution is to pass a NativeOverlapped structure retrieved from a call to System.Threading.Overlapped.Pack().  If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidOverlappedToPinvoke/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)