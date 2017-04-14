---
title: "440 - StartSignpostEvent1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27b551b5-ae76-49f8-bab8-6300009eb4c1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 440 - StartSignpostEvent1
## Proprietà  
  
|||  
|-|-|  
|ID|440|  
|Parole chiave|Risoluzione dei problemi|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Server applicazioni\-Applicazioni\/Analitico|  
  
## Descrizione  
 Quando si traccia di attività, indica che un messaggio ha iniziato ad attraversare il limite di un'attività nell'invio o nella ricezione.  
  
## Messaggio  
 Limite dell'attività.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|ExtendedData|`xs:string`|Nome dell’attività.|  
|AppDomain|`xs:string`|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|