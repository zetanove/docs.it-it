---
title: "1148 - FlowchartSwitchCaseNotFound | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9ee7fcee-e040-4306-968e-ed840a1cb00c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 1148 - FlowchartSwitchCaseNotFound
## Proprietà  
  
|||  
|-|-|  
|ID|1148|  
|Parole chiave|WFActivities|  
|Livello|Informazioni|  
|Canale|Microsoft\-Windows\-Application Server\-Applications\/Debug|  
  
## Descrizione  
 Indica che non è stato trovato un case corrispondente o un case predefinito in un'opzione diagramma di flusso.  L'esecuzione del diagramma di flusso terminerà.  
  
## Messaggio  
 Diagramma di flusso '%1'\/FlowSwitch: impossibile trovare un'attività Case o un case predefinito corrispondente al risultato dell'espressione.  L'esecuzione del diagramma di flusso terminerà.  
  
## Dettagli  
  
|Nome elemento dati|Tipo elemento dati|Descrizione|  
|------------------------|------------------------|-----------------|  
|Diagramma di flusso|xs:string|Nome visualizzato del diagramma di flusso.|  
|AppDomain|xs:string|Stringa restituita da AppDomain.CurrentDomain.FriendlyName.|