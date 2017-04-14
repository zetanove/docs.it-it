---
title: "Elemento &lt;clear&gt; per &lt;listeners&gt; per &lt;source&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/clear"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<clear> (elemento) per <listeners> per <source>"
  - "clear (elemento) per <listeners> per <source>"
ms.assetid: 76796bb2-9c0b-4526-8135-8bf18b16d8d9
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Elemento &lt;clear&gt; per &lt;listeners&gt; per &lt;source&gt;
Cancella la raccolta `Listeners` per un'origine di traccia.  
  
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
|`sources`|Contiene le origini di analisi che danno inizio ai messaggi di tracciatura.|  
|`source`|Specifica un'origine di analisi che dà inizio ai messaggi di tracciatura.|  
|`listeners`|Specifica i listener per la raccolta, l'archiviazione e l'invio di messaggi.|  
  
## Note  
 L'elemento `<clear>` consente di rimuovere tutti i listener dalla raccolta `Listeners` per un'origine di traccia, incluso <xref:System.Diagnostics.DefaultTraceListener>.  È possibile utilizzare l'elemento `<clear>` prima dell'elemento `<add>` per essere certi che nella raccolta non vi siano altri listener attivi.  
  
## File di configurazione  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<clear>` prima degli elementi `<add>` per l'aggiunta dei listener `console` e `textListener` alla raccolta `Listeners` per l'origine di traccia `TraceSourceApp`.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
       <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <clear/>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.TraceListener>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)