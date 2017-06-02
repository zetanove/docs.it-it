---
title: "Elemento &lt;clear&gt; per &lt;namedCaches&gt; | Microsoft Docs"
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
  - "<clear> (elemento) per <namedCaches>"
  - "clear (elemento) per <namedCaches>"
ms.assetid: ea01a858-65da-4348-800f-5e3df59d4d79
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Elemento &lt;clear&gt; per &lt;namedCaches&gt;
Cancellare tutte le voci `namedCache` nella raccolta `namedCaches` per una cache in memoria.  
  
## Sintassi  
  
```  
<namedCaches>  
    <clear name="default" />  
    <!-- child elements -->  
 </namedCaches>  
```  
  
## Tipo  
 `Type`  
  
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
 L'elemento `clear` cancella tutte le voci nella raccolta della cache denominata `namedCache` per una cache in memoria.  È possibile utilizzare l'elemento `clear` prima dell'elemento `add` da aggiungere alla nuova cache denominata per essere certi che nella raccolta non vi siano altre cache denominate.  
  
## Vedere anche  
 [Elemento \<namedCaches\> \(impostazioni cache\)](../../../../../docs/framework/configure-apps/file-schema/runtime/namedcaches-element-cache-settings.md)