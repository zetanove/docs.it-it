---
title: "Elemento &lt;namedCaches&gt; (impostazioni cache) | Microsoft Docs"
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
  - "<namedCaches> (elemento)"
  - "memorizzazione nella cache [.NET Framework], configurazione"
  - "namedCaches (elemento)"
ms.assetid: 6bd4fbc5-55a6-4dc4-998b-cdcc7e023330
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;namedCaches&gt; (impostazioni cache)
Specifica una raccolta di impostazioni di configurazione delle istanze di <xref:System.Runtime.Caching.MemoryCache> denominate.  La proprietà <xref:System.Runtime.Caching.Configuration.MemoryCacheSection.NamedCaches%2A> fa riferimento all'insieme di impostazioni di configurazione da uno o più elementi `namedCaches` del file di configurazione.  
  
## Sintassi  
  
```  
<namedCaches>  
  <add name="default"   
</namedCaches>  
```  
  
## Tipo  
 `None`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`CacheMemoryLimitMegabytes`|Valore intero che specifica la dimensione massima consentita, in megabyte, che un'istanza di un oggetto <xref:System.Runtime.Caching.MemoryCache> può raggiungere.  Il valore predefinito è 0, il che indica che le euristiche di dimensionamento automatico della classe <xref:System.Runtime.Caching.MemoryCache> sono utilizzate per impostazione predefinita.|  
|`Name`|Nome della cache.|  
|`PhysicalMemoryLimitPercentage`|Un valore intero tra 0 e 100 specifica la percentuale massima di memoria del computer fisicamente installata che può essere utilizzata dalla cache.  Il valore predefinito è 0, il che indica che le euristiche di dimensionamento automatico della classe <xref:System.Runtime.Caching.MemoryCache> sono utilizzate per impostazione predefinita.|  
|`PollingInterval`|Un valore che indica l'intervallo di tempo, trascorso il quale l'implementazione della cache confronta il carico di memoria corrente a fronte dei limiti di memoria in percentuale e assoluti impostati per l'istanza della cache.  Il valore viene immesso in formato "hh:mm:ss."|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/runtime/add-element-for-namedcaches.md)|Aggiunge una cache denominata alla raccolta `namedCaches` per una cache di memoria.|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/runtime/clear-element-for-namedcaches.md)|Cancella la raccolta `namedCaches` per una cache in memoria.|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/runtime/remove-element-for-namedcaches.md)|Rimuove una cache denominata dalla raccolta `namedCaches` per una cache in memoria.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<memoryCache\>](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md)|Definisce un elemento utilizzato per configurare una cache basata sulla classe <xref:System.Runtime.Caching.MemoryCache>.|  
  
## Note  
 La sezione di configurazione della cache in memoria del file Web.config può contenere attributi `add`, `remove` e `clear` per la raccolta `namedCaches`.  La voce `namedCaches` viene identificata in modo univoco dall'attributo `name`.  
  
 È possibile recuperare istanze di voci della cache in memoria facendo riferimento alle informazioni nei file di configurazione dell'applicazione.  Per impostazione predefinita, solo l'istanza della cache predefinita dispone di una voce nel file di configurazione.  L'istanza della cache predefinita è l'istanza restituita dalla proprietà <xref:System.Runtime.Caching.MemoryCache.Default%2A>.  
  
 Se si imposta l'attributo del nome in "predefinito", l'elemento utilizza l'istanza della cache in memoria predefinita.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come impostare il nome della cache nel nome della voce della cache predefinita, impostando l'attributo `name` su "valore predefinito".  
  
 L'attributo `cacheMemoryLimitMegabytes` e l'attributo `physicalMemoryPercentage` sono impostati su zero.  Impostando questi attributi su zero, vengono utilizzate le regole euristiche di dimensionamento automatico della classe <xref:System.Runtime.Caching.MemoryCache>.  L'implementazione della cache confronta il carico di memoria corrente ai limiti di memoria in percentuale e assoluti ogni due minuti.  
  
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
 [Elemento \<memoryCache\> \(Impostazioni cache\)](../../../../../docs/framework/configure-apps/file-schema/runtime/memorycache-element-cache-settings.md)