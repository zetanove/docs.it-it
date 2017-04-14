---
title: "Attivit&#224; di runtime in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5ae8c31-19bc-4655-88b3-6b75cd6a1bd5
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivit&#224; di runtime in WF
In [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] sono disponibili diverse attività fornite dal sistema per l'accesso alle funzionalità di esecuzione del flusso di lavoro, ad esempio la persistenza e la chiusura.  
  
|Attività|Descrizione|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.Persist>|Richiede in modo esplicito la persistenza dello stato del flusso di lavoro.|  
|<xref:System.Activities.Statements.TerminateWorkflow>|Termina l'istanza del flusso di lavoro in esecuzione.|  
|<xref:System.Activities.Statements.NoPersistScope>|Attività contenitore che impedisce la persistenza delle attività figlio.|