---
title: "Elemento &lt;remove&gt; per &lt;namedCaches&gt; | Microsoft Docs"
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
  - "<remove> (elemento) per namedCaches"
  - "remove (elemento) per namedCaches"
ms.assetid: 24211ea5-163e-4fe5-aed8-004d8499760c
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Elemento &lt;remove&gt; per &lt;namedCaches&gt;
Rimuove una cache denominata dalla raccolta `namedCaches` per una cache in memoria.  
  
## Sintassi  
  
```  
<namedCaches>  
    <remove name="default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## Tipo  
 `None`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 `None`  
  
### Elementi figlio  
 `None`  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<namedCaches\>](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)|Contiene una raccolta di impostazioni di configurazione delle istanze di <xref:System.Runtime.Caching.MemoryCache> denominate.|  
  
## Note  
 L'elemento `remove` rimuove una voce `namedCache` dalla raccolta della cache denominata per una cache in memoria.  
  
## Vedere anche  
 [Elemento \<namedCaches\> \(impostazioni cache\)](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)