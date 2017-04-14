---
title: "1040 - InArgumentBound | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7dfaad1b-36c0-4575-84c1-31d63b0eaf5d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1040 - InArgumentBound
## Proprietà  
  
|||  
|-|-|  
|ID|1040|  
|Parole chiave|WFActivities|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un argomento In è stato associato.  
  
## Messaggio  
 Argomento In '%1' nell'attività '%2', DisplayName: '%3', InstanceId: '%4' è stato associato al valore: %5.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InArgument|xs:string|Nome dell'argomento In.|  
|Attività|xs:string|Il nome del tipo di attività.|  
|DisplayName|xs:string|Nome visualizzato dell'attività.|  
|InstanceId|xs:string|L'ID dell'istanza dell'attività.|  
|Valore|xs:string|Il valore associato all'argomento In.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|