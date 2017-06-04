---
title: "marshaling MDA | Microsoft Docs"
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
  - "marshaling, run-time errors"
  - "marshaling MDA"
  - "managed debugging assistants (MDAs), marshaling"
  - "MDAs (managed debugging assistants), marshaling"
ms.assetid: 5433b1f8-b0e5-40c9-a49a-0e5bd213363d
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# marshaling MDA
L'assistente al debug gestito `marshaling` viene attivato quando CLR configura le informazioni di marshalling per un parametro di un metodo o un campo di una struttura.  Questo assistente al debug gestito non funziona per gli assembly con compilazione JIT.  
  
## Effetto sull'ambiente di esecuzione  
 L'assistente al debug gestito non ha alcun effetto su CLR.  
  
## Output  
 L'assistente al debug gestito visualizza il tipo del parametro o del campo nei contesti gestiti e non gestiti e la struttura o il metodo contenente il tipo.  Di seguito viene riportato un esempio di output per un campo.  
  
```  
Marshaling from 'Char' to 'ANSI char'  
name="assembly!Namespace.Class::myChar  
```  
  
## Configurazione  
 La configurazione dell'assistente al debug gestito consente di filtrare le informazioni di marshalling restituite in base ai nomi dei campi o dei metodi coinvolti.  Il seguente esempio mostra l'uso degli elementi `methodFilter`, `fieldFilter`e `match` per specificare i filtri.  Impostando l'attributo `name` su un asterisco \(\*\), tutti gli elementi corrisponderanno.  
  
```  
<mdaConfig>  
  <assistants>  
    <marshaling>  
      <methodFilter>  
        <match name="Method1"/>  
        <match name="Method2"/>  
      </methodFilter>  
      <fieldFilter>  
        <match name="Field1"/>  
        <match name="Field2"/>  
       </fieldFilter>  
    </marshaling>  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md)