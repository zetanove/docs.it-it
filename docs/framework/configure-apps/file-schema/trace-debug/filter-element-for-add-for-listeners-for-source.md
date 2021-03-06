---
title: "Elemento &lt;filter&gt; per &lt;add&gt; per &lt;listeners&gt; per &lt;source&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#filter"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add/filter"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<filter> elemento per <add> per <listeners> per <source>"
  - "<filter> elemento per <add> per <listeners> per <source>"
  - "attributo initializeData"
ms.assetid: 15808b80-4579-4c25-b385-178cfdf154ba
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Elemento &lt;filter&gt; per &lt;add&gt; per &lt;listeners&gt; per &lt;source&gt;
Consente di aggiungere un filtro a un listener della raccolta `Listeners` per un'origine di traccia.  
  
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
|`sources`|Contiene le origini di analisi che danno inizio ai messaggi di tracciatura.|  
|`source`|Specifica un'origine di analisi che dà inizio ai messaggi di tracciatura.|  
|`listeners`|Contiene listener per la raccolta, l'archiviazione e l'invio di messaggi.  I listener indirizzano l'output di tracciatura a una destinazione adatta.|  
|`add`|Consente di aggiungere un listener alla raccolta `Listeners` per un'origine di traccia.|  
  
## Note  
 L'elemento `<filter>` deve essere incluso in un elemento `<add>` per un listener dell'origine di traccia che specifica il tipo del listener e non solo il nome di un listener definito in un [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md).  Se il listener viene definito in un [\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md), è necessario definire il filtro per il listener in tale elemento.  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<filter>` per aggiungere un filtro al listener `console` nella raccolta `Listeners` per l'origine di traccia `myTraceSource`, specificando `Error` come livello di evento per il filtro.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" switchName="SourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch"  >  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener" >  
            <filter type="System.Diagnostics.EventTypeFilter"   
              initializeData="Error" />  
          </add>  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="SourceSwitch" value="Warning" />  
    </switches>  
  </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.TraceListener.Filter%2A?displayProperty=fullName>   
 <xref:System.Diagnostics.TraceFilter>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)