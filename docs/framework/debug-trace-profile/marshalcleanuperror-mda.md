---
title: "marshalCleanupError MDA | Microsoft Docs"
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
  - "cleanup operations"
  - "marshaling, run-time errors"
  - "managed debugging assistants (MDAs), marshaling"
  - "MDAs (managed debugging assistants), marshaling"
  - "marshaling cleanup error"
  - "MarshalCleanupError MDA"
  - "memory, cleanup errors"
ms.assetid: 2f5d9e7c-ae51-4155-a435-54347aa1f091
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# marshalCleanupError MDA
L'assistente al debug gestito `marshalCleanupError` viene attivato quando in Common Language Runtime si verifica un errore durante il tentativo di eseguire la pulizia di strutture temporanee e della memoria usata per il marshalling dei tipi di dati tra limiti del codice gestito e nativo.  
  
## Sintomi  
 Si verifica una perdita di memoria durante transizioni di codice gestito e nativo, lo stato di esecuzione, ad esempio le impostazioni cultura del thread, non viene ripristinato o si verificano errori durante la pulizia di <xref:System.Runtime.InteropServices.SafeHandle>.  
  
## Causa  
 Si è verificato un errore imprevisto durante la pulizia delle strutture temporanee.  
  
## Risoluzione  
 Rivedere tutte le implementazioni del marshaler personalizzato, del finalizzatore e del distruttore <xref:System.Runtime.InteropServices.SafeHandle> per individuare eventuali errori.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 Un messaggio che indica l'operazione non riuscita durante la pulizia.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <marshalCleanupError />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)