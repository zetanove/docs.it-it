---
title: "4210 - SqlExceptionCaught | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0ce8af3-eb4c-48c8-b3d9-dd2f94b5574b
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4210 - SqlExceptionCaught
## Proprietà  
  
|||  
|-|-|  
|ID|4210|  
|Parole chiave|WFInstanceStore|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che è stata rilevata un'eccezione SQL.  
  
## Messaggio  
 Rilevata eccezione SQL numero %1 messaggio %2.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|ErrorNumber|xs:string|Numero di errore SQL.|  
|ExceptionMessage|xs:string|Messaggio dell'eccezione SQL.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|