---
title: "Debugging, Tracing, and Profiling | Microsoft Docs"
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
  - "debugging [.NET Framework]"
  - ".NET Framework application configuration, debugging"
  - "debugging [.NET Framework], .NET Framework application debugging"
  - "troubleshooting applications [.NET Framework], profiling"
  - "application development [.NET Framework], debugging"
  - ".NET Framework application configuration, profiling"
  - "profiling applications"
  - "troubleshooting applications [.NET Framework], debugging"
  - "troubleshooting applications [.NET Framework]"
  - "application development [.NET Framework], profiling"
ms.assetid: 4a04863e-2475-46f4-bc3f-3c11510c2a4b
caps.latest.revision: 28
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 28
---
# Debugging, Tracing, and Profiling
Per eseguire il debug di un'applicazione .NET Framework, l'ambiente del compilatore e di runtime deve essere configurato per consentire a un debugger di connettersi all'applicazione e di produrre simboli e mappe di linee, se possibile, per l'applicazione e il corrispondente Microsoft Intermediate Language \(MSIL\).  Dopo il debug di un'applicazione gestita, è possibile eseguire la profilatura per migliorare le prestazioni.  La profilatura valuta e descrive le righe del codice sorgente che generano il codice eseguito con maggiore frequenza e il tempo richiesto per eseguirle.  
  
 Il debug delle applicazioni .NET framework viene eseguito facilmente tramite Visual Studio, che gestisce molti dettagli della configurazione.  Se Visual Studio non è installato, è possibile esaminare e migliorare le prestazioni delle applicazioni .NET Framework usando le classi di debug nello spazio dei nomi <xref:System.Diagnostics> di .NET Framework.  Questo spazio dei nomi include le classi <xref:System.Diagnostics.Trace>, <xref:System.Diagnostics.Debug> e <xref:System.Diagnostics.TraceSource> per la traccia del flusso di esecuzione e le classi <xref:System.Diagnostics.Process>, <xref:System.Diagnostics.EventLog> e <xref:System.Diagnostics.PerformanceCounter> per il codice di profilatura.  
  
## In questa sezione  
 [Enabling JIT\-Attach Debugging](../../../docs/framework/debug-trace-profile/enabling-jit-attach-debugging.md)  
 Mostra come configurare il Registro di sistema per eseguire l'associazione JIT di un motore di debug in un'applicazione .NET Framework.  
  
 [Semplificazione del debug di un'immagine](../../../docs/framework/debug-trace-profile/making-an-image-easier-to-debug.md)  
 Mostra come attivare il rilevamento JIT e disattivare l'ottimizzazione per rendere più semplice l'esecuzione del debug di un assembly.  
  
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)  
 Descrive come monitorare l'esecuzione dell'applicazione mentre è in esecuzione e come instrumentarla per visualizzare lo stato o gli errori durante l'esecuzione.  
  
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)  
 Descrive gli assistenti al debug gestito, strumenti di supporto al debug che funzionano in combinazione con Common Language Runtime \(CLR\) per fornire informazioni sullo stato di runtime.  
  
 [Enhancing Debugging with the Debugger Display Attributes](../../../docs/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes.md)  
 Descrive in che modo lo sviluppatore di un tipo può specificarne l'aspetto quando viene visualizzato in un debugger.  
  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)  
 Descrive i contatori che è possibile usare per registrare le prestazioni di un'applicazione.  
  
## Sezioni correlate  
 [Debug di applicazioni ASP.NET e AJAX](../Topic/Debugging%20ASP.NET%20and%20AJAX%20Applications.md)  
 Fornisce i prerequisiti e le istruzioni su come eseguire il debug di un'applicazione ASP.NET durante lo sviluppo o dopo la distribuzione.  
  
 [Guida di sviluppo](../../../docs/framework/development-guide.md)  
 Viene fornita una guida per tutte le aree e attività principali per lo sviluppo di applicazioni, quali la creazione, la configurazione, il debug, la sicurezza e la distribuzione dell'applicazione e informazioni su programmazione dinamica, interoperabilità, estendibilità, gestione della memoria e threading.