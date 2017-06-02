---
title: "raceOnRCWCleanup MDA | Microsoft Docs"
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
  - "RCW"
  - "managed debugging assistants (MDAs), RCWs"
  - "race on RCW cleanup"
  - "MDAs (managed debugging assistants), RCWs"
  - "RaceOnRCWCleanup MDA"
  - "runtime callable wrappers"
ms.assetid: bee1e9b1-50a8-4c89-9cd9-7dd6b2458187
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# raceOnRCWCleanup MDA
L'assistente al debug gestito `raceOnRCWCleanup` viene attivato quando Common Language Runtime \(CLR\) rileva che è in uso un [Runtime Callable Wrapper](../../../docs/framework/interop/runtime-callable-wrapper.md) \(RCW\) quando viene eseguita una chiamata per rilasciarlo con un comando come il metodo <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=fullName>.  
  
## Sintomi  
 Violazioni di accesso o danneggiamento della memoria durante o dopo il rilascio di un RCW con <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> o un metodo simile.  
  
## Causa  
 Il wrapper RCW è in uso in un altro thread o durante il rilascio dello stack di thread.  Non è possibile rilasciare un RCW in uso.  
  
## Risoluzione  
 Non rilasciare un RCW che potrebbe essere in uso nel thread corrente o in altri.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 Messaggio che descrive l'errore.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <raceOnRCWCleanup/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)