---
title: "3502 - InferredOperationDescription | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aebb614-3c72-4537-ba11-3cc7200ef1f1
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3502 - InferredOperationDescription
## Proprietà  
  
|||  
|-|-|  
|ID|3502|  
|Parole chiave|WFServices|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Analytic|  
  
## Descrizione  
 Indica che OperationDescription è stato dedotto da WorkflowService.  
  
## Messaggio  
 OperationDescription con Name\= '%1'' nel contratto '%2' dedotta da WorkflowService.  IsOneWay\=%3.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|OperationName|xs:string|Nome dell'operazione.|  
|ContractName|xs:string|Nome del contratto.|  
|IsOneWay|xs:string|True o False che indica se il contratto è unidirezionale.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|