---
title: "Elemento &lt;system.diagnostics&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#system.diagnostics"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<system.diagnostics> (elemento)"
  - "system.diagnostics (elemento)"
ms.assetid: 3f348f42-fa72-4ff2-aa1c-bb9eecad4bb2
caps.latest.revision: 17
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 15
---
# Elemento &lt;system.diagnostics&gt;
Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.  
  
## Sintassi  
  
```  
<system.diagnostics>   
</system.diagnostics>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<assert\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/assert-element.md)|Consente di specificare se deve essere visualizzata una finestra di messaggio quando viene richiamato il metodo <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> e permette, inoltre, di specificare il nome del file in cui scrivere i messaggi.|  
|[\<performanceCounters\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/performancecounters-element.md)|Specifica la dimensione della memoria globale condivisa dai contatori delle prestazioni.|  
|[\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md)|Contiene i listener a cui può fare riferimento un qualsiasi elemento di origine o di traccia.  I listener identificati come condivisi possono essere aggiunti alle origini o alle traccia in base al nome.|  
|[\<origini\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sources-element.md)|Specifica le origini di traccia che danno inizio ai messaggi di tracciatura.|  
|[\<parametri\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/switches-element.md)|Contiene opzioni di traccia e i livelli in cui vengono impostate.|  
|[\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md)|Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come incorporare un'opzione di traccia e un listener di traccia all'interno dell'elemento **\<system.diagnostics\>**.  L'opzione di traccia `General` è impostata sul livello [TraceLevel.Error](frlrfSystemDiagnosticsTraceLevelClassTopic).  Il listener di traccia `myListener` crea un file denominato `MyListener.log` e scrive l'output al suo interno.  
  
> [!NOTE]
>  In .NET Framework versione 2.0 è possibile utilizzare testo per specificare il valore di un'opzione,  ad esempio `true` per <xref:System.Diagnostics.BooleanSwitch> o il testo che rappresenta un valore di enumerazione, come `Error`, per la classe <xref:System.Diagnostics.TraceSwitch>.  La riga `<add name="myTraceSwitch" value="Error" />` equivale a `<add name="myTraceSwitch" value="1" />`.  
  
```  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
      </switches>  
      <trace autoflush="true" indentsize="2">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="MyListener.log" traceOutputOptions="ProcessId, LogicalOperationStack, Timestamp, ThreadId, Callstack, DateTime" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.Debug>   
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)