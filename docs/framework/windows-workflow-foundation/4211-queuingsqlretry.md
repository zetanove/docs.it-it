---
title: "4211 - QueuingSqlRetry | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df569f88-c86b-4503-840d-1399b67f4df7
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4211 - QueuingSqlRetry
## Proprietà  
  
|||  
|-|-|  
|ID|4211|  
|Parole chiave|WFInstanceStore|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica l'accodamento di nuovi tentativi di SQL.  
  
## Messaggio  
 Accodamento nuovi tentativi di SQL con ritardo di %1 millisecondi.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Delay|xs:string|Il ritardo tra i tentativi.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|