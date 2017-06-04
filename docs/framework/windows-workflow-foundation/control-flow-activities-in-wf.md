---
title: "Attivit&#224; del flusso di controllo in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6892885b-f7c5-4aea-8f5e-28863fb4ae75
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Attivit&#224; del flusso di controllo in WF
In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] sono disponibili numerose attività per il controllo del flusso di esecuzione all'interno di un flusso di lavoro.Alcune di queste attività \(ad esempio `Switch` e `If`\) implementano strutture di controllo del flusso simili a quelle degli ambienti di programmazione come [!INCLUDE[csprcs](../../../includes/csprcs-md.md)], mentre altre \(ad esempio `Pick`\) modellano nuove strutture di programmazione.  
  
 Si noti che mentre le attività quali `Parallel` e `ParallelForEach` pianificano l'esecuzione di più attività figlio contemporaneamente, per un flusso di lavoro viene utilizzato un solo thread.Ogni attività figlio di queste attività viene eseguita in sequenza e le attività successive non vengono eseguite fino a quando le attività precedenti non vengono completate o non diventano inattive.Di conseguenza, queste attività sono molto utili per applicazioni nelle quali diverse attività potenzialmente di blocco devono essere eseguite in un modo caratterizzato da interfoliazione.Se nessuna delle attività figlio di queste attività diventa inattiva, un'attività `Parallel` viene eseguita come un'attività `Sequence` e un'attività `ParallelForEach` viene eseguita come un'attività `ForEach`.Se, tuttavia, vengono utilizzate attività asincrone \(come le attività che derivano da <xref:System.Activities.AsyncCodeActivity>\) o attività di messaggistica, il controllo passa al branch successivo mentre l'attività figlio attende la ricezione del messaggio o il completamento del relativo lavoro asincrono.  
  
## Attività di controllo del flusso  
  
|Attività|Descrizione|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.DoWhile>|Esegue una volta le attività contenute e continua mentre una condizione è `true`.|  
|<xref:System.Activities.Statements.ForEach%601>|Esegue un'istruzione incorporata in sequenza per ogni elemento in una raccolta.<xref:System.Activities.Statements.ForEach%601> è simile alla parola chiave `foreach`, ma viene implementata come attività anziché come istruzione di linguaggio.|  
|<xref:System.Activities.Statements.If>|Esegue le attività contenute se una condizione è `true` e può eseguire attività contenute nella proprietà <xref:System.Activities.Statements.If.Else%2A> se la condizione è `false`.|  
|<xref:System.Activities.Statements.Parallel>|Esegue attività contenute in parallelo.|  
|<xref:System.Activities.Statements.ParallelForEach%601>|Esegue un'istruzione incorporata in parallelo per ogni elemento in una raccolta.|  
|<xref:System.Activities.Statements.Pick>|Fornisce modellazione del flusso di controllo basato sull'evento.|  
|<xref:System.Activities.Statements.PickBranch>|Rappresenta un percorso potenziale di esecuzione in un'attività <xref:System.Activities.Statements.Pick>.|  
|<xref:System.Activities.Statements.Sequence>|Esegue attività contenute in sequenza.|  
|<xref:System.Activities.Statements.Switch%601>|Seleziona una scelta da un numero di attività da eseguire, in base al valore di una determinata espressione.|  
|<xref:System.Activities.Statements.While>|Esegue le attività contenute mentre una condizione è `true`.|