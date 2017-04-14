---
title: "Optimization for Shared Web Hosting | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "garbage collection, Web hosting"
  - "garbage collection, optimizing"
  - "garbage collection, shared Web hosting"
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Optimization for Shared Web Hosting
L'amministratore di un server condiviso che ospita alcuni siti Web di piccole dimensioni può ottimizzare le prestazioni e aumentare le capacità del sito aggiungendo l'impostazione `gcTrimCommitOnLowMemory` seguente al nodo `runtime` nel file Aspnet.config della directory Framework .NET:  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
>  Questa impostazione è consigliata solo per scenari di hosting Web condiviso.  
  
 Poiché il Garbage Collector riserva una parte di memoria per future allocazioni, lo spazio utilizzato può risultare maggiore di quello effettivamente necessario.  È possibile ridurre tale spazio nei casi in cui la memoria di sistema è sottoposta a un carico di lavoro eccessivo.  La riduzione di tale spazio determina un miglioramento delle prestazioni e un ampliamento delle capacità in modo da ospitare più siti.  
  
 Quanto è abilitata l'impostazione `gcTrimCommitOnLowMemory` il Garbage Collector valuta il carico della memoria di sistema e attiva la modalità trimming quando il carico raggiunge il 90%.  Tale modalità rimane attiva finché il carico non scende al di sotto dell'85%.  
  
 A seconda delle condizioni, il Garbage Collector può ignorare l'impostazione `gcTrimCommitOnLowMemory` ritenendola non utile all'applicazione.  
  
## Esempio  
 Nel frammento XML seguente viene indicato come attivare l'impostazione `gcTrimCommitOnLowMemory`.  I puntini di sospensione indicano altre impostazioni presenti nel nodo `runtime`.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## Vedere anche  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)