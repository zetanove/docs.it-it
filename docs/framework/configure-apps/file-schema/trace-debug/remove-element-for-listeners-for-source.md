---
title: "Elemento &lt;remove&gt; per &lt;listeners&gt; per &lt;source&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<remove> (elemento) per <listeners> per <source>"
  - "remove (elemento) per <listeners> per <source>"
ms.assetid: 3ff6b578-273d-407f-b07f-8251f1f9f5d0
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Elemento &lt;remove&gt; per &lt;listeners&gt; per &lt;source&gt;
Rimuove un listener dalla raccolta `Listeners` per un'origine di traccia.  
  
## Sintassi  
  
```  
<remove name="listenerName" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo obbligatorio.<br /><br /> Nome del listener da rimuovere dalla raccolta `Listeners`.|  
  
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
 L'elemento `<remove>` consente di rimuovere un listener specificato dalla raccolta `Listeners` per un'origine di traccia.  
  
 È possibile rimuovere un elemento dalla raccolta `Listeners` per un'origine di traccia a livello di codice chiamando il metodo <xref:System.Diagnostics.TraceListenerCollection.Remove%2A> sulla proprietà <xref:System.Diagnostics.TraceSource.Listeners%2A> dell'istanza di <xref:System.Diagnostics.TraceSource>.  
  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<remove>` prima dell'elemento `<add>` per l'aggiunta del listener `console` alla raccolta `Listeners` per l'origine di traccia `TraceSourceApp`.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch" >  
         <listeners>  
           <remove name="Default"/>  
           <add name="console"   
             type="System.Diagnostics.ConsoleTraceListener" />  
         </listeners>  
      </source>  
    </sources>  
  </system.diagnostics>  
</configuration>   
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceSource.Listeners%2A>   
 <xref:System.Diagnostics.TraceSource>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [\<clear\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-source.md)   
 [Trace Listeners](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)