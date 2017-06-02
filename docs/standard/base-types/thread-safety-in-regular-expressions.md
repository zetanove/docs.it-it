---
title: "Thread safety nelle espressioni regolari | Microsoft Docs"
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
  - "espressioni regolari di .NET Framework, thread"
  - "analisi di testo con espressioni regolari, thread"
  - "corrispondenza al modello con espressioni regolari, thread"
  - "espressioni regolari, thread"
  - "ricerca con espressioni regolari, thread"
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Thread safety nelle espressioni regolari
La classe <xref:System.Text.RegularExpressions.Regex> è thread\-safe e non modificabile \(in sola lettura\).  In altre parole, gli oggetti **Regex** possono essere creati in qualsiasi thread e condivisi da thread diversi. I metodi di corrispondenza possono essere chiamati da qualsiasi thread e non modificano mai alcuno stato globale.  
  
 È tuttavia necessario utilizzare gli oggetti restituiti da**Regex** \( **Match**e **MatchCollection** \) in un singolo thread.  Sebbene molti di questi oggetti siano immutabili dal punto di vista logico, le relative implementazioni possono ritardare il calcolo di alcuni risultati per migliorare le prestazioni ed è quindi necessario che i chiamanti vi accedano serialmente.  
  
 Se è necessario condividere gli oggetti dei risultati di **Regex** in più thread, sarà possibile convertire tali oggetti in istanze thread\-safe chiamando i relativi metodi sincronizzati.  Fatta eccezione per gli enumeratori, tutte le classi di espressioni regolari sono thread\-safe o possono essere convertite in oggetti thread\-safe da un metodo sincronizzato.  
  
 Gli enumeratori rappresentano l'unica eccezione.  È necessario che un'applicazione serializzi le chiamate agli enumeratori di raccolte.  Se una raccolta può essere enumerata in più thread contemporaneamente, sarà necessario sincronizzare i metodi dell'enumeratore all'oggetto radice della raccolta enumerata.  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)