---
title: "invalidFunctionPointerInDelegate MDA | Microsoft Docs"
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
  - "invalidFunctionPointerInDelegate MDA"
  - "managed debugging assistants (MDAs), invalid function pointer to delegates"
  - "MDAs (managed debugging assistants), invalid function pointer to delegates"
  - "function pointers, invalid"
  - "marshaling, run-time errors"
  - "managed debugging assistants (MDAs), marshaling"
  - "MDAs (managed debugging assistants), marshaling"
  - "invalid function pointers"
ms.assetid: 99ae44f1-783e-49a9-9009-24f54bbd0f09
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# invalidFunctionPointerInDelegate MDA
L'assistente al debug gestito `invalidFunctionPointerInDelegate` viene attivato quando viene passato un puntatore a funzione non valido per costruire un delegato su un puntatore a funzione nativo.  
  
## Sintomi  
 Violazioni di accesso o danneggiamento imprevisto della memoria quando viene usato un delegato su un puntatore a funzione.  
  
## Causa  
 È stato specificato un puntatore a funzione non valido.  
  
## Risoluzione  
 Specificare un puntatore a funzione valido  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 Il puntatore a funzione non valido.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidFunctionPointerInDelegate />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)