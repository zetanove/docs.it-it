---
title: "Elemento &lt;add&gt; per &lt;listeners&gt; per &lt;source&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento) per <listeners> per <source>"
  - "add (elemento) per <listeners> per <source>"
  - "attributo initializeData"
ms.assetid: 4ce36ac1-81ef-48e8-b8b2-b5a5b0e2adcb
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Elemento &lt;add&gt; per &lt;listeners&gt; per &lt;source&gt;
Consente di aggiungere un listener alla raccolta `Listeners` per un'origine di traccia.  
  
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
|`type`|Attributo obbligatorio.<br /><br /> Specifica il tipo del listener.  È necessario utilizzare una stringa che soddisfi i requisiti indicati in [Specifying Fully Qualified Type Names](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|`initializeData`|Attributo facoltativo.<br /><br /> Stringa passata al costruttore per la classe specificata.  Viene generata un'eccezione <xref:System.Configuration.ConfigurationException> se la classe non dispone di un costruttore che accetta una stringa.|  
|`name`|Attributo facoltativo.<br /><br /> Specifica il nome del listener.|  
|`traceOutputOptions`|Attributo facoltativo.<br /><br /> Specifica il valore della proprietà <xref:System.Diagnostics.TraceListener.TraceOutputOptions%2A> per il listener di traccia.|  
|\[attributi personalizzati\]|Attributi facoltativi.<br /><br /> Specifica il valore degli attributi specifici del listener identificati dal metodo <xref:System.Diagnostics.TraceListener.GetSupportedAttributes%2A> per tale listener.  <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A> rappresenta un esempio di attributo aggiuntivo univoco per la classe <xref:System.Diagnostics.DelimitedListTraceListener>.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|Consente di aggiungere un filtro a un listener della raccolta `Listeners` per un'origine di traccia.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`sources`|Contiene le origini di analisi che danno inizio ai messaggi di tracciatura.|  
|`source`|Specifica un'origine di analisi che dà inizio ai messaggi di tracciatura.|  
|`listeners`|Specifica i listener per la raccolta, l'archiviazione e l'invio di messaggi.|  
  
## Note  
 Le classi di listener fornite con .NET Framework derivano dalla classe <xref:System.Diagnostics.TraceListener>.  
  
 Se non viene specificato l'attributo `name` del listener di traccia, l'impostazione predefinita della proprietà <xref:System.Diagnostics.TraceListener.Name%2A> del listener di traccia sarà una stringa vuota \(""\).  Se l'applicazione dispone di un solo listener, è possibile aggiungerlo senza specificarne il nome e rimuoverlo specificando per il nome una stringa vuota.  Se invece l'applicazione dispone di più listener, è necessario specificare un nome univoco per ciascun listener di traccia, al fine di identificare e gestire singolarmente i listener di traccia nella raccolta <xref:System.Diagnostics.TraceSource.Listeners%2A?displayProperty=fullName>.  
  
> [!NOTE]
>  L'aggiunta di più listener di traccia dello stesso tipo e con lo stesso nome implica l'aggiunta di un solo listener di traccia di tale tipo e con tale nome alla raccolta `Listeners`.  È tuttavia possibile aggiungere a livello di codice più listener identici alla raccolta `Listeners`.  
  
 Il valore dell'attributo `initializeData` dipende dal tipo di listener creato.  Non per tutti i listener di traccia è necessario specificare l'attributo `initializeData`.  
  
> [!NOTE]
>  Quando si utilizza l'attributo `initializeData`, è possibile ottenere l'avviso del compilatore "Attributo 'initializeData' non dichiarato". Questo avviso viene generato perché le impostazioni di configurazione vengono convalidate in base alla classe di base astratta <xref:System.Diagnostics.TraceListener> che non riconosce l'attributo `initializeData`.  In genere, è possibile ignorare questo avviso per implementazioni del listener di traccia che presentano un costruttore che accetta un parametro.  
  
 Nella tabella riportata di seguito vengono elencati i listener di traccia inclusi in .NET Framework e viene fornita una descrizione del valore dei relativi attributi `initializeData`.  
  
|Classe di listener di traccia|Valore dell'attributo initializeData|  
|-----------------------------------|------------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName>|Valore `useErrorStream` del costruttore <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>.  Impostare l'attributo `initializeData` su `true` per scrivere l'output di traccia e di debug nel flusso di errori standard. Impostarlo invece su `false` per scrivere nel flusso di output standard.|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName>|Nome del file in cui scrive <xref:System.Diagnostics.DelimitedListTraceListener>.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>|Nome di un'origine del log eventi esistente.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.EventSchemaTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.TextWriterTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.XmlWriterTraceListener> esegue operazioni di scrittura.|  
  
## File di configurazione  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare elementi `<add>` per aggiungere i listener `console` e `textListener` alla raccolta `Listeners` per l'origine di traccia `TraceSourceApp`.  Il listener `textListener` scrive l'output di traccia nel file myListener.log.  
  
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