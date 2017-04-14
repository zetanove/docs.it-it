---
title: "1010 - ActivityCompleted | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d256284e-3fd2-4c33-82f4-abb617575706
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 1010 - ActivityCompleted
## Proprietà  
  
|||  
|-|-|  
|ID|1010|  
|Parole chiave|WFRuntime|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che l'esecuzione di un'attività è stata completata.  
  
## Messaggio  
 Attività "%1 " DisplayName:, "%2", InstanceId: "%3 " è stata completata in "%4 " stato.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Attività|xs:string|Il nome del tipo di attività.|  
|DisplayName|xs:string|Nome visualizzato dell'attività.|  
|InstanceId|xs:string|L'ID dell'istanza dell'attività.|  
|Stato|xs:string|Stato dell'attività.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|