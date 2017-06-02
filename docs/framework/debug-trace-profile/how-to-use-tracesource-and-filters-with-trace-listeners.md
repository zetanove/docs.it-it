---
title: "How to: Use TraceSource and Filters with Trace Listeners | Microsoft Docs"
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
  - "configuration files [.NET Framework], trace listeners"
  - "app.config files, trace listeners"
  - "levels of writing trace messages"
  - "trace listeners, TraceSource class"
  - "application configuration files, trace listeners"
  - "filters, trace listeners"
  - "TraceSource class, trace listeners"
  - "trace listeners, creating"
  - "trace listeners, filters"
  - "trace listeners, initializing"
ms.assetid: 21dc2169-947d-453a-b0e2-3dac3ba0cc9f
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Use TraceSource and Filters with Trace Listeners
In .NET Framework versione 2.0 è stato introdotto un sistema di tracciatura avanzato.  Il principio di base è rimasto invariato: i messaggi di traccia vengono inviati tramite oggetti di commutazione ai listener, i quali trasmettono i dati a un supporto di output associato.  Una delle principali differenze della versione 2.0 consiste nel fatto che le traccia possono essere avviate mediante istanze della classe <xref:System.Diagnostics.TraceSource>.  <xref:System.Diagnostics.TraceSource> funziona come un sistema di tracciatura avanzato e può essere utilizzata al posto dei metodi statici delle classi di traccia <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> delle versioni precedenti.  Sebbene le classi <xref:System.Diagnostics.Trace> e <xref:System.Diagnostics.Debug> siano ancora disponibili, per la tracciatura si consiglia di utilizzare la classe <xref:System.Diagnostics.TraceSource>.  
  
 In questa sezione viene descritto come utilizzare una classe <xref:System.Diagnostics.TraceSource> insieme a un file di configurazione dell'applicazione.  Sebbene non sia consigliato, è possibile eseguire la traccia utilizzando una classe <xref:System.Diagnostics.TraceSource> senza un file di configurazione.  Per informazioni su come eseguire la tracciatura senza utilizzare un file di configurazione, vedere [Procedura: creare e inizializzare origini di traccia](../../../docs/framework/debug-trace-profile/how-to-create-and-initialize-trace-sources.md).  
  
### Per creare e inizializzare l'origine di traccia  
  
1.  Il primo passo per la strumentazione di un'applicazione con il sistema di tracciatura consiste nel creare un'origine di traccia.  Nei progetti di grandi dimensioni in cui sono presenti diversi componenti è possibile creare un'origine di traccia distinta per ciascun componente.  Si consiglia di assegnare all'origine di traccia il nome dell'applicazione.  In questo modo sarà più semplice mantenere separate le diverse traccia.  Nel codice riportato di seguito viene creata una nuova origine di traccia \(`mySource)` e viene chiamato un metodo \(`Activity1`\) che analizza gli eventi.  I messaggi di traccia vengono scritti dal listener di traccia predefinito.  
  
    ```  
    using System;  
    using System.Diagnostics;  
    using System.Threading;  
  
    namespace TraceSourceApp  
    {  
        class Program  
        {  
            private static TraceSource mySource =   
                new TraceSource("TraceSourceApp");  
            static void Main(string[] args)  
            {  
                Activity1();  
                mySource.Close();  
                return;  
            }  
            static void Activity1()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 1,   
                    "Error message.");  
                mySource.TraceEvent(TraceEventType.Warning, 2,   
                    "Warning message.");  
            }  
        }  
    }  
    ```  
  
### Per creare e inizializzare i listener di traccia e i filtri  
  
1.  Il codice riportato nella prima procedura non consente di identificare a livello di codice eventuali listener di traccia o filtri.  Nei messaggi di traccia scritti nel listener di traccia predefinito è riportato soltanto il codice.  Per configurare listener di traccia specifici e i relativi filtri associati, modificare il file di configurazione corrispondente al nome dell'applicazione.  In questo file è possibile aggiungere o rimuovere un listener, impostare le proprietà e un filtro per un listener oppure rimuovere i listener.  Nell'esempio di file di configurazione riportato di seguito viene illustrato come inizializzare un listener di traccia console e un listener di traccia writer di testo per l'origine di traccia creata nella procedura precedente.  Oltre alla configurazione dei listener di traccia, il file di configurazione crea filtri per entrambi i listener nonché un oggetto sourceSwitch per l'origine di traccia.  Per l'aggiunta dei listener di analisi sono illustrate due tecniche: aggiunta del listener direttamente nell'origine di analisi e aggiunta di un listener alla raccolta dei listener condivisi e quindi aggiunta di quest'ultimo in base al nome all'origine di analisi.  I filtri identificati per i due listener vengono inizializzati con livelli di origine differenti.  Di conseguenza, alcuni messaggi vengono scritti da uno solo dei due listener.  
  
    ```  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="TraceSourceApp"   
            switchName="sourceSwitch"   
            switchType="System.Diagnostics.SourceSwitch">  
            <listeners>  
              <add name="console"   
                type="System.Diagnostics.ConsoleTraceListener">  
                <filter type="System.Diagnostics.EventTypeFilter"   
                  initializeData="Warning"/>  
              </add>  
              <add name="myListener"/>  
              <remove name="Default"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="sourceSwitch" value="Warning"/>  
        </switches>  
        <sharedListeners>  
          <add name="myListener"   
            type="System.Diagnostics.TextWriterTraceListener"   
            initializeData="myListener.log">  
            <filter type="System.Diagnostics.EventTypeFilter"   
              initializeData="Error"/>  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
### Per modificare il livello in cui un listener scrive un messaggio di traccia  
  
1.  Il file di configurazione inizializza le impostazioni dell'origine di traccia nel momento in cui l'applicazione viene inizializzata.  Per modificare queste impostazioni è necessario modificare il file di configurazione e riavviare l'applicazione oppure aggiornare l'applicazione a livello di codice utilizzando il metodo <xref:System.Diagnostics.Trace.Refresh%2A?displayProperty=fullName>.  L'applicazione può modificare dinamicamente le proprietà impostate dal file di configurazione per eseguire l'override delle eventuali impostazioni specificate dall'utente.  È possibile, ad esempio, assicurare che i messaggi critici vengano sempre inviati a un file di testo, indipendentemente dalle impostazioni di configurazione correnti.  
  
    ```  
    using System;  
    using System.Diagnostics;  
    using System.Threading;  
  
    namespace TraceSourceApp  
    {  
        class Program  
        {  
            private static TraceSource mySource =   
                new TraceSource("TraceSourceApp");  
            static void Main(string[] args)  
            {  
                Activity1();  
  
                // Change the event type for which tracing occurs.  
                // The console trace listener must be specified   
                // in the configuration file. First, save the original  
                // settings from the configuration file.  
                EventTypeFilter configFilter =   
                    (EventTypeFilter)mySource.Listeners["console"].Filter;  
  
                // Then create a new event type filter that ensures   
                // critical messages will be written.  
                mySource.Listeners["console"].Filter =  
                    new EventTypeFilter(SourceLevels.Critical);  
                Activity2();  
  
                // Allow the trace source to send messages to listeners   
                // for all event types. This statement will override   
                // any settings in the configuration file.  
                mySource.Switch.Level = SourceLevels.All;  
  
                // Restore the original filter settings.  
                mySource.Listeners["console"].Filter = configFilter;  
                Activity3();  
                mySource.Close();  
                return;  
            }  
            static void Activity1()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 1,   
                    "Error message.");  
                mySource.TraceEvent(TraceEventType.Warning, 2,   
                    "Warning message.");  
            }  
            static void Activity2()  
            {  
                mySource.TraceEvent(TraceEventType.Critical, 3,   
                    "Critical message.");  
                mySource.TraceInformation("Informational message.");  
            }  
            static void Activity3()  
            {  
                mySource.TraceEvent(TraceEventType.Error, 4,   
                    "Error message.");  
                mySource.TraceInformation("Informational message.");  
            }  
        }  
    }  
    ```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.TextWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics.EventTypeFilter>   
 [Procedura: creare e inizializzare origini di traccia](../../../docs/framework/debug-trace-profile/how-to-create-and-initialize-trace-sources.md)   
 [Trace Listeners](../../../docs/framework/debug-trace-profile/trace-listeners.md)