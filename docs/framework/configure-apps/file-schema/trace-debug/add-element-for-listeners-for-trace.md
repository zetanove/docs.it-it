---
title: "Elemento &lt;add&gt; per &lt;listeners&gt; per &lt;trace&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento) per <listeners>"
  - "add (elemento) per <listeners>"
  - "attributo initializeData"
ms.assetid: 81e804a3-ef11-4d39-bbde-bfa012c179e2
caps.latest.revision: 24
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 22
---
# Elemento &lt;add&gt; per &lt;listeners&gt; per &lt;trace&gt;
Consente di aggiungere un listener alla raccolta **Listeners**.  
  
## Sintassi  
  
```  
<add name="name"   
     type="trace listener class name, Version, Culture, PublicKeyToken"  
     initializeData="data"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|**type**|Attributo obbligatorio.<br /><br /> Specifica il tipo del listener.  È necessario utilizzare una stringa che soddisfi i requisiti indicati in [Specifica di nomi di tipi completi](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|**initializeData**|Attributo facoltativo.<br /><br /> Stringa passata al costruttore per la classe specificata.|  
|**name**|Attributo facoltativo.<br /><br /> Specifica il nome del listener.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-trace.md)|Consente di aggiungere un filtro a un listener della raccolta `Listeners` per una traccia.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`listeners`|Consente di specificare un listener per la raccolta, la memorizzazione e l'invio di messaggi.  I listener indirizzano l'output di tracciatura a una destinazione adatta.|  
|`system.diagnostics`|Specifica l'elemento radice per la sezione di configurazione ASP.NET.|  
|`trace`|Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.|  
  
## Note  
 Le classi <xref:System.Diagnostics.Debug> e <xref:System.Diagnostics.Trace> condividono la stessa raccolta **Listeners**.  Se si aggiunge un oggetto listener alla raccolta di una delle due classi, lo stesso listener verrà utilizzato anche dall'altra classe.  Le classi di listener derivano dalla [classe TraceListener](frlrfSystemDiagnosticsTraceListenerClassTopic).  
  
 Se non viene specificato l'attributo `nam`e del listener di traccia, l'impostazione predefinita della proprietà <xref:System.Diagnostics.TraceListener.Name%2A> del listener di traccia sarà una stringa vuota \(""\).  Se l'applicazione dispone di un solo listener, è possibile aggiungerlo senza specificarne il nome e rimuoverlo specificando per il nome una stringa vuota.  Se invece l'applicazione dispone di più listener, è necessario specificare nomi univoci per ciascun listener di traccia, al fine di identificare e gestire singolarmente i listener di traccia nelle raccolte <xref:System.Diagnostics.Debug.Listeners%2A> e <xref:System.Diagnostics.Trace.Listeners%2A>.  
  
> [!NOTE]
>  L'aggiunta di più listener di traccia dello stesso tipo e con lo stesso nome implica l'aggiunta di un solo listener di traccia di tale tipo e con tale nome alla raccolta `Listeners`.  È tuttavia possibile aggiungere a livello di codice più listener identici alla raccolta `Listeners`.  
  
 Il valore dell'attributo **initializeData** dipende dal tipo di listener creato.  Non per tutti i listener di traccia è necessario specificare l'attributo **initializeData**.  
  
> [!NOTE]
>  Quando si utilizza l'attributo `initializeData`, è possibile ottenere l'avviso del compilatore "Attributo 'initializeData' non dichiarato". Questo avviso viene generato perché le impostazioni di configurazione vengono convalidate in base alla classe di base astratta <xref:System.Diagnostics.TraceListener> che non riconosce l'attributo `initializeData`.  In genere, è possibile ignorare questo avviso per implementazioni del listener di traccia che presentano un costruttore che accetta un parametro.  
  
 Nella tabella riportata di seguito vengono elencati i listener di traccia inclusi in .NET Framework e viene fornita una descrizione del valore dei relativi attributi **initializeData**.  
  
|Classe di listener di traccia|Valore dell'attributo initializeData|  
|-----------------------------------|------------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=fullName>|Valore `useErrorStream` del costruttore <xref:System.Diagnostics.ConsoleTraceListener.%23ctor%2A>.  Impostare l'attributo `initializeData` su "`true`" per scrivere l'output di traccia e debug in <xref:System.Console.Error%2A?displayProperty=fullName>, oppure su "`false`" per scrivere l'output in <xref:System.Console.Out%2A?displayProperty=fullName>.|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=fullName>|Nome del file in cui scrive <xref:System.Diagnostics.DelimitedListTraceListener>.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=fullName>|Nome di un'origine del log eventi esistente.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.EventSchemaTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.TextWriterTraceListener> esegue operazioni di scrittura.|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=fullName>|Nome del file in cui <xref:System.Diagnostics.XmlWriterTraceListener> esegue operazioni di scrittura.|  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare gli elementi **\<add\>** per aggiungere i listener `MyListener` e `MyEventListener` alla raccolta **Listeners**.  `MyListener` crea un file denominato `MyListener.log` e scrive l'output al suo interno.  `MyEventListener` crea una voce nel log eventi.  
  
```  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
            <add name="MyEventListener"  
                 type="System.Diagnostics.EventLogTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"                 initializeData="MyConfigEventLog"/>  
            <add name="configConsoleListener"  
                 type="System.Diagnostics.ConsoleTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.Debug>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 <xref:System.Diagnostics.ConsoleTraceListener>   
 <xref:System.Diagnostics.TextWriterTraceListener>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)