---
title: "exceptionSwallowedOnCallFromCom MDA | Microsoft Docs"
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
  - "messages, informational"
  - "informational messages"
  - "managed debugging assistants (MDAs), exceptions"
  - "exception handling, managed debugging assistants"
  - "MDAs (managed debugging assistants), exceptions"
  - "ExceptionSwallowedOnCallFromCOM MDA"
ms.assetid: 55d6ab12-f251-4aab-aa64-aacbe9d9f974
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# exceptionSwallowedOnCallFromCom MDA
L'assistente al debug gestito `exceptionSwallowedOnCallFromCOM` viene attivato alla generazione di un'eccezione da parte del codice Common Language Runtime \(CLR\) chiamato da COM mediante un metodo che non presenta un tipo restituito HRESULT non gestito.  
  
## Sintomi  
 Il valore restituito per una chiamata a un componente gestito da COM corrisponde a FALSE o a 0.  In alternativa, se il metodo presenta un tipo restituito void, potrebbero non esservi indicazioni relative alla generazione di un'eccezione durante l'esecuzione del metodo.  In tal caso, l'eccezione verrà intercettata senza avviso e l'esecuzione tornerà al chiamante COM.  
  
## Causa  
 È stata generata un'eccezione, ma non esiste un modo valido per segnalarla.  
  
## Risoluzione  
 Messaggio esclusivamente informativo. Non indica necessariamente la presenza di un bug.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  Si limita a restituire dati relativi alle eccezioni intercettate senza avviso.  
  
## Output  
 Messaggio informativo contenente il nome del metodo, il nome del tipo e il messaggio dell'eccezione.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <exceptionSwallowedOnCallFromCom />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)