---
title: "invalidGCHandleCookie MDA | Microsoft Docs"
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
  - "MDAs (managed debugging assistants), invalid cookies"
  - "cookies, invalid"
  - "managed debugging assistants (MDAs), invalid cookies"
  - "InvalidGCHandleCookie MDA"
  - "invalid cookies"
ms.assetid: 613ad742-3c11-401d-a6b3-893ceb8de4f8
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# invalidGCHandleCookie MDA
L'assistente al debug gestito `invalidGCHandleCookie` viene attivato quando viene effettuato un tentativo di conversione da un cookie <xref:System.IntPtr> non valido in un <xref:System.Runtime.InteropServices.GCHandle>.  
  
## Sintomi  
 Un comportamento indefinito, come le violazioni di accesso e il danneggiamento della memoria, durante il tentativo di utilizzo o di recupero di un <xref:System.Runtime.InteropServices.GCHandle> da un <xref:System.IntPtr>.  
  
## Causa  
 Il cookie probabilmente non è valido perché non è stato originariamente creato da un <xref:System.Runtime.InteropServices.GCHandle>, rappresenta un <xref:System.Runtime.InteropServices.GCHandle> già liberato, è il cookie di un <xref:System.Runtime.InteropServices.GCHandle> di un dominio applicazione diverso oppure è stato sottoposto a marshalling nel codice nativo come <xref:System.Runtime.InteropServices.GCHandle>, ma passato come <xref:System.IntPtr> a CLR, dove è stato tentato un cast.  
  
## Risoluzione  
 Specificare un cookie <xref:System.IntPtr> valido per <xref:System.Runtime.InteropServices.GCHandle>.  
  
## Effetto sul runtime  
 Quando questo assistente viene attivato, il debugger non è più in grado di ricondurre le radici ai relativi oggetti in quanto i valori del cookie passati sono diversi da quelli restituiti quando l'assistente in oggetto non è attivato.  
  
## Output  
 Il valore del cookie <xref:System.IntPtr> non valido viene inserito nel report.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <invalidGCHandleCookie />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.GCHandle.FromIntPtr%2A>   
 <xref:System.Runtime.InteropServices.GCHandle>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)