---
title: "Attivit&#224; della macchina a stati in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 93312eaf-07e0-4a55-b4f7-4cdbbc4dee2d
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Attivit&#224; della macchina a stati in WF
In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono disponibili numerose attività fornite dal sistema e ActivityDesigner per la creazione di flussi di lavoro di macchine a stati.  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.StateMachine>|Esegue attività contenute utilizzando il comune paradigma della macchina a stati.|  
|<xref:System.Activities.Statements.State>|Rappresenta uno stato in una macchina a stati.|  
|<xref:System.Activities.Core.Presentation.FinalState>|Rappresenta uno stato di chiusura in una macchina a stati.<xref:System.Activities.Core.Presentation.FinalState> è un ActivityDesigner che, quando utilizzato, crea un elemento <xref:System.Activities.Statements.State> preconfigurato come stato di chiusura.Per ulteriori informazioni, vedere [ActivityDesigner FinalState](../Topic/FinalState%20Activity%20Designer.md).|  
|<xref:System.Activities.Statements.Transition>|Rappresenta la transizione tra due stati.Non esiste un elemento nella **Casella degli strumenti** per <xref:System.Activities.Statements.Transition>; le transizioni vengono create nella finestra di progettazione del flusso di lavoro trascinando e rilasciando una linea tra due stati o rilasciando uno stato sui triangoli visualizzati quando uno stato viene passato sopra un altro stato.Per ulteriori informazioni, vedere [ActivityDesigner Transition](../Topic/Transition%20Activity%20Designer.md).|  
  
## Vedere anche  
 [Esercitazione introduttiva](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)