---
title: "Esercitazione introduttiva [.NET Framework 4.5] | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WF [WF], introduzione"
  - "Windows Workflow Foundation [WF], introduzione"
ms.assetid: c2d3585f-6b1a-4d4f-9865-bd7cd31c5d42
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Esercitazione introduttiva [.NET Framework 4.5]
In questa sezione è contenuto un set di argomenti di procedure dettagliate che introducono alla programmazione di applicazioni [!INCLUDE[wf](../../../includes/wf-md.md)].Seguendo le procedure di questi argomenti, verrà compilata un'applicazione che è un gioco per determinare un numero.Nel primo argomento dell'esercitazione vengono descritti i passaggi per creare le attività personalizzate richieste per il flusso di lavoro.Nel secondo argomento, queste attività vengono assemblate in un flusso di lavoro del diagramma di flusso insieme alle attività incorporate del flusso di lavoro.Nel terzo argomento, l'applicazione host viene configurata in modo da eseguire il flusso di lavoro e nell'ultimo argomento viene introdotta la persistenza.Ogni passaggio in questo processo dipende dai passaggi precedenti, pertanto si consiglia di completarli in ordine.  
  
## In questa sezione  
 [Procedura: creare un'attività](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md)  
 Viene descritto come creare un'attività personalizzata che deriva dall'oggetto <xref:System.Activities.NativeActivity%601> e come comporre questa attività insieme a un'attività incorporata in un'attività composita tramite l'ActivityDesigner.  
  
 [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)  
 Viene descritto come creare flussi di lavoro di diagramma di flusso, sequenziali e di macchina a stati tramite le attività predefinite e le attività personalizzate dall'esercitazione precedente.  
  
 [Procedura: eseguire un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md)  
 Viene descritto come richiamare un flusso di lavoro da un ambiente host, come passare i dati all'interno e all'esterno di un flusso di lavoro e come riprendere i segnalibri.  
  
 [Procedura: creare ed eseguire un flusso di lavoro con esecuzione prolungata](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md)  
 Viene descritto come aggiungere la persistenza a un'applicazione flusso di lavoro.  
  
 [Procedura: creare un partecipante del rilevamento personalizzato](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md)  
 Viene descritto come creare un partecipante del rilevamento personalizzato e un profilo di rilevamento.  
  
 [Procedura: ospitare più versioni di un flusso di lavoro side\-by\-side](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md)  
 Viene descritto come utilizzare `WorkflowIdentity` per ospitare più versioni di un flusso di lavoro side\-by\-side.  
  
 [Procedura: aggiornare la definizione di un'istanza del flusso di lavoro in esecuzione](../../../docs/framework/windows-workflow-foundation//how-to-update-the-definition-of-a-running-workflow-instance.md)  
 Viene descritto come utilizzare l'aggiornamento dinamico per modificare le istanze in esecuzione del flusso di lavoro.  
  
## Vedere anche  
 [Programmazione di Windows Workflow Foundation](../../../docs/framework/windows-workflow-foundation//programming.md)