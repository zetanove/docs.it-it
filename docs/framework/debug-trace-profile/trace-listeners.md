---
title: "Trace Listeners | Microsoft Docs"
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
  - "Listener object types"
  - "listeners"
  - "Trace class, listeners"
  - "trace listeners, about trace listeners"
  - "Listeners collection"
  - "trace listeners"
  - "tracing [.NET Framework], trace listeners"
  - "logs, trace listeners"
ms.assetid: 444b0d33-67ea-4c36-9e94-79c50f839025
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Trace Listeners
Quando si usa **Trace**, **Debug** e <xref:System.Diagnostics.TraceSource>, è necessario disporre di un meccanismo per la raccolta e la registrazione dei messaggi inviati.  I messaggi di traccia vengono ricevuti dai *listener*.  Il compito di un listener è raccogliere, archiviare e inviare messaggi di errore.  I listener indirizzano l'output di tracciatura a una destinazione appropriata, ad esempio un file di log, una finestra o un file di testo.  
  
 I listener sono disponibili per le classi **Debug**, **Trace** e <xref:System.Diagnostics.TraceSource>, ognuna delle quali può inviare il proprio output a un'ampia gamma di oggetti listener.  Di seguito sono riportati i listener predefiniti comunemente usati:  
  
-   <xref:System.Diagnostics.TextWriterTraceListener> reindirizza l'output a un'istanza della classe <xref:System.IO.TextWriter> o a qualsiasi oggetto che sia una classe <xref:System.IO.Stream>.  Può anche scrivere nella console o in un file, perché si tratta di classi <xref:System.IO.Stream>.  
  
-   <xref:System.Diagnostics.EventLogTraceListener> reindirizza l'output a un log eventi.  
  
-   <xref:System.Diagnostics.DefaultTraceListener> genera messaggi **Write** e **WriteLine** in **OutputDebugString** e nel metodo **Debugger.Log**.  In Visual Studio questo comportamento fa sì che i messaggi di debug vengano visualizzati nella finestra di output.  I messaggi **Assert** non riusciti e **Fail** vengono generati anche nell'API Windows **OutputDebugString** e nel metodo **Debugger.Log** e provocano anche la visualizzazione di una finestra di messaggio.  Questo comportamento è quello predefinito per i messaggi di **Debug** e **Trace**, perché **DefaultTraceListener** viene automaticamente incluso in ogni raccolta `Listeners` ed è l'unico listener incluso automaticamente.  
  
-   <xref:System.Diagnostics.ConsoleTraceListener> reindirizza l'output di traccia o di debug all'output standard o al flusso di errori standard.  
  
-   Tramite l'oggetto <xref:System.Diagnostics.DelimitedListTraceListener> l'output di traccia o di debug viene indirizzato a un writer di testo, ad esempio un writer di flusso oppure a un flusso, ad esempio un flusso di file. L'output di traccia è in un formato testo delimitato che usa il delimitatore specificato dalla proprietà <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A>.  
  
-   <xref:System.Diagnostics.XmlWriterTraceListener> reindirizza l'output di traccia o di debug come dati con codifica XML a un oggetto <xref:System.IO.TextWriter> o <xref:System.IO.Stream>, come <xref:System.IO.FileStream>.  
  
 Se si vuole che altri listener oltre a <xref:System.Diagnostics.DefaultTraceListener> ricevano l'output di **Debug**, **Trace** e <xref:System.Diagnostics.TraceSource>, è necessario aggiungerli alla raccolta `Listeners`.  Per altre informazioni, vedere [How to: Create and Initialize Trace Listeners](../../../docs/framework/debug-trace-profile/how-to-create-and-initialize-trace-listeners.md) e [How to: Use TraceSource and Filters with Trace Listeners](../../../docs/framework/debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners.md).  Tutti i listener inclusi nella raccolta **Listeners** ricevono gli stessi messaggi dai metodi di output di traccia.  Si supponga, ad esempio, di configurare due listener, **TextWriterTraceListener** e **EventLogTraceListener**.  Ogni listener riceve lo stesso messaggio.  **TextWriterTraceListener** reindirizzerà l'output a un flusso, mentre **EventLogTraceListener** reindirizzerà l'output a un log eventi.  
  
 L'esempio seguente mostra come inviare l'output alla raccolta **Listeners**.  
  
```vb  
' Use this example when debugging.  
Debug.WriteLine("Error in Widget 42")  
' Use this example when tracing.  
Trace.WriteLine("Error in Widget 42")  
```  
  
```csharp  
// Use this example when debugging.  
System.Diagnostics.Debug.WriteLine("Error in Widget 42");  
// Use this example when tracing.  
System.Diagnostics.Trace.WriteLine("Error in Widget 42");  
```  
  
 Poiché Debug e Trace condividono la stessa raccolta **Listeners**, se si aggiunge un oggetto listener a una raccolta **Debug.Listeners** nell'applicazione, l'oggetto viene aggiunto anche alla raccolta **Trace.Listeners**.  
  
 L'esempio seguente mostra come usare un listener per inviare informazioni di traccia a una console:  
  
```vb  
Trace.Listeners.Clear()  
Trace.Listeners.Add(New TextWriterTraceListener(Console.Out))  
```  
  
```csharp  
System.Diagnostics.Trace.Listeners.Clear();  
System.Diagnostics.Trace.Listeners.Add(  
   new System.Diagnostics.TextWriterTraceListener(Console.Out));  
```  
  
## Listener definiti dallo sviluppatore  
 È possibile definire listener personalizzati ereditando dalla classe base **TraceListener** ed eseguendo l'override dei metodi della classe con metodi personalizzati.  Per altre informazioni sulla creazione di listener definiti dallo sviluppatore, vedere <xref:System.Diagnostics.TraceListener> negli argomenti di riferimento su .NET Framework.  
  
## Vedere anche  
 <xref:System.Diagnostics.TextWriterTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.TraceListener>   
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)   
 [Trace Switches](../../../docs/framework/debug-trace-profile/trace-switches.md)