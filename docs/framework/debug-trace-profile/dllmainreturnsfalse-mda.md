---
title: "dllMainReturnsFalse MDA | Microsoft Docs"
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
  - "managed debugging assistants (MDAs), DllMain returns false"
  - "DllMainReturnsFalse MDA"
  - "DllMain function"
  - "MDAs (managed debugging assistants), DllMain returns false"
ms.assetid: e2abdd04-f571-4b97-8c16-2221b8588429
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# dllMainReturnsFalse MDA
L'assistente al debug gestito `dllMainReturnsFalse` viene attivato se la funzione `DllMain` gestita di un assembly utente, chiamata per il motivo DLL\_PROCESS\_ATTACH, restituisce FALSE.  
  
## Sintomi  
 La funzione `DllMain` ha restituito FALSE, valore che ne indica l'esecuzione non corretta.  Ciò può provocare problemi imprevisti in quanto le funzioni `DllMain` generalmente contengono codice di inizializzazione importante.  
  
## Causa  
 La funzione `DllMain` viene chiamata per il motivo DLL\_PROCESS\_ATTACH per l'inizializzazione della DLL al caricamento.  Se restituisce FALSE, l'inizializzazione della DLL ha avuto esito negativo.  
  
## Risoluzione  
 Analizzare il codice della funzione `DllMain` della DLL non riuscita e identificare la causa dell'errore di inizializzazione.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  Si limita a generare un report dei dati relativi al valore restituito per la funzione `DllMain`.  
  
## Output  
 Un messaggio nel quale è indicato che una funzione `DllMain`, chiamata per il motivo DLL\_PROCESS\_ATTACH, ha restituito FALSE.  Questo assistente al debug gestito viene attivato solo se la funzione `DllMain` viene implementata nel codice gestito.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <dllMainReturnsFalse />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)