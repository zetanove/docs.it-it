---
title: "Flussi di lavoro procedurali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52401de9-9115-472d-8fd9-047af6a072b9
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Flussi di lavoro procedurali
Nei flussi di lavoro procedurali vengono utilizzati metodi di controllo del flusso simili a quelli dei linguaggi procedurali.Tra questi costrutti sono inclusi `While` e `If`.Questi flussi di lavoro possono essere creati liberamente utilizzando altre attività di controllo del flusso quale <xref:System.Activities.Statements.Flowchart> e <xref:System.Activities.Statements.Sequence>.  
  
## Controllo del flusso di esecuzione  
 La libreria di attività del flusso di lavoro dispone di attività per modellare la maggior parte dei metodi di controllo del flusso utilizzati nei linguaggi procedurali,tra cui:  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.DoWhile>  
  
-   <xref:System.Activities.Statements.ForEach>  
  
-   <xref:System.Activities.Statements.Parallel>  
  
-   <xref:System.Activities.Statements.ParallelForEach>  
  
-   <xref:System.Activities.Statements.If>  
  
-   <xref:System.Activities.Statements.Switch>  
  
-   <xref:System.Activities.Statements.Pick>  
  
 Per utilizzare le attività di controllo del flusso, trascinarle dalla casella degli strumenti **Attività** in un'attività composta nella finestra di progettazione.  
  
> [!NOTE]
>  Se si utilizza [!INCLUDE[dublin](../../../includes/dublin-md.md)] per ospitare i flussi di lavoro in una Web farm, le istanze verranno spostate da AppFabric tra server di AppFabric differenti.È necessario quindi che le risorse possano essere condivise tra tutti i nodi.Nessuna delle attività predefinite del flusso di lavoro di .NET 4 contiene operazioni di accesso alle risorse locali.Poiché AppFabric non offre alcun meccanismo per contrassegnare un flusso di lavoro come non spostabile, uno sviluppatore non deve creare attività personalizzate che non vengono eseguite correttamente quando un flusso di lavoro viene spostato.  
  
## Vedere anche  
 [Flussi di lavoro del diagramma di flusso](../../../docs/framework/windows-workflow-foundation//flowchart-workflows.md)