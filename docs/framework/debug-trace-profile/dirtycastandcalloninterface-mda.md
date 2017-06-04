---
title: "dirtyCastAndCallOnInterface MDA | Microsoft Docs"
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
  - "managed debugging assistants (MDAs), early bound calls AutoDispatch"
  - "dispatch-only mode"
  - "dirtyCastAndCallOnInterface"
  - "early-bound managed classes"
  - "early bound calls on AutoDispatch"
  - "MDAs (managed debugging assistants), early bound calls AutoDispatch"
  - "EarlyBoundCallOnAutorDispatchClassInteface MDA"
ms.assetid: aa388ed3-7e3d-48ea-a0b5-c47ae19cec38
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# dirtyCastAndCallOnInterface MDA
L'assistente al debug gestito `dirtyCastAndCallOnInterface` viene attivato quando viene tentata una chiamata ad associazione anticipata attraverso un vtable su un'interfaccia di classe contrassegnata solo per l'associazione tardiva.  
  
## Sintomi  
 Un'applicazione genera una violazione di accesso o ha un comportamento imprevisto quando si inserisce in CLR una chiamata ad associazione anticipata tramite COM.  
  
## Causa  
 Il codice sta tentando una chiamata ad associazione anticipata attraverso un vtable tramite un'interfaccia di classe solo ad associazione tardiva.  Si noti che, per impostazione predefinita, le interfacce di classe vengono identificate solo come ad associazione tardiva.  Possono essere identificate come ad associazione tardiva anche con l'attributo <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> con un valore <xref:System.Runtime.InteropServices.ClassInterfaceType> \(`[ClassInterface(ClassInterfaceType.AutoDispatch)]`\).  
  
## Risoluzione  
 La soluzione consigliata prevede di definire un'interfaccia esplicita da usare con COM e di fare in modo che i client COM chiamino tramite questa interfaccia invece che tramite l'interfaccia di classe generata automaticamente.  In alternativa, è possibile trasformare la chiamata da COM in una chiamata ad associazione tardiva mediante `IDispatch`.  
  
 Infine, è possibile identificare la classe come <xref:System.Runtime.InteropServices.ClassInterfaceType> \(`[ClassInterface(ClassInterfaceType.AutoDual)]`\) per consentire alle chiamate ad associazione anticipata di essere inserite da COM. Tuttavia, l'uso di <xref:System.Runtime.InteropServices.ClassInterfaceType> è fortemente sconsigliato a causa delle limitazioni nel controllo delle versioni descritte in <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  Segnala solo i dati sulle chiamate ad associazione anticipata sulle interfacce ad associazione tardiva.  
  
## Output  
 Nome del metodo o nome del campo a cui si accede con associazione anticipata.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <dirtyCastAndCallOnInterface />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)