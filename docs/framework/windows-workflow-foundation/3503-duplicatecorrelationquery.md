---
title: "3503 - DuplicateCorrelationQuery | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b857f8e6-ce4d-4da4-bc9d-6cd63fa558a4
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3503 - DuplicateCorrelationQuery
## Proprietà  
  
|||  
|-|-|  
|ID|3503|  
|Parole chiave|WFServices|  
|Livello|Avviso|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che è stato trovato un elemento CorrelationQuery duplicato.  La query duplicata non verrà usata per il calcolo della correlazione.  
  
## Messaggio  
 CorrelationQuery duplicata trovata con Where\='%1'.  La query duplicata non verrà usata per il calcolo della correlazione.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Dove|xs:string|La parte Where della query di correlazione.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|