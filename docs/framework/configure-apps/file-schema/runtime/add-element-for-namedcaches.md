---
title: "Elemento &lt;add&gt; per &lt;namedCaches&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<add> (elemento) per <namedCaches>"
  - "add (elemento) per <namedCaches>"
ms.assetid: ce2a63a8-c829-4742-a6ea-72ee5d89f169
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;add&gt; per &lt;namedCaches&gt;
Aggiunge una voce `namedCache` alla raccolta `namedCaches` per una cache in memoria.  
  
## Sintassi  
  
```  
<namedCaches>  
    <add name="default" />  
      <!-- child elements -->  
 </namedCaches>  
```  
  
## Tipo  
 `None`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|||  
|-|-|  
|Attributo|Descrizione|  
|`CacheMemoryLimitMegabytes`|Valore intero che specifica la dimensione massima consentita \(in megabyte\) che un'istanza di un oggetto <xref:System.Runtime.Caching.MemoryCache> può raggiungere.  Il valore predefinito è 0, il che indica che le euristiche di dimensionamento automatico della classe <xref:System.Runtime.Caching.MemoryCache> sono utilizzate per impostazione predefinita.|  
|`Name`|Nome della cache.|  
|`PhysicalMemoryLimitPercentage`|Un valore intero tra 0 e 100 specifica la percentuale massima di memoria del computer fisicamente installata che può essere utilizzata dalla cache.  Il valore predefinito è 0, il che indica che le euristiche di dimensionamento automatico della classe <xref:System.Runtime.Caching.MemoryCache> sono utilizzate per impostazione predefinita.|  
|`PollingInterval`|Un valore che indica l'intervallo di tempo, trascorso il quale l'implementazione della cache confronta il carico di memoria corrente a fronte dei limiti di memoria in percentuale e assoluti impostati per l'istanza della cache.  Il valore viene immesso in formato "hh:mm:ss."|  
  
### Elementi figlio  
 `None`  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<namedCaches\>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|Contiene una raccolta di impostazioni di configurazione delle istanze di <xref:System.Runtime.Caching.MemoryCache> denominate.|  
  
## Note  
 L'elemento `add` aggiunge una voce alla raccolta `namedCaches` per una cache in memoria.  È possibile utilizzare l'elemento [clear](../../../../../docs/framework/configure-apps/file-schema/runtime/clear-element-for-namedcaches.md) prima dell'elemento `add` per essere certi che nella raccolta non vi siano altri listener attivi.    È possibile utilizzare questo elemento nei file di configurazione del computer \(machine.config\) e dell'applicazione e nel file di configurazione web \(Web.config\).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come definire le impostazioni per la voce `namedCache` predefinita nella raccolta `namedCaches`  per una cache in memoria.  
  
```  
<configuration>  
  
  <system.runtime.caching>  
    <memoryCache>  
      <namedCaches>  
          <add name="default"   
               cacheMemoryLimitMegabytes="0"   
               physicalMemoryPercentage="0"  
               pollingInterval="00:02:00" />  
      </namedCaches>  
    </memoryCache>  
  </system.runtime.caching>  
  
</configuration>  
```  
  
## Vedere anche  
 [Elemento \<namedCaches\> \(impostazioni cache\)](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)