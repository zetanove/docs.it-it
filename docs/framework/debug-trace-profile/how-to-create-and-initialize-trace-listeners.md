---
title: "How to: Create and Initialize Trace Listeners | Microsoft Docs"
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
  - "initializing trace listeners"
  - "trace listeners, creating"
  - "trace listeners, initializing"
  - "tracing [.NET Framework], trace listeners"
  - "logs, trace listeners"
ms.assetid: 21726de1-61ee-4fdc-9dd0-3be49324d066
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Create and Initialize Trace Listeners
Le classi <xref:System.Diagnostics.Debug?displayProperty=fullName> e <xref:System.Diagnostics.Trace?displayProperty=fullName> inviano messaggi a oggetti detti listener, che li ricevono e li elaborano.  Uno di questi listener, <xref:System.Diagnostics.DefaultTraceListener?displayProperty=fullName>, viene creato e inizializzato automaticamente quando si abilita la traccia o il debug.  Se si vuole indirizzare l'output di <xref:System.Diagnostics.Trace> o <xref:System.Diagnostics.Debug> a origini aggiuntive, è necessario creare e inizializzare listener di traccia aggiuntivi.  
  
 I listener devono essere creati in base alle esigenze dell'applicazione.  Se, ad esempio, si desidera un record di testo di tutti gli output di traccia, creare un listener <xref:System.Diagnostics.TextWriterTraceListener>, che, quando è abilitato, scrive tutto l'output in un nuovo file di testo.  Se invece si vuole visualizzare l'output solo durante l'esecuzione dell'applicazione, creare un listener <xref:System.Diagnostics.ConsoleTraceListener>, che indirizza tutto l'output a una finestra della console.  Il listener <xref:System.Diagnostics.EventLogTraceListener> è in grado di indirizzare l'output di traccia a un registro eventi.  Per altre informazioni, vedere [Listener di traccia](../../../docs/framework/debug-trace-profile/trace-listeners.md).  
  
 È possibile creare listener di traccia in un [file di configurazione dell'applicazione](../../../docs/framework/configure-apps/index.md) o nel codice.  È consigliabile usare file di configurazione dell'applicazione, in quanto consentono di aggiungere, modificare o rimuovere listener di traccia senza dover modificare il codice.  
  
### Per creare e usare un listener di traccia tramite un file di configurazione  
  
1.  Dichiarare il listener di traccia nel file di configurazione dell'applicazione.  Se il listener che si sta creando richiede altri oggetti, dichiarare anche tali oggetti.  L'esempio seguente mostra come creare un listener denominato `myListener` che scrive nel file di testo `TextWriterOutput.log`.  
  
    ```  
    <configuration>  
      <system.diagnostics>  
        <trace autoflush="false" indentsize="4">  
          <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />  
            <remove name="Default" />  
          </listeners>  
        </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
2.  Usare la classe <xref:System.Diagnostics.Trace> nel codice per scrivere un messaggio nei listener di traccia.  
  
    ```vb  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
### Per creare e usare un listener di traccia nel codice  
  
-   Aggiungere il listener di traccia alla raccolta <xref:System.Diagnostics.Trace.Listeners%2A> e inviare le informazioni di traccia ai listener.  
  
    ```vb  
    Trace.Listeners.Add(New TextWriterTraceListener("TextWriterOutput.log", "myListener"))  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.Listeners.Add(new TextWriterTraceListener("TextWriterOutput.log", "myListener"));  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
     \-oppure\-  
  
-   Se non si vuole che il listener riceva l'output di traccia, non aggiungerlo alla raccolta <xref:System.Diagnostics.Trace.Listeners%2A>.  È possibile trasmettere l'output tramite un listener indipendentemente dalla raccolta <xref:System.Diagnostics.Trace.Listeners%2A> chiamando i metodi di output del listener stesso.  L'esempio seguente mostra come scrivere una riga in un listener non incluso nella raccolta <xref:System.Diagnostics.Trace.Listeners%2A>.  
  
    ```vb  
    Dim myListener As New TextWriterTraceListener("TextWriterOutput.log", "myListener")  
    myListener.WriteLine("Test message.")  
    ' You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush()  
    ```  
  
    ```csharp  
    TextWriterTraceListener myListener = new TextWriterTraceListener("TextWriterOutput.log", "myListener");  
    myListener.WriteLine("Test message.");  
    // You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush();  
    ```  
  
## Vedere anche  
 [Trace Listeners](../../../docs/framework/debug-trace-profile/trace-listeners.md)   
 [Trace Switches](../../../docs/framework/debug-trace-profile/trace-switches.md)   
 [How to: Add Trace Statements to Application Code](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)