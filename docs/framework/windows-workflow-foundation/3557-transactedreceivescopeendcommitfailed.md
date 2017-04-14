---
title: "3557 - TransactedReceiveScopeEndCommitFailed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 079f0188-8146-49ee-b6ae-a08f4e4d2b9b
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3557 - TransactedReceiveScopeEndCommitFailed
## Proprietà  
  
|||  
|-|-|  
|ID|3557|  
|Parole chiave|WFServices|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che la chiamata a EndCommit in CommittableTransaction ha generato TransactionException.  
  
## Messaggio  
 La chiamata a EndCommit in CommittableTransaction con ID \= '%1' ha generato TransactionException con il messaggio seguente: '%2'.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|TransactionId|xs:string|ID della transazione di cui eseguire il commit.|  
|Eccezione|xs:string|Dettagli dell'eccezione.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|