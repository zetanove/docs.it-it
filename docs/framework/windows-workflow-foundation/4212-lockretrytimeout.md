---
title: "4212 - LockRetryTimeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d4ad415a-9871-49fc-85b8-8ee2ea149b1d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4212 - LockRetryTimeout
## Proprietà  
  
|||  
|-|-|  
|ID|4212|  
|Parole chiave|WFInstanceStore|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Timeout rilevato del provider SQL durante il tentativo di acquisire il blocco di istanza.  
  
## Messaggio  
 Timeout durante il tentativo di acquisire il blocco di istanza. Operazione non completata entro il timeout assegnato di %1.  È possibile che la durata consentita per l'operazione fosse una porzione di un timeout più lungo.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Delay|xs:string|Il ritardo tra i tentativi.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|