---
title: "Attivit&#224; di transazione in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb33378e-82c6-4ea0-870f-76dc77e7f0fe
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attivit&#224; di transazione in WF
In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] sono disponibili numerose attività fornite dal sistema per la modellazione delle transazioni, la compensazione e l'annullamento.Questi modelli di programmazione consentono al flusso di lavoro di proseguire esecuzione nel caso di modifiche nella logica aziendale e durante la gestione degli errori.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lle transazioni, la compensazione e l'annullamento, vedere [Transazioni](../../../docs/framework/windows-workflow-foundation//workflow-transactions.md), [Compensazione](../../../docs/framework/windows-workflow-foundation//compensation.md) e [Annullamento](../../../docs/framework/windows-workflow-foundation//modeling-cancellation-behavior-in-workflows.md).  
  
## Attività di transazione  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.CancellationScope>|Associa la logica di annullamento, sotto forma di un'attività, a un percorso principale di esecuzione, anch'esso espresso come attività.|  
|<xref:System.Activities.Statements.CompensableActivity>|Supporta la compensazione delle relative attività figlio.|  
|<xref:System.Activities.Statements.Compensate>|Richiama in modo esplicito il gestore compensazione di un oggetto <xref:System.Activities.Statements.CompensableActivity>.|  
|<xref:System.Activities.Statements.Confirm>|Richiama in modo esplicito il gestore conferma di un oggetto <xref:System.Activities.Statements.CompensableActivity>.|  
|<xref:System.Activities.Statements.TransactionScope>|Demarca un limite della transazione.|  
|<xref:System.ServiceModel.Activities.TransactedReceiveScope>|Ambito della durata di una transazione iniziata da un messaggio ricevuto.È possibile che la transazione sia propagata nel flusso di lavoro al messaggio di avvio o venga creata dal dispatcher alla ricezione del messaggio. **Note:**  L'oggetto <xref:System.ServiceModel.Activities.TransactedReceiveScope> si trova nella sezione **Messaggistica** della **Casella degli strumenti**.|