---
title: "4209 - TimeoutOpeningSqlConnection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0e56518-9758-41dc-a760-50d1a10fba6e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4209 - TimeoutOpeningSqlConnection
## Proprietà  
  
|||  
|-|-|  
|ID|4209|  
|Parole chiave|WFInstanceStore|  
|Livello|Errore|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che è stato rilevato un timeout durante il tentativo di stabilire una connessione SQL.  
  
## Messaggio  
 Timeout durante il tentativo di aprire una connessione SQL.  Operazione non completata entro il timeout assegnato di %1.  È possibile che la durata consentita per l'operazione fosse una porzione di un timeout più lungo.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Timeout|xs:string|Valore di timeout per l'apertura della connessione SQL.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|