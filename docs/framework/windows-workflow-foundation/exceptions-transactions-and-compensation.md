---
title: "Eccezioni, transazioni e compensazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "programmazione [WF], gestione degli errori"
ms.assetid: 694db4f9-7387-4b13-8f9f-b923b18c7490
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Eccezioni, transazioni e compensazione
[!INCLUDE[wf1](../../../includes/wf1-md.md)] offre diversi meccanismi differenti per la gestione di condizioni di errore di runtime nei flussi di lavoro,all'interno dei quali è possibile utilizzare una combinazione di gestori di eccezioni, transazioni, annullamento e compensazione per gestire e risolvere normalmente condizioni di errore.  
  
## In questa sezione  
 [Eccezioni](../../../docs/framework/windows-workflow-foundation//exceptions.md)  
 Viene illustrato come utilizzare l'attività <xref:System.Activities.Statements.TryCatch> per la gestione delle eccezioni in un flusso di lavoro.  
  
 [Transazioni](../../../docs/framework/windows-workflow-foundation//workflow-transactions.md)  
 Viene illustrato come utilizzare l'attività <xref:System.Activities.Statements.TransactionScope> per l'utilizzo delle transazioni in un flusso di lavoro.  
  
 [Compensazione](../../../docs/framework/windows-workflow-foundation//compensation.md)  
 Viene illustrata la compensazione nei flussi di lavoro e viene mostrato come utilizzare le attività di compensazione quali <xref:System.Activities.Statements.CompensableActivity>, <xref:System.Activities.Statements.Compensate> e <xref:System.Activities.Statements.Confirm>.  
  
 [Annullamento](../../../docs/framework/windows-workflow-foundation//modeling-cancellation-behavior-in-workflows.md)  
 Viene descritto come eseguire la gestione dell'annullamento in flussi di lavoro utilizzando attività predefinite e attività personalizzate.  
  
 [Esecuzione del debug dei flussi di lavoro](../../../docs/framework/windows-workflow-foundation//debugging-workflows.md)  
 Viene illustrato come eseguire il debug dei flussi di lavoro.