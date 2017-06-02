---
title: "Transazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51212219-a39e-448e-bff3-10064ff5de64
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Transazioni
In questa sezione sono contenuti esempi che illustrano scenari in cui vengono utilizzate transazioni del flusso di lavoro in [!INCLUDE[wf](../../../../includes/wf-md.md)].  
  
## In questa sezione  
 [Eseguire un flusso di lavoro in un oggetto TransactionScope imperativo](../../../../docs/framework/windows-workflow-foundation/samples/execute-a-workflow-in-an-imperative-transactionscope.md)  
 Viene illustrato come eseguire un flusso di lavoro tramite <xref:System.Activities.WorkflowInvoker> in un oggetto <xref:System.Transactions.Transaction> da codice C\# imperativo.  
  
 [Ambito di istruzioni della transazione](../../../../docs/framework/windows-workflow-foundation/samples/transaction-convoy-scope.md)  
 Viene illustrato come creare un modello di attività di messaggistica di una serie di istruzioni parallele insieme a un oggetto <xref:System.ServiceModel.Activities.TransactedReceiveScope> per modellare un protocollo in cui possono verificarsi diverse operazioni in qualsiasi ordine, tutte nella stessa transazione.  
  
 [Rollback di transazioni](../../../../docs/framework/windows-workflow-foundation/samples/transaction-rollback.md)  
 Viene illustrato come creare un oggetto <xref:System.Activities.NativeActivity> personalizzato che accede all'oggetto <xref:System.Activities.RuntimeTransactionHandle> di ambiente per ottenere la transazione di ambiente ed eseguirne il rollback in modo esplicito.  
  
 [Eliminare l'ambito della transazione](../../../../docs/framework/windows-workflow-foundation/samples/suppress-transaction-scope.md)  
 Viene illustrato come creare un'attività `SuppressTransactionScope` personalizzata per eliminare la transazione di runtime di ambiente, se presente.  
  
 [Code transazionali](../../../../docs/framework/windows-workflow-foundation/samples/transacted-queues.md)  
 Viene illustrato come integrare code e transazioni in [!INCLUDE[wf1](../../../../includes/wf1-md.md)] per creare servizi affidabili e scalabili.