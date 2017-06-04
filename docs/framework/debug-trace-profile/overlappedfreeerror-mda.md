---
title: "overlappedFreeError MDA | Microsoft Docs"
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
  - "OverlappedFreeError MDA"
  - "overlapped free method call error"
  - "managed debugging assistants (MDAs), overlapped structures"
  - "overlapped structures"
  - "MDAs (managed debugging assistants), overlapped structures"
  - "freeing overlapped structures"
ms.assetid: b6ab2d48-6eee-4bab-97a3-046b3b0a5470
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# overlappedFreeError MDA
L'assistente al debug gestito `overlappedFreeError` viene attivato quando il metodo <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29?displayProperty=fullName> viene chiamato prima del completamento dell'operazione sovrapposta.  
  
## Sintomi  
 Violazioni di accesso o danneggiamento dell'heap sottoposto a Garbage Collection.  
  
## Causa  
 Una struttura sovrapposta è stata liberata prima del completamento dell'operazione.  È quindi possibile che la funzione che utilizza il puntatore sovrapposto scriva nella struttura dopo che questa è stata liberata.  Ciò può causare il danneggiamento dell'heap poiché tale area potrebbe essere già stata occupata da un altro oggetto.  
  
 Questo assistente al debug gestito può non rappresentare un errore se l'operazione sovrapposta non è stata avviata correttamente.  
  
## Risoluzione  
 Assicurarsi che l'operazione di I\/O in cui viene utilizzata la struttura sovrapposta sia completata prima della chiamata al metodo <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29>.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
 Di seguito è riportato un esempio di output relativo a questo assistente al debug gestito.  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the win32 function 'WriteFile' in module 'KERNEL32.DLL'.  If the AppDomain is shut down, this can cause heap corruption when the async I/O completes.  The best solution is to pass a NativeOverlappedStructure retrieved from a call to System.Threading.Overlapped.Pack().  If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <overlappedFreeError/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)