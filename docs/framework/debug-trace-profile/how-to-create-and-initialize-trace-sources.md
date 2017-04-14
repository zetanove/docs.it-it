---
title: "Procedura: creare e inizializzare origini di traccia | Microsoft Docs"
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
  - "origini di traccia"
  - "inizializzazione delle origini di traccia"
  - "file di configurazione [.NET Framework], origini di traccia"
ms.assetid: f88dda6f-5fda-45be-9b3c-745a9b708c4d
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: creare e inizializzare origini di traccia
La classe <xref:System.Diagnostics.TraceSource> viene utilizzata dalle applicazioni per produrre tracce associabili all'applicazione.  <xref:System.Diagnostics.TraceSource> fornisce metodi di traccia che consentono di tracciare con facilità eventi e dati e di generare tracce informative.  L'output di traccia da <xref:System.Diagnostics.TraceSource> può essere creato e inizializzato con o senza l'utilizzo di file di configurazione.  In questo argomento vengono fornite istruzioni per entrambe le opzioni.  È tuttavia consigliabile utilizzare file di configurazione per semplificare la riconfigurazione delle tracce prodotte dalle origini di traccia in fase di esecuzione.  
  
### Per creare e inizializzare un'origine di traccia utilizzando un file di configurazione  
  
1.  Creare un progetto di applicazione console di Visual Studio e sostituire il codice fornito con il codice seguente.  Il codice registra errori e avvisi e ne restituisce alcuni sulla console e alcuni nel file myListener creato dalle voci del file di configurazione.  
  
     [!code-csharp[TraceSourceExample1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tracesourceexample1/cs/program.cs#1)]
     [!code-vb[TraceSourceExample1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tracesourceexample1/vb/program.vb#1)]  
  
2.  Aggiungere un file di configurazione dell'applicazione al progetto per inizializzare l'origine della traccia denominata `TraceSourceApp` nell'esempio di codice riportato nel passaggio 1.  
  
3.  Sostituire il contenuto del file di configurazione predefinito con le impostazioni seguenti per inizializzare un listener di traccia della console e un listener di traccia del writer di testo per l'origine di traccia creata nel passaggio 1.  
  
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
                  initializeData="Error"/>  
              </add>  
              <add name="myListener"/>  
              <remove name="Default"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="sourceSwitch" value="Error"/>  
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
  
     Oltre alla configurazione dei listener di traccia, il file di configurazione crea filtri per entrambi i listener nonché un'opzione di origine per l'origine di traccia.  Per l'aggiunta dei listener di analisi sono illustrate due tecniche: aggiunta del listener direttamente nell'origine di analisi e aggiunta di un listener alla raccolta dei listener condivisi e quindi aggiunta di quest'ultimo in base al nome all'origine di analisi.  I filtri identificati per i due listener vengono inizializzati con livelli di origine differenti.  Di conseguenza, alcuni messaggi vengono scritti da uno solo dei due listener.  
  
     Il file di configurazione inizializza le impostazioni dell'origine di traccia nel momento in cui l'applicazione viene inizializzata.  L'applicazione può modificare dinamicamente le proprietà impostate dal file di configurazione per eseguire l'override delle eventuali impostazioni specificate dall'utente.  È possibile, ad esempio, assicurare che i messaggi critici vengano sempre inviati a un file di testo, indipendentemente dalle impostazioni di configurazione correnti.  Nell'esempio di codice viene illustrato come eseguire l'override delle impostazioni del file di configurazione per garantire l'invio dei messaggi critici ai listener di traccia.  
  
     Le eventuali modifiche apportate alle impostazioni del file di configurazione durante l'esecuzione dell'applicazione non vengono applicate immediatamente.  Per modificare le impostazioni, è necessario riavviare l'applicazione o aggiornare l'applicazione a livello di codice utilizzando il metodo <xref:System.Diagnostics.Trace.Refresh%2A?displayProperty=fullName>.  
  
### Per inizializzare le origini di analisi, i listener e i filtri senza un file di configurazione  
  
-   Utilizzare l'esempio di codice seguente per abilitare la traccia in un'origine di traccia senza utilizzare un file di configurazione.  Si consiglia, tuttavia, di utilizzare questa tecnica soltanto quando si desidera eseguire la traccia senza dipendere dai file di configurazione.  
  
     [!code-csharp[TraceSourceExample2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tracesourceexample2/cs/program.cs#1)]
     [!code-vb[TraceSourceExample2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tracesourceexample2/vb/program.vb#1)]  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.TextWriterTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics.EventTypeFilter>   
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)