---
title: "Elemento &lt;sharedListeners&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#sharedListeners"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<sharedListeners> (elemento)"
  - "listener"
  - "listener condivisi"
  - "sharedListeners (elemento)"
  - "listener di traccia, <sharedListeners> (elemento)"
ms.assetid: de200534-19dd-4156-86cf-c50521802c4c
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Elemento &lt;sharedListeners&gt;
Contiene i listener a cui può fare riferimento un qualsiasi elemento di origine o di traccia.  Per impostazione predefinita, questi listener non ricevono alcuna traccia e non possono essere recuperati in fase di esecuzione.  I listener identificati come condivisi possono essere aggiunti alle origini o alle traccia in base al nome.  
  
## Sintassi  
  
```  
<sharedListeners>   
  <add>...</add>  
</sharedListeners>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-trace.md)|Consente di aggiungere un listener alla raccolta `sharedListeners`.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`Configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Specifica l'elemento radice per la sezione di configurazione ASP.NET.|  
  
## Note  
 Un listener aggiunto alla raccolta dei listener condivisi non diventa automaticamente attivo.  Deve infatti essere ancora aggiunto a un'origine di traccia o a una traccia, ovvero inserito nella raccolta `Listeners` per tale elemento di traccia.  Le classi di listener in .NET Framework derivano dalla classe <xref:System.Diagnostics.TraceListener>.  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<sharedListeners>` per aggiungere il listener `console` alla raccolta `Listeners` per le classi <xref:System.Diagnostics.TraceSource> e <xref:System.Diagnostics.Trace>.  Il listener di traccia di console scrive le informazioni sulla traccia sulla console mediante chiamate a <xref:System.Diagnostics.TraceSource> o a <xref:System.Diagnostics.Trace>.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sharedListeners>  
      <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"  
          initializeData="Warning" />  
      </add>  
    </sharedListeners>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch"  >  
        <listeners>  
          <add name="console" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="sourceSwitch" value="Verbose"/>  
    </switches>  
    <trace>  
      <listeners>  
        <add name="console" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration></system.diagnostics>   
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceListener>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)