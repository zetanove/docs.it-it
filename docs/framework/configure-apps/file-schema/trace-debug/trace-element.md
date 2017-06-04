---
title: "Elemento &lt;trace&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#trace"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<trace> (elemento)"
  - "listener"
  - "trace (elemento)"
  - "listener di traccia, <trace> (elemento)"
ms.assetid: 7931c942-63c1-47c3-a045-9d9de3cacdbf
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;trace&gt;
Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.  
  
## Sintassi  
  
```  
<trace autoflush="true|false"   
       indentsize="indent value"  
       useGlobalLock="true| false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`autoflush`|Attributo facoltativo.<br /><br /> Indica se i listener di traccia svuotano automaticamente il buffer di output dopo ogni operazione di scrittura.|  
|`indentsize`|Attributo facoltativo.<br /><br /> Specifica il numero di spazi da utilizzare per il rientro.|  
|`useGlobalLock`|Attributo facoltativo.<br /><br /> Indica se utilizzare il blocco globale.|  
  
## Attributo autoflush  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Il buffer di output non viene svuotato automaticamente.  Questa è l'impostazione predefinita.|  
|`true`|Il buffer di output viene svuotato automaticamente.|  
  
## Attributo useGlobalLock  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Non utilizza il blocco globale se il listener è thread\-safe; in caso contrario, utilizza il blocco globale.|  
|`true`|Utilizza il blocco globale indipendentemente dal fatto che il listener sia thread\-safe.  Questa è l'impostazione predefinita.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-trace.md)|Consente di specificare un listener per la raccolta, la memorizzazione e l'invio di messaggi.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'elemento `<trace>` per aggiungere il listener `MyListener` alla raccolta `Listeners`.  `MyListener` crea un file denominato `MyListener.log` e scrive l'output al suo interno.  L'attributo `useGlobalLock` è impostato su `false`, quindi il blocco globale non viene utilizzato se il listener di traccia è thread\-safe.  L'attributo `autoflush` è impostato su `true`, quindi il listener di traccia scrive all'interno del file indipendentemente dal fatto che sia stato chiamato il metodo <xref:System.Diagnostics.Trace.Flush%2A?displayProperty=fullName>.  L'attributo `indentsize` è impostato su 0 \(zero\), quindi il listener non utilizza alcuno spazio per il rientro quando viene chiamato il metodo <xref:System.Diagnostics.Trace.Indent%2A?displayProperty=fullName>.  
  
```  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
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