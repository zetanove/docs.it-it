---
title: "1131 - InvokeMethodUseAsyncPattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eca50fa7-5276-4759-ad1c-e490b9bd1f82
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1131 - InvokeMethodUseAsyncPattern
## Proprietà  
  
|||  
|-|-|  
|ID|1131|  
|Parole chiave|WFRuntime|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Durante il passaggio CacheMetadata, l'attività InvokeMethod indica che viene usato il modello asincrono quando viene richiamato il metodo.  
  
## Messaggio  
 InvokeMethod '%1': il metodo usa un modello asincrono di '%2' e '%3'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|InvokeMethod|xs:string|Nome visualizzato dell'attività InvokeMethod.|  
|BeginMethod|xs:string|Nome del metodo Begin.|  
|EndMethod|xs:string|Nome del metodo End.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|