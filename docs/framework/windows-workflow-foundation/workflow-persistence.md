---
title: "Persistenza del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "programmazione [WF], persistenza"
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Persistenza del flusso di lavoro
La persistenza del flusso di lavoro è l'acquisizione durevole di uno stato di un'istanza del flusso di lavoro, indipendentemente dalle informazioni relative al processo o al computer.In questo modo viene fornito un punto noto di ripristino dell'istanza del flusso di lavoro in caso di errore di sistema o viene conservata memoria scaricando istanze del flusso di lavoro il cui funzionamento non viene eseguito in modo attivo o ancora viene spostato lo stato dell'istanza del flusso di lavoro da un nodo a un altro in una server farm.  
  
 La persistenza abilita agilità di processo, scalabilità, ripristino nonostante errori e la possibilità di gestire la memoria in modo più efficiente.Il processo di persistenza include l'identificazione di un punto di persistenza, la raccolta dei dati da salvare e infine la delega dell'archiviazione effettiva dei dati a un provider di persistenza.  
  
 Per abilitare la persistenza di un flusso di lavoro, è necessario associare un archivio di istanze all'oggetto **WorkflowApplication** o all'oggetto **WorkflowServiceHost** come menzionato in [Procedura: abilitare la persistenza per i flussi di lavoro e i relativi servizi](../../../docs/framework/windows-workflow-foundation//how-to-enable-persistence-for-workflows-and-workflow-services.md).Gli oggetti **WorkflowApplication** e **WorkflowServiceHost** utilizzano il relativo archivio di istanze associato per abilitare la persistenza delle istanze del flusso di lavoro in un archivio di persistenza e il carico delle istanze del flusso di lavoro in memoria in base ai dati dell'istanza del flusso di lavoro archiviati nell'archivio di persistenza.  
  
 In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] è disponibile la classe **SqlWorkflowInstanceStore** che consente la persistenza di dati e metadati relativamente alle istanze del flusso di lavoro in un database di SQL Server 2005 o di SQL Server 2008.Per ulteriori informazioni, vedere [Archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).  
  
 Per archiviare e caricare i dati specifici dell'applicazione insieme alle informazioni correlate all'istanza del flusso di lavoro, è possibile creare partecipanti di persistenza che estendono la classe <xref:System.Activities.Persistence.PersistenceParticipant>.Un partecipante di persistenza fa parte del processo di persistenza per salvare dati serializzabili personalizzati nell'archivio di persistenza, per caricare i dati dall'archivio di istanze in memoria ed eseguire qualsiasi logica aggiuntiva in una transazione di persistenza.Per ulteriori informazioni, vedere [Partecipanti di persistenza](../../../docs/framework/windows-workflow-foundation//persistence-participants.md).  
  
 Windows Server AppFabric semplifica il processo di configurazione della persistenza.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Concetti di persistenza con Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201200)  
  
## Punti di persistenza impliciti  
 Nell'elenco seguente sono contenuti esempi di condizioni in base alle quali un flusso di lavoro viene reso persistente quando un archivio di istanze è associato a un flusso di lavoro.  
  
-   Quando un'attività **TransactionScope** o un'attività **TransactedReceiveScope** viene completata.  
  
-   Quando un'istanza del flusso di lavoro diventa inattiva e **WorkflowIdleBehavior** viene impostato sull'host del flusso di lavoro.Questa situazione si verifica, ad esempio, quando si utilizzano attività di messaggistica o un'attività **Delay**.  
  
-   Quando WorkflowApplication diventa inattivo e la proprietà **PersistableIdle** dell'applicazione viene impostata su **PersistableIdleAction.Persist**.  
  
-   Quando a un'applicazione host viene richiesto di rendere persistente o scaricare un'istanza del flusso di lavoro.  
  
-   Quando un'istanza del flusso di lavoro viene terminata o finisce.  
  
-   Quando viene eseguita un'attività **Persist**.  
  
-   Quando un'istanza di un flusso di lavoro sviluppata utilizzando una versione precedente di Windows Workflow Foundation incontra un punto di persistenza durante l'esecuzione interoperativa.  
  
## In questa sezione  
  
-   [Archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md)  
  
-   [Archivio di istanze](../../../docs/framework/windows-workflow-foundation//instance-stores.md)  
  
-   [Partecipanti di persistenza](../../../docs/framework/windows-workflow-foundation//persistence-participants.md)  
  
-   [Procedure consigliate per la persistenza](../../../docs/framework/windows-workflow-foundation//persistence-best-practices.md)  
  
-   [Istanze del flusso di lavoro non persistenti](../../../docs/framework/windows-workflow-foundation//non-persisted-workflow-instances.md)  
  
-   [Sospensione e ripresa di un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//pausing-and-resuming-a-workflow.md)