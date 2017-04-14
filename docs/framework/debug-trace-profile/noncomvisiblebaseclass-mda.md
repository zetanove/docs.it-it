---
title: "nonComVisibleBaseClass MDA | Microsoft Docs"
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
  - "visible classes"
  - "managed debugging assistants (MDAs), COM visible classes"
  - "nonComVisibleBaseClass MDA"
  - "COM visible classes"
  - "QueryInterface call failures"
  - "MDAs (managed debugging assistants), COM visible classes"
ms.assetid: 9ec1af27-604b-477e-9ee2-e833eb10d3ce
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# nonComVisibleBaseClass MDA
L'assistente al debug gestito `nonComVisibleBaseClass` viene attivato quando viene effettuata una chiamata `QueryInterface` da codice nativo o non gestito nel CCW \(COM Callable Wrapper\) di una classe gestita visibile a COM, che deriva da una classe di base non visibile a COM.  La chiamata `QueryInterface` determina l'attivazione dell'assistente al debug gestito solo nei casi in cui la chiamata richiede l'interfaccia di classe o l'interfaccia `IDispatch` predefinita della classe gestita visibile a COM.  L'assistente al debug gestito non viene attivato quando la chiamata `QueryInterface` è destinata a un'interfaccia esplicita alla quale è applicato l'attributo <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> ed è implementata esplicitamente dalla classe visibile a COM.  
  
## Sintomi  
 Viene effettuata una chiamata `QueryInterface` da codice nativo che restituisce l'errore COR\_E\_INVALIDOPERATION HRESULT.  L'errore HRESULT potrebbe essere causato dal fatto che Common Language Runtime non consente chiamate `QueryInterface` che comporterebbero l'attivazione di questo assistente al debug gestito.  
  
## Causa  
 Per evitare potenziali problemi di controllo delle versioni, il runtime non consente chiamate `QueryInterface` per l'interfaccia di classe o l'interfaccia `IDispatch` predefinita di una classe visibile a COM, che deriva da una classe non visibile a COM.  Ad esempio, se sono stati aggiunti membri pubblici alla classe di base non visibile a COM, i client COM esistenti che usano la classe derivata potrebbero interrompersi, perché la vtable della classe derivata, che contiene i membri della classe di base, verrebbe alterata da una tale modifica.  Le interfacce esplicite esposte a COM non presentano questo problema, perché non includono i membri di base delle interfacce nella vtable.  
  
## Risoluzione  
 Non esporre l'interfaccia della classe.  Definire un'interfaccia esplicita e applicarvi l'attributo <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 Di seguito è riportato un messaggio di esempio relativo a una chiamata `QueryInterface` su una classe `Derived` visibile a COM che deriva da una classe `Base` non visibile a COM.  
  
```  
A QueryInterface call was made requesting the class interface of COM   
visible managed class 'Derived'. However since this class derives from   
non COM visible class 'Base', the QueryInterface call will fail. This   
is done to prevent the non COM visible base class from being   
constrained by the COM versioning rules.   
```  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <nonComVisibleBaseClass />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)