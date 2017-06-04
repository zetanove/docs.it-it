---
title: "Abilitazione della traccia di rete | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "destinazioni di traccia"
  - "invio di tracce al file di log"
  - "listener di traccia, traccia di rete"
  - "traccia di rete, abilitazione"
  - "Debugger CLR"
  - "listener predefiniti"
  - "log, traccia"
  - "destinazione per l'output di traccia"
ms.assetid: 5fff458c-51a6-4134-ba47-8a6137ddc41e
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Abilitazione della traccia di rete
La tracciatura della rete fornisce l'accesso alle informazioni sulle chiamate al metodo e il traffico di rete generato da un'applicazione gestita.  È necessario eseguire le attività seguenti per abilitare la tracciatura della rete nell'applicazione:  
  
-   Compilare il codice con abilitata la tracciatura.  Vedere [How to: Compile Conditionally with Trace and Debug](../../../docs/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md) per ulteriori informazioni sulle opzioni del compilatore necessarie per abilitare la tracciatura.  
  
-   Specificare una destinazione di output.  
  
-   Configurare il comportamento di tracciatura della rete.  Vedere [Procedura: Configurare la tracciatura della rete](../../../docs/framework/network-programming/how-to-configure-network-tracing.md) per informazioni dettagliate.  
  
 La maggior parte delle destinazioni comuni di traccia, definite anche listener di traccia, è il listener predefinito e il file di log.  
  
 La traccia viene utilizzato il listener predefinito se non si specifica un listener di traccia.  È possibile visualizzare i messaggi inviati al listener predefinito esegue il codice in un debugger di codice gestito attivato come il debugger CLR fornito con .NET Framework SDK, o DBwin32.exe fornito con Windows SDK.  Utilizzando il debugger CLR, i messaggi di traccia vengono visualizzate nella finestra **Output**.  
  
 Se si preferisce utilizzare un file per ricevere le analisi, è possibile specificare un file di log utilizzando le impostazioni di configurazione, come illustrato nell'esempio seguente.  \(Per una descrizione generale dei file di configurazione, vedere [file di configurazione](../../../docs/framework/configure-apps/index.md)\).  
  
 Per l'invio di traccia in un file di log, aggiungere il seguente il nodo `<system.diagnostics>` del file di configurazione appropriato \(applicazione o computer\).  È possibile modificare il nome del file \(trace.log\) per esigenze.  
  
```  
<system.diagnostics>  
  <trace autoflush="true" indentsize="4">  
    <listeners>  
      <add name="file" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log"/>  
    </listeners>   
  </trace>  
</system.diagnostics>  
```  
  
## Vedere anche  
 [Interpretazione della traccia di rete](../../../docs/framework/network-programming/interpreting-network-tracing.md)   
 [Tracciatura di rete in .NET Framework](../../../docs/framework/network-programming/network-tracing.md)   
 [Introduction to Instrumentation and Tracing](http://msdn.microsoft.com/it-it/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)