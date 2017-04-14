---
title: "1035 - RuntimeTransactionSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 03b37de9-778c-4beb-b0e3-de73ece6088e
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1035 - RuntimeTransactionSet
## Proprietà  
  
|||  
|-|-|  
|ID|1035|  
|Parole chiave|WFRuntime|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un'attività ha impostato la transazione runtime.  
  
## Messaggio  
 Transazione di runtime impostata dall'attività '%1', DisplayName: '%2', InstanceId: '%3'. Esecuzione isolata all'attività '%4', DisplayName: '%5', InstanceId: '%6'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Attività|xs:string|Il nome del tipo di attività.|  
|DisplayName|xs:string|Nome visualizzato dell'attività.|  
|InstanceId|xs:string|L'ID dell'istanza dell'attività.|  
|IsolatedActivity|xs:string|Il nome del tipo di attività che la transazione su cui è isolata.|  
|IsolatedActivityDisplayName|xs:string|Il nome visualizzato dell'attività che la transazione su cui è isolata.|  
|IsolatedActivityInstanceId|xs:string|L'ID istanza dell'attività che la transazione su cui è isolata.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|