---
title: "failedQI MDA | Microsoft Docs"
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
  - "failed QueryInterface"
  - "FailedQI MDA"
  - "QueryInterface call failures"
  - "MDAs (managed debugging assistants), failed QueryInterface"
  - "managed debugging assistants (MDAs), failed QueryInterface"
ms.assetid: 902dc863-34b3-477c-b433-b8a6bb6133c6
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# failedQI MDA
L'assistente al debug gestito `failedQI` viene attivato quando il runtime chiama `QueryInterface` su un puntatore a interfaccia COM per conto di un Runtime Callable Wrapper \(RWC\) e la chiamata `QueryInterface` non riesce.  
  
## Sintomi  
 Mancata riuscita di un cast su un RCW oppure errore imprevisto di una chiamata a COM da parte di un RCW.  
  
## Causa  
  
-   La chiamata viene effettuata da un contesto errato.  
  
-   Il proxy registrato non riesce a chiamare `QueryInterface` perché il tentativo di chiamata è stato effettuato nel contesto errato.  
  
-   Un proxy di proprietà di OLE ha restituito un HRESULT di errore.  
  
## Risoluzione  
 Vedere la documentazione MSDN relativa alle regole COM.  
  
## Effetto sull'ambiente di esecuzione  
 Se una chiamata a `QueryInterface` non riesce, viene cambiato il contesto e viene tentata di nuovo la chiamata a `QueryInterface` per verificare se l'errore è stato causato da un contesto errato.  
  
## Output  
 Il nome gestito e il GUID dell'interfaccia e l'oggetto HRESULT dell'errore.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <failedQI/>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)