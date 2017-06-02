---
title: "Elemento &lt;filter&gt; per &lt;add&gt; per &lt;listeners&gt; per &lt;trace&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add/filter"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<filter> elemento per <add> per <listeners> per <trace>"
  - "<filter> elemento per <add> per <listeners> per <trace>"
  - "attributo initializeData"
ms.assetid: eb9c18f5-dfa8-47c5-b91b-e4b93e76e1cc
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Elemento &lt;filter&gt; per &lt;add&gt; per &lt;listeners&gt; per &lt;trace&gt;
Consente di aggiungere un filtro a un listener della raccolta `Listeners` per una traccia.  
  
## Sintassi  
  
```  
<filter   
  type="traceFilterClassName"   
  initializeData="data" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`type`|Attributo obbligatorio.<br /><br /> Specifica il tipo di filtro, che deve ereditare dalla classe <xref:System.Diagnostics.TraceFilter>.  È possibile utilizzare solo il nome completo dello spazio dei nomi del tipo, che corrisponde alla proprietà <xref:System.Type.FullName%2A> del tipo, oppure il nome completo del tipo incluse le informazioni sull'assembly, che corrisponde alla proprietà <xref:System.Type.AssemblyQualifiedName%2A>.  Per informazioni sui nomi completi dei tipi, vedere [Specifying Fully Qualified Type Names](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|`initializeData`|Attributo facoltativo.<br /><br /> Stringa passata al costruttore per la classe di filtro specificata.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`trace`|Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.|  
|`listeners`|Contiene listener per la raccolta, l'archiviazione e l'invio di messaggi.  I listener indirizzano l'output di tracciatura a una destinazione adatta.|  
|`add`|Consente di aggiungere un listener alla raccolta `Listeners`.|  
  
## Note  
 L'elemento `<filter>` deve essere incluso in un elemento `<add>` per un listener di traccia che specifica il tipo del listener e non solo il nome di un listener definito in un [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md).  Se il listener viene definito in un [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md), è necessario definire il filtro per il listener in tale elemento.  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<filter>`  per aggiungere un filtro al listener `console` nella raccolta `Listeners` per la traccia, specificando `Error` come livello di evento per il filtro.  
  
```  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <add name="console"   
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"   
            initializeData="Error" />  
        </add>  
        <remove name="Default" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.TraceListener.Filter%2A?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceFilter>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)