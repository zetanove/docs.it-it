---
title: "illegalPrepareConstrainedRegion MDA | Microsoft Docs"
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
  - "PrepareConstrainedRegions method"
  - "managed debugging assistants (MDAs), illegal PrepareConstrainedRegions"
  - "try/catch exception handling, managed debugging assistants"
  - "IllegalPrepareConstrainedRegions MDA"
  - "MDAs (managed debugging assistants), illegal PrepareConstrainedRegions"
ms.assetid: 2f9b5031-f910-4e01-a196-f89eab313eaf
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# illegalPrepareConstrainedRegion MDA
L'assistente al debug gestito `illegalPrepareConstrainedRegion` viene attivato quando una chiamata al metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A?displayProperty=fullName> non precede immediatamente l'istruzione `try` del gestore eccezioni.  Questa restrizione è valida al livello MSIL. È pertanto consentito che siano presenti origini che non generano codice tra la chiamata e l'istruzione `try`, come i commenti.  
  
## Sintomi  
 Un'area a esecuzione vincolata \(CER, Constrained Execution Region\) che non viene mai considerata come tale, bensì come semplice blocco di gestione delle eccezioni \(`finally` o `catch`\).  Di conseguenza, l'area non viene eseguita nel caso di una condizione di memoria insufficiente o di interruzione di un thread in modo imprevisto.  
  
## Causa  
 Il modello di preparazione di una CER non è stato seguito correttamente.  Si tratta di un evento di errore.  La chiamata al metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> utilizzata per contrassegnare i gestori eccezioni durante l'introduzione di una CER nei blocchi `catch`\/`finally`\/`fault`\/`filter` associati deve essere utilizzata prima dell'istruzione `try`.  
  
## Risoluzione  
 Verificare che la chiamata al metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> venga effettuata prima dell'istruzione `try` `` .  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  
  
## Output  
 L'assistente al debug gestito visualizza il nome del metodo che chiama il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>, l'offset MSIL e un messaggio nel quale viene indicato che la chiamata non precede l'inizio del blocco try.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <illegalPrepareConstrainedRegion/>  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato il modello che determina l'attivazione dell'assistente al debug gestito di questo argomento.  
  
```  
void MethodWithInvalidPCR()  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    Object o = new Object();  
    try  
    {  
        …  
    }  
    finally  
    {  
        …  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)