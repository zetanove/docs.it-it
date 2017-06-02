---
title: "1015 - StartCompletionWorkItem | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96fd1d4e-c5d0-46ad-8a71-4b4b49ac7262
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1015 - StartCompletionWorkItem
## Proprietà  
  
|||  
|-|-|  
|ID|1015|  
|Parole chiave|WFRuntime|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che viene avviata l'esecuzione di CompletionWorkItem.  
  
## Messaggio  
 Avvio dell'esecuzione di CompletionWorkItem per l'attività padre '%1', DisplayName: '%2', InstanceId: '%3'.  Attività '%4', DisplayName: '%5', InstanceId: '%6' completata.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|ParentActivity|xs:string|Nome tipo dell'attività padre.|  
|ParentDisplayName|xs:string|Nome visualizzato dell'attività padre.|  
|ParentInstanceId|xs:string|ID dell'istanza dell'attività padre.|  
|CompletedActivity|xs:string|Nome tipo dell'attività completata.|  
|CompletedActivityDisplayName|xs:string|Nome visualizzato dell'attività completata.|  
|CompletedActivityInstanceId|xs:string|L'ID dell'istanza dell'attività completata.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|