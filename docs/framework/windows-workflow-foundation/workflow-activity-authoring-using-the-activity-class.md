---
title: "Creazione di attivit&#224; del flusso di lavoro tramite la classe Activity | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b7b1c66-f093-43c3-b4d1-7173b46516da
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Creazione di attivit&#224; del flusso di lavoro tramite la classe Activity
Il modo più semplice per creare un'attività utilizzando [!INCLUDE[wf](../../../includes/wf-md.md)] in [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] consiste nel creare una classe che eredita dall'oggetto <xref:System.Activities.Activity> che crea la funzionalità assemblando attività o attività personalizzate dall'oggetto [Libreria attività incorporata](../../../docs/framework/windows-workflow-foundation//net-framework-4-5-built-in-activity-library.md).In questo argomento viene illustrato come creare un'attività che consente di scrivere due messaggi nella console.  
  
### Per creare un'attività personalizzata utilizzando ActivityDesigner  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)].  
  
2.  Scegliere File, Nuovo, Progetto.Selezionare **Workflow 4.0** sotto **Visual C\#** nella finestra **Tipi progetto** e scegliere il nodo **v2010**.Selezionare **Libreria attività**  nella finestra **Modelli**.Assegnare al nuovo progetto il nome HelloActivity.  
  
3.  Aprire la nuova attività.Trascinare un'attività <xref:System.Activities.Statements.Sequence> dalla casella degli strumenti nell'area di progettazione.  
  
4.  Trascinare un'attività <xref:System.Activities.Statements.WriteLine> nell'attività <xref:System.Activities.Statements.Sequence>.Immettere `"Hello World"` \(con le virgolette\) nel campo **Testo**.  
  
5.  Trascinare una seconda attività <xref:System.Activities.Statements.WriteLine> nell'attività <xref:System.Activities.Statements.Sequence>, al di sotto della prima.Immettere `"Goodbye"` \(con le virgolette\) nel campo **Testo**.