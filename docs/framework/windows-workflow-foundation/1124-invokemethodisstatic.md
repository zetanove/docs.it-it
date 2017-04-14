---
title: "1124 - InvokeMethodIsStatic | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9643641-fb52-4fa8-b354-4dd6617d68f6
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1124 - InvokeMethodIsStatic
## Proprietà  
  
|||  
|-|-|  
|ID|1124|  
|Parole chiave|WFRuntime|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Durante il passaggio CacheMetadata, l'attività InvokeMethod indica che il metodo da richiamare è statico.  
  
## Messaggio  
 InvokeMethod '%1': il metodo è statico.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InvokeMethod|xs:string|Nome visualizzato dell'attività InvokeMethod.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|