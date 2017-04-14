---
title: "Elemento &lt;filter&gt; per &lt;add&gt; per &lt;sharedListeners&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add/filter"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<filter> (elemento) per <add> per <sharedListeners>"
  - "filter (elemento) per <add> per <sharedListeners>"
  - "filtri, listener di traccia"
  - "attributo initializeData"
  - "listener di traccia, filtri"
ms.assetid: 7d4e7faa-2e4e-4379-ac76-f6cd7f2f8fac
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Elemento &lt;filter&gt; per &lt;add&gt; per &lt;sharedListeners&gt;
Consente di aggiungere un filtro a un listener della raccolta `sharedListeners`.  
  
## Sintassi  
  
```  
<filter type="System.Diagnostics.EventTypeFilter"   
  initializeData="Warning" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**type**|Attributo obbligatorio.<br /><br /> Specifica il tipo di filtro.  È possibile utilizzare solo il nome completo del tipo nel formato della proprietà <xref:System.Type.FullName%2A?displayProperty=fullName> oppure il nome completo del tipo incluse le informazioni sull'assembly nel formato della proprietà <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName>.  Per informazioni sulla creazione di un nome di tipo completo, vedere [Specifying Fully Qualified Type Names](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
|**initializeData**|Attributo facoltativo.<br /><br /> Stringa passata al costruttore per la classe specificata.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`sharedListeners`|Raccolta di listener cui può fare riferimento qualsiasi elemento di origine o di traccia.|  
|`add`|Consente di aggiungere un listener alla raccolta **sharedListeners**.|  
  
## Note  
 Se un listener viene definito in un elemento `<add>` dell'elemento `<sharedListeners>`, è necessario definire il filtro per tale listener in un elemento `<filter>` figlio dell'elemento `<add>`.  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<filter>` per aggiungere un filtro al listener di traccia `console` nella raccolta `sharedListeners`.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" >  
        <listeners>  
          <add name="console" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="console"   
        type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"   
          initializeData="Error" />  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceFilter>   
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.TraceSource>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)