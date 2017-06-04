---
title: "Elemento &lt;remove&gt; per &lt;listeners&gt; per &lt;trace&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<remove> (elemento)"
  - "remove (elemento)"
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Elemento &lt;remove&gt; per &lt;listeners&gt; per &lt;trace&gt;
Consente di rimuovere un listener dalla raccolta **Listeners**.  
  
## Sintassi  
  
```  
  
<remove name="listener name" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|**name**|Attributo obbligatorio.<br /><br /> Nome del listener da rimuovere dalla raccolta **Listeners**.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`listeners`|Consente di specificare un listener per la raccolta, la memorizzazione e l'invio di messaggi.  I listener indirizzano l'output di tracciatura a una destinazione adatta.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`trace`|Configura il servizio di traccia di ASP.NET.|  
  
## Note  
  
> [!NOTE]
>  Rimuovendo la classe <xref:System.Diagnostics.DefaultTraceListener> dalla raccolta `Listeners` si modifica il comportamento dei metodi <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=fullName> e <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=fullName>.  La chiamata a un metodo `Assert` o `Fail` normalmente comporta la visualizzazione di una finestra di messaggio, ma la finestra di messaggio non viene visualizzata se la classe <xref:System.Diagnostics.DefaultTraceListener> non è contenuta nella raccolta `Listeners`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come rimuovere il listener di traccia predefinito dalla raccolta **Listeners** di traccia.  
  
```  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.TraceListener>   
 <xref:System.Diagnostics.DefaultTraceListener>   
 <xref:System.Diagnostics.TextWriterTraceListener>   
 <xref:System.Diagnostics.EventLogTraceListener>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)