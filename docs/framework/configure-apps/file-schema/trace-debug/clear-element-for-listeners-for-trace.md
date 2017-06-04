---
title: "Elemento &lt;clear&gt; per &lt;listeners&gt; per &lt;trace&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<clear> (elemento) per <listeners> per <trace>"
  - "clear (elemento) per <listeners> per <trace>"
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;clear&gt; per &lt;listeners&gt; per &lt;trace&gt;
Cancella la raccolta `Listeners` per la traccia.  
  
## Sintassi  
  
```  
<clear/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`trace`|Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.|  
|`listeners`|Contiene listener per la raccolta, l'archiviazione e l'invio di messaggi.  I listener indirizzano l'output di tracciatura a una destinazione adatta.|  
  
## Note  
 L'elemento `<clear>` consente di rimuovere tutti i listener dalla raccolta `Listeners` per la traccia.  È possibile utilizzare l'elemento `<clear>` prima dell'elemento `<add>` per essere certi che nella raccolta non vi siano altri listener attivi.  
  
 È possibile cancellare la raccolta `Listeners` a livello di codice chiamando il metodo <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> sulla proprietà <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=fullName> \(`System.Diagnostics.Trace.Listeners.Clear()`\).  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
> [!NOTE]
>  L'elemento `<clear>` rimuove la classe <xref:System.Diagnostics.DefaultTraceListener> dalla raccolta `Listeners` modificando il comportamento dei metodi <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> e <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName>.  La chiamata di un metodo `Assert` o `Fail` comporta generalmente la visualizzazione di una finestra di messaggio.  La finestra di messaggio non viene tuttavia visualizzata se <xref:System.Diagnostics.DefaultTraceListener> non è incluso nella raccolta `Listeners`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<clear>` prima dell'elemento `<add>` per l'aggiunta del listener `console` alla raccolta `Listeners` per la traccia.  
  
```  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"   
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"   
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>   
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Trace.Listeners%2A>   
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.Debug>   
 <xref:System.Diagnostics.TraceSource>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [\<remove\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-trace.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)