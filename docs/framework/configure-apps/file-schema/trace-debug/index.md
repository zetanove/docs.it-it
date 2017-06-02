---
title: "Schema delle impostazioni di traccia e debug | Microsoft Docs"
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
  - "schema di configurazione [.NET Framework], impostazioni di traccia e debug"
  - "sezioni di configurazione [.NET Framework]"
  - "impostazioni di configurazione [.NET Framework], debug"
  - "impostazioni di configurazione [.NET Framework], traccia"
  - "elementi [.NET Framework], impostazioni di traccia e debug"
  - "impostazioni di configurazione di schema"
  - "listener di traccia, schema delle impostazioni di traccia e debug"
  - "traccia [.NET Framework], schema delle impostazioni di traccia e debug"
ms.assetid: 277ca5f6-e1c4-41b6-a47f-3a67ce5b94ac
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Schema delle impostazioni di traccia e debug
Le impostazioni di traccia e debug consentono di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di traccia.  
  
 Nella tabella riportata di seguito viene descritta la funzione di ciascun elemento delle impostazioni di traccia e debug.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-source.md)|Consente di aggiungere un listener alla raccolta `Listeners` per un'origine di traccia.|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-listeners-for-trace.md)|Consente di aggiungere un listener alla raccolta `Listeners`.|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-sharedlisteners.md)|Consente di aggiungere un listener alla raccolta `sharedListeners`.|  
|[\<add\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/add-element-for-switches.md)|Consente di specificare il livello in cui viene impostata un'opzione di traccia.|  
|[\<assert\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/assert-element.md)|Consente di specificare se deve essere visualizzata una finestra di messaggio quando viene richiamato il metodo <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> e permette, inoltre, di specificare il nome del file in cui scrivere i messaggi.|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-source.md)|Cancella la raccolta `Listeners` per un'origine di traccia.|  
|[\<clear\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-trace.md)|Cancella la raccolta `Listeners` per la traccia.|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-source.md)|Consente di aggiungere un filtro a un listener della raccolta `Listeners` per un'origine di traccia.|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-listeners-for-trace.md)|Consente di aggiungere un filtro a un listener della raccolta `Listeners` per la traccia.|  
|[\<filter\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/filter-element-for-add-for-sharedlisteners.md)|Consente di aggiungere un filtro a un listener della raccolta `sharedListeners`.|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-source.md)|Specifica i listener per la raccolta `Listeners` per un'origine di traccia.|  
|[\<listeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/listeners-element-for-trace.md)|Specifica i listener della raccolta `Listeners` per la traccia.|  
|[\<performanceCounters\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/performancecounters-element.md)|Specifica la dimensione della memoria globale condivisa dai contatori delle prestazioni.|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-trace.md)|Consente di rimuovere un listener dalla raccolta `Listeners` per la traccia.|  
|[\<remove\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/remove-element-for-listeners-for-source.md)|Rimuove un listener dalla raccolta `Listeners` per un'origine di traccia.|  
|[\<sharedListeners\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sharedlisteners-element.md)|Contiene i listener a cui può fare riferimento un qualsiasi elemento di origine o di traccia.|  
|[\<sources\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/sources-element.md)|Contiene le origini di analisi che danno inizio ai messaggi di tracciatura.|  
|[\<source\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/source-element.md)|Specifica un'origine di analisi che dà inizio ai messaggi di tracciatura.|  
|[\<switches\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/switches-element.md)|Contiene opzioni di traccia e il livello in cui vengono impostate.|  
|[\<system.diagnostics\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/system-diagnostics-element.md)|Consente di specificare listener di traccia per la raccolta, la memorizzazione e l'invio di messaggi, nonché il livello in cui viene impostata un'opzione di analisi.|  
|[\<trace\>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/trace-element.md)|Contiene listener per la raccolta, la memorizzazione e l'invio di messaggi di tracciatura.|  
  
## Vedere anche  
 <xref:System.Diagnostics.Trace>   
 <xref:System.Diagnostics.TraceSource>   
 <xref:System.Diagnostics.Debug>   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)