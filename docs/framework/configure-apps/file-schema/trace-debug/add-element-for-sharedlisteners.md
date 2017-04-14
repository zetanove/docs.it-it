---
title: "Elemento &lt;add&gt; per &lt;sharedListeners&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento) per <sharedListeners>"
  - "add (elemento) per <sharedListeners>"
  - "attributo initializeData"
ms.assetid: 1595e1bc-2492-421f-8384-7f382eb8eb57
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;add&gt; per &lt;sharedListeners&gt;
Consente di aggiungere un listener alla raccolta `sharedListeners`.  `sharedListeners` è una raccolta di listener cui può fare riferimento qualsiasi elemento [\<source\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/source-element.md) o [\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md).  Per impostazione predefinita, i listener della raccolta `sharedListeners` non vengono inseriti in una raccolta `Listeners`,  ma devono essere aggiunti per nome all'[\<source\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/source-element.md) o all'[\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md).  Non è possibile ottenere i listener nella raccolta `sharedListeners` nel codice in fase di esecuzione.  
  
## Sintassi  
  
```  
<add name="name"   
  type="TraceListenerClassName, Version, Culture, PublicKeyToken"  
  initializeData="data"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo obbligatorio.<br /><br /> Specifica il nome del listener utilizzato per aggiungere il listener condiviso a una raccolta `Listeners`.|  
|`type`|Attributo obbligatorio.<br /><br /> Specifica il tipo del listener.  È necessario utilizzare una stringa che soddisfi i requisiti indicati in [Specifying Fully Qualified Type Names](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|`initializeData`|Attributo facoltativo.<br /><br /> Stringa passata al costruttore per la classe specificata.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-sharedlisteners.md)|Consente di aggiungere un filtro a un listener della raccolta `sharedListeners`.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`sharedListeners`|Raccolta di listener cui può fare riferimento qualsiasi elemento di origine o di traccia.|  
  
## Note  
 Le classi di listener fornite con .NET Framework derivano dalla classe <xref:System.Diagnostics.TraceListener>.  Il valore dell'attributo `name` viene utilizzato per aggiungere il listener condiviso a una raccolta `Listeners` per una traccia o un'origine di traccia.  Il valore dell'attributo `initializeData` dipende dal tipo di listener creato.  Non per tutti i listener di traccia è necessario specificare l'attributo `initializeData`.  
  
> [!NOTE]
>  Quando si utilizza l'attributo `initializeData`, è possibile ottenere l'avviso del compilatore "Attributo 'initializeData' non dichiarato". Questo avviso viene generato perché le impostazioni di configurazione vengono convalidate in base alla classe di base astratta <xref:System.Diagnostics.TraceListener> che non riconosce l'attributo `initializeData`.  In genere, è possibile ignorare questo avviso per implementazioni del listener di traccia che presentano un costruttore che accetta un parametro.  
  
 Nella tabella riportata di seguito vengono elencati i listener di traccia inclusi in .NET Framework e viene fornita una descrizione del valore dei relativi attributi `initializeData`.  
  
|Classe di listener di traccia|Valore dell'attributo initializeData|  
|-----------------------------------|------------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener>|Valore `useErrorStream` del costruttore <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>.  Impostare l'attributo `initializeData` su `true` per scrivere l'output di traccia e di debug nel flusso di errori standard. Impostarlo invece su `false` per scrivere nel flusso di output standard.|  
|<xref:System.Diagnostics.DelimitedListTraceListener>|Nome del file in cui scrive <xref:System.Diagnostics.DelimitedListTraceListener>.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>|Nome di un'origine del log eventi esistente.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.EventSchemaTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.TextWriterTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.XmlWriterTraceListener>|Nome del file in cui <xref:System.Diagnostics.XmlWriterTraceListener> esegue operazioni di scrittura.|  
  
## File di configurazione  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare gli elementi di `<add>` per aggiungere <xref:System.Diagnostics.TextWriterTraceListener> `textListener` alla raccolta di `sharedListeners`.   `textListener` viene aggiunto per nome alla raccolta di `Listeners` per l'origine di traccia `TraceSourceApp`.  Il listener `textListener` scrive l'output di traccia nel file myListener.log.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
          <remove name="Default"/>  
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