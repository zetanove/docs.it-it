---
title: "1034 - CompleteRuntimeWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45620011-8b04-4f87-ab5a-65b24145e17d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1034 - CompleteRuntimeWorkItem
## Proprietà  
  
|||  
|-|-|  
|ID|1034|  
|Parole chiave|WFRuntime|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che RuntimeWorkItem è completato.  
  
## Messaggio  
 Elemento di lavoro del runtime completato per l'attività '%1', DisplayName: '%2', InstanceId: '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Attività|xs:string|Il nome del tipo di attività.|  
|DisplayName|xs:string|Nome visualizzato dell'attività.|  
|InstanceId|xs:string|L'ID dell'istanza dell'attività.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|