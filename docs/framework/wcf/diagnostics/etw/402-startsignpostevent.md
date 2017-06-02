---
title: "402 - StartSignpostEvent | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5e5be126-765d-4ac9-88e7-008e9ef4f0e5
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 402 - StartSignpostEvent
## Proprietà  
  
|||  
|-|-|  
|ID|402|  
|Parole chiave|Risoluzione dei problemi|  
|Livello|Informazioni|  
|Channel|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Questo evento contrassegna l'inizio di un'attività end\-to\-endcontenente il nome dell’attività.  
  
## Messaggio  
 Limite dell'attività.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Dati estesi|`xs:string`|Nome dell’attività.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|