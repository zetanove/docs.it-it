---
title: "Contatori delle prestazioni per l&#39;operazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 333a51e0-f56e-4e1a-b359-5c91ff390568
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Contatori delle prestazioni per l&#39;operazione
I contatori delle prestazioni per l'operazione si trovano nell'oggetto prestazione `ServiceModelOperation 4.0.0.0` in caso di visualizzazione con Performance Monitor \(Perfmon.exe\).Ogni operazione ha un'istanza singola.Ovvero, se un determinato contratto ha 10 operazioni, ad esso sono associate 10 istanze di contatore per l'operazione.Le istanze di oggetti vengono denominate utilizzando il modello seguente:  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 Questo contatore consente di misurare come viene utilizzata la chiamata e le prestazioni dell'operazione.  
  
> [!CAUTION]
>  Esiste un limite di lunghezza per il nome dell'istanza di un contatore delle prestazioni.Quando il nome dell'istanza di un contatore [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] supera la lunghezza massima, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] sostituisce una parte del nome dell'istanza con un valore hash.  
  
## Vedere anche  
 [Contatori di prestazioni](../../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)