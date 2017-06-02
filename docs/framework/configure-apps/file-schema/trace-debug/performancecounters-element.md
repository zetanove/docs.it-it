---
title: "Elemento &lt;performanceCounters&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/performanceCounters"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<perfomanceCounters> (elemento)"
  - "performanceCounters (elemento)"
ms.assetid: a71f605b-c7d9-4501-a5c3-abcbb964a43f
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Elemento &lt;performanceCounters&gt;
Specifica la dimensione della memoria globale condivisa dai contatori delle prestazioni.  
  
## Sintassi  
  
```  
<performanceCounters filemappingsize="524288" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|filemappingsize|Attributo obbligatorio.<br /><br /> Specifica la dimensione, in byte, della memoria globale condivisa dai contatori delle prestazioni.  Il valore predefinito è 524288.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`Configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.diagnostics`|Specifica l'elemento radice per la sezione di configurazione ASP.NET.|  
  
## Note  
 Ai fini della pubblicazione dei dati relativi alle prestazioni nei contatori delle prestazioni viene utilizzato un file mappato alla memoria, o memoria condivisa.  La dimensione della memoria condivisa determina il numero di istanze utilizzabili contemporaneamente.  Sono disponibili due tipi di memoria condivisa, ovvero la memoria condivisa globale e la memoria condivisa separata.  La memoria condivisa globale viene utilizzata in tutte le categorie di contatori delle prestazioni installate con .NET Framework versione 1.0 o 1.1.  Per le categorie di contatori delle prestazioni installate con .NET Framework versione 2.0 vengono utilizzate memorie condivise separate, pertanto ciascuna categoria dispone di una propria memoria.  
  
 La dimensione della memoria condivisa globale può essere impostata solo tramite un file di configurazione.  La dimensione predefinita è pari a 524.288 byte, quella massima a 33.554.432 byte e quella minima a 32.768 byte.  Poiché la memoria condivisa globale viene condivisa tra tutti i processi e tutte le categorie, la relativa dimensione viene specificata dal primo creatore.  L'eventuale dimensione definita nel file di configurazione dell'applicazione verrà utilizzata solo se l'applicazione in uso è la prima a determinare l'esecuzione dei contatori delle prestazioni.  Il valore `filemappingsize` deve quindi essere specificato nel file Machine.config.  I singoli contatori delle prestazioni non possono rilasciare la memoria allocata alla memoria condivisa globale, pertanto quest'ultima esaurirà lo spazio disponibile se viene creato un numero elevato di istanze dei contatori delle prestazioni con nomi diversi.  
  
 Per la dimensione della memoria condivisa separata viene fatto riferimento innanzitutto al valore della chiave DWORD FileMappingSize HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\*\<category name\>*\\Performance del Registro di sistema e quindi al valore specificato per la memoria condivisa globale nel file di configurazione.  Se il valore FileMappingSize non esiste, la dimensione della memoria condivisa separata verrà impostata su un quarto \(1\/4\) dell'impostazione globale nel file di configurazione.  
  
## Vedere anche  
 <xref:System.Diagnostics.PerformanceCounter>   
 <xref:System.Diagnostics.PerformanceCounterCategory>   
 <xref:System.Diagnostics.PerformanceCounter.InstanceLifetime%2A>   
 <xref:System.Diagnostics.PerformanceCounterInstanceLifetime>