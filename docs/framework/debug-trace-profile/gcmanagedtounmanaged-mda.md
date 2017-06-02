---
title: "gcManagedToUnmanaged MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), garbage collection"
  - "GcManagedToUnmanaged MDA"
  - "GC managed to unmanaged"
  - "transitioning threads managed to unmanaged code"
  - "threading [.NET Framework], garbage collection"
  - "managed to unmanaged garbage collection"
  - "managed debugging assistants (MDAs), garbage collection"
  - "threading [.NET Framework], managed debugging assistants"
  - "garbage collection, run-time errors"
ms.assetid: 7417f837-805e-4fed-a430-ca919c8421dc
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# gcManagedToUnmanaged MDA
L'assistente al debug gestito `gcManagedToUnmanaged` determina un'operazione di Garbage Collection ogni volta che un thread passa dal codice gestito al codice non gestito.  
  
## Sintomi  
 Un componente utente non gestito genera una violazione di accesso quando si cerca di usare un oggetto gestito esposto a COM.  L'oggetto COM appare come rilasciato  e la violazione di accesso è non deterministica.  
  
## Causa  
 Se un componente non gestito non esegue correttamente il conteggio dei riferimenti a un oggetto COM gestito, il runtime potrebbe eseguire una Garbage Collection di un oggetto gestito esposto a COM mentre il componente gestito contiene ancora un riferimento all'oggetto.  Il runtime chiama il metodo <xref:System.Runtime.InteropServices.Marshal.Release%2A> durante le Garbage Collection. In questo modo, se il componente utente usa l'oggetto prima che si verifichi la Garbage Collection, non sarà ancora stato sottoposto all'operazione.  Da ciò deriva il non determinismo.  
  
## Risoluzione  
 L'attivazione di questo assistente consente di ridurre il periodo compreso tra il momento in cui l'oggetto è disponibile per la Garbage Collection e la chiamata di <xref:System.Runtime.InteropServices.Marshal.Release%2A> rendendo possibile tenere traccia del componente non gestito che tenta per primo di accedere all'oggetto sottoposto a Garbage Collection.  
  
## Effetto sull'ambiente di esecuzione  
 Viene causata una Garbage Collection ogni volta che un thread passa dal codice gestito al codice non gestito.  
  
## Output  
 Questo assistente al debug gestito non produce output.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <gcManagedToUnmanaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)   
 [gcUnmanagedToManaged](../../../docs/framework/debug-trace-profile/gcunmanagedtomanaged-mda.md)