---
title: "3551 - BufferOutOfOrderMessageNoBookmark | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7930d6c4-c843-4a83-933a-cecd71b80d1e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3551 - BufferOutOfOrderMessageNoBookmark
## Proprietà  
  
|||  
|-|-|  
|ID|3551|  
|Parole chiave|WFServices|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che il riavvio di un segnalibro non è riuscito.  L'operazione di ricezione memorizzata nel buffer verrà tentata nuovamente quando l'istanza del servizio sarà pronta per l'elaborazione di questa operazione specifica.  
  
## Messaggio  
 Impossibile eseguire l'operazione '%2' nell'istanza del servizio '%1'.  Verrà effettuato un altro tentativo quando l'istanza del servizio è pronta a elaborare questa operazione.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|OperationName|xs:string|Nome dell'operazione.|  
|ServiceInstanceId|xs:string|ID istanza del servizio.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|