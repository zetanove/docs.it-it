---
title: "Attivazione di istanze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 134c3f70-5d4e-46d0-9d49-469a6643edd8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Attivazione di istanze
L'archivio di istanze del flusso di lavoro SQL esegue un'attività interna che attiva e rileva periodicamente istanze del flusso di lavoro eseguibili o attivabili nel database di persistenza.Se rileva un'istanza del flusso di lavoro eseguibile, notifica all'host del flusso di lavoro la possibilità di attivare l'istanza.Se l'archivio di istanze rileva un'istanza del flusso di lavoro attivabile, invia una notifica a un host generico che attiva un host del flusso di lavoro il quale, a sua volta, esegue l'istanza del flusso di lavoro.Nelle sezioni seguenti di questo argomento viene illustrato dettagliatamente il processo di attivazione delle istanze.  
  
##  <a name="RunnableSection"></a> Rilevamento e attivazione di istanze del flusso di lavoro eseguibili  
 L'archivio di istanze del flusso di lavoro SQL considera un'istanza del flusso di lavoro *eseguibile* se lo stato dell'istanza non è Suspended o Completed e soddisfa le condizioni seguenti:  
  
-   L'istanza è sbloccata e dispone di un timer in sospeso scaduto.  
  
-   Nell'istanza è presente un blocco scaduto.  
  
-   L'istanza è sbloccata e il relativo stato è **Executing**.  
  
 L'archivio di istanze del flusso di lavoro SQL genera l'oggetto <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> quando rileva un'istanza eseguibile.Successivamente, l'oggetto SqlWorkflowInstanceStore arresta il monitoraggio finché l'oggetto <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand> non viene chiamato una volta sull'archivio.  
  
 Un host del flusso di lavoro che ha sottoscritto l'oggetto <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> ed è in grado di caricare l'istanza, esegue l'oggetto <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand> sull'archivio di istanze per caricare l'istanza in memoria.Un host del flusso di lavoro viene considerato capace di caricare un'istanza del flusso di lavoro se la proprietà dei metadati **WorkflowServiceType** dell'host e dell'istanza è impostata sullo stesso valore.  
  
## Rilevamento e attivazione di istanze del flusso di lavoro attivabili  
 Un'istanza del flusso di lavoro viene considerata *attivabile* se è eseguibile e nessun host del flusso di lavoro è in grado di caricare l'istanza in esecuzione nel computer.Vedere la sezione precedente Rilevamento e attivazione di istanze del flusso di lavoro eseguibili per la definizione di un'istanza del flusso di lavoro eseguibile.  
  
 L'archivio di istanze del flusso di lavoro SQL genera l'oggetto <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> quando rileva un'istanza del flusso di lavoro eseguibile nel database.Successivamente, l'oggetto SqlWorkflowInstanceStore arresta il monitoraggio finché l'oggetto <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> non viene chiamato una volta sull'archivio.  
  
 Quando un host generico che ha sottoscritto l'oggetto <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> riceve l'evento, esegue l'oggetto <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> sull'archivio di istanze per ottenere i parametri di attivazione necessari per creare un host del flusso di lavoro.L'host generico utilizza questi parametri di attivazione per creare un host del flusso di lavoro che, a sua volta, carica ed esegue l'istanza del servizio eseguibile.  
  
## Host generici  
 Si definisce generico un host il cui valore della proprietà dei metadati **WorkflowServiceType** per gli host generici è impostato su **WorkflowServiceType.Any** per indicare che può gestire qualsiasi tipo di flusso di lavoro.Un host generico dispone di un parametro XName denominato **ActivationType**.  
  
 L'archivio di istanze del flusso di lavoro SQL supporta attualmente host generici con il valore del parametro ActivationType impostato su **WAS**.Se il parametro ActivationType non è impostato su WAS, l'archivio di istanze del flusso di lavoro SQL genera un'eccezione <xref:System.Runtime.DurableInstancing.InstancePersistenceException>.Il Servizio di gestione flussi di lavoro fornito con [!INCLUDE[dublin](../../../includes/dublin-md.md)] è un host generico il cui tipo di attivazione è impostato su **WAS**.  
  
 Per l'attivazione di WAS, un host generico richiede un set di parametri di attivazione per derivare l'indirizzo dell'endpoint in cui possono essere attivati nuovi host.I parametri per l'attivazione di WAS sono: nome del sito, percorso dell'applicazione relativa al sito e percorso del servizio relativo all'applicazione.L'archivio di istanze del flusso di lavoro SQL archivia questi parametri di attivazione durante l'esecuzione dell'oggetto <xref:System.Activities.DurableInstancing.SaveWorkflowCommand>.  
  
## Runnable Instances Detection Period  
 La proprietà **Runnable Instances Detection Period** dell'archivio di istanze del flusso di lavoro SQL specifica il periodo di tempo dopo cui l'archivio di istanze del flusso di lavoro SQL esegue un'attività di rilevamento per individuare eventuali istanze del flusso di lavoro eseguibili o attivabili nel database di persistenza dopo il ciclo di rilevamento precedente.Per ulteriori informazioni su questa proprietà, vedere [Runnable Instances Detection Period](../../../docs/framework/windows-workflow-foundation//runnable-instances-detection-period.md).