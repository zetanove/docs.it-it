---
title: "Contatori delle prestazioni del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4210f549-31f2-4ea7-99bd-69eaffb98ddf
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Contatori delle prestazioni del servizio
I contatori delle prestazioni del servizio misurano il comportamento del servizio nel suo insieme e possono essere utilizzati per diagnosticare le prestazioni dell'intero servizio.Sono reperibili nell'oggetto prestazione `ServiceModelService 4.0.0.0` in caso di visualizzazione con Performance Monitor \(Perfmon.exe\).Le istanze vengono denominate utilizzando il modello seguente:  
  
```  
ServiceName@ServiceBaseAddress  
```  
  
> [!CAUTION]
>  Esiste un limite di lunghezza per il nome dell'istanza di un contatore delle prestazioni.Quando il nome dell'istanza di un contatore [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] supera la lunghezza massima, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] sostituisce una parte del nome dell'istanza con un valore hash.  
  
## Vedere anche  
 [Contatori di prestazioni](../../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)