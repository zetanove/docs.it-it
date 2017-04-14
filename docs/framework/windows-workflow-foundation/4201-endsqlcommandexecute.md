---
title: "4201 - EndSqlCommandExecute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae0dbc15-f98c-4096-a8d9-fbe4dc36f1cd
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 4201 - EndSqlCommandExecute
## Proprietà  
  
|||  
|-|-|  
|ID|4201|  
|Parole chiave|WFInstanceStore|  
|Livello|Dettagliato|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che un comando SQL ha completato l'esecuzione.  
  
## Messaggio  
 Fine esecuzione comando SQL: %1  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|SqlCommand|xs:string|Comando SQL eseguito.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|