---
title: "Elemento &lt;source&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#source"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<source> (elemento)"
  - "source (elemento)"
ms.assetid: ecf86505-735d-4844-aaba-266fdd134218
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;source&gt;
Specifica un'origine di analisi che dà inizio ai messaggi di tracciatura.  
  
## Sintassi  
  
```  
<source>   
  <listeners>...</listeners>  
</source>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo facoltativo.<br /><br /> Specifica il nome dell'origine di traccia.|  
|`switchName`|Attributo facoltativo.<br /><br /> Specifica il nome di un'istanza dell'opzione di traccia nell'applicazione.  Se l'opzione non è identificata in un elemento `<switches>`, il valore indica il livello dell'opzione.|  
|`switchType`|Attributo facoltativo.<br /><br /> Specifica il tipo dell'opzione di traccia.  Se presente, il tipo deve essere un nome di classe valido e non può essere costituito da una stringa vuota.|  
|`extraAttribute`|Attributo facoltativo.<br /><br /> Specifica il valore di un attributo database di origine\-specifico di traccia identificato dal metodo di <xref:System.Diagnostics.TraceSource.GetSupportedAttributes%2A> per l'origine di traccia.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-trace.md)|Contiene listener per la raccolta, l'archiviazione e l'invio di messaggi.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|`sources`|Contiene le origini di analisi che danno inizio ai messaggi di tracciatura.|  
  
## Note  
 È possibile utilizzare questo elemento nei file di configurazione del computer \(Machine.config\) e dell'applicazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo dell'elemento `<source>`  per aggiungere l'origine di traccia `mySource` e impostare il livello per l'opzione di origine denominata `sourceSwitch`.  Viene aggiunto un listener di analisi di console che consente di scrivere le informazioni di traccia sulla console.  
  
```  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch" switchType="System.Diagnostics.SourceSwitch"  >  
        <listeners>  
          <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
            <filter type="System.Diagnostics.EventTypeFilter" initializeData="Error" />  
          </add>  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
        <switches>  
           <add name="sourceSwitch" value="Warning" />  
        </switches>    
  </system.diagnostics>   
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni di traccia e debug](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)   
 [Trace Switches](../../../../../docs/framework/debug-trace-profile/trace-switches.md)