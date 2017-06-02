---
title: "Istruzioni di migrazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cb65c132-58c9-4028-b3d4-1efc71d5e60e
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Istruzioni di migrazione
In [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] viene rilasciata la seconda versione principale di [!INCLUDE[wf](../../../includes/wf-md.md)].[!INCLUDE[wf1](../../../includes/wf1-md.md)] è stato rilasciato in [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] \(inclusi i tipi nei namespace System.Workflow.\*, ora definiti WF3\) e migliorato in [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)].WF3 fa anche parte di [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)], ma è presente insieme alla nuova tecnologia del flusso di lavoro \(i tipi negli spazi dei nomi System.Activities.\*, definiti WF4\).Quando si considera di utilizzare WF4, è importante innanzitutto tenere presente che si sta controllando il tempo.  
  
-   WF3 è una parte integralmente supportata di [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)].  
  
-   Le applicazioni WF3 vengono eseguite in [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] senza alcuna modifica e continuano a essere pienamente supportate.  
  
-   È possibile creare nuove applicazioni WF3, mentre le applicazioni esistenti possono essere modificate in [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] con il pieno supporto.  
  
 Pertanto, la decisione di adottare .NET Framework 4 non dipende dalla scelta di passare da WF3 \(System.Workflow.\*\) a WF4 \(System.Activities.\*\).In questo argomento vengono forniti i collegamenti alle istruzioni di migrazione di WF che contengono informazioni sull'utilizzo di WF3 e WF4.  
  
## Whitepaper e guide di riferimento dettagliate sulla migrazione di WF  
 Nell'argomento [WF Migration Overview](http://go.microsoft.com/fwlink/?LinkId=153873) viene fornita un'ampia panoramica sulla relazione tra WF3 e WF4 e sulle strategie di migrazione.Gli argomenti complementari consentono di esaminare argomenti specifici.  
  
 [WF Migration Overview](http://go.microsoft.com/fwlink/?LinkId=153873)  
 Viene descritta la relazione tra WF3 e WF4 e le scelte che si possono effettuare in qualità di utente effettivo o potenziale della tecnologia del flusso di lavoro in .NET 4.  
  
 [WF Migration: Best Practices for WF3 Development](http://go.microsoft.com/fwlink/?LinkId=153852)  
 Viene descritto come progettare gli elementi WF3 in modo che sia possibile eseguirne facilmente la migrazione a WF4.  
  
 [WF Guidance: Rules](http://go.microsoft.com/fwlink/?LinkId=153854)  
 Viene descritto come visualizzare gli investimenti correlati alle regole nelle soluzioni [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)].  
  
 [WF Guidance: State Machine](http://go.microsoft.com/fwlink/?LinkId=153855)  
 Viene descritta la modellazione del flusso di controllo di WF4 in assenza di un'attività State\-Machine.  
  
 Queste linee guida si applicano solo ai progetti di flusso di lavoro destinati a .NET Framework 4.I flussi di lavoro di macchina a stati sono stati aggiunti in .NET 4.0.1 con la versione Platform Update 1 e sono inclusi come parte di .NET Framework 4.5.[!INCLUDE[crabout](../../../includes/crabout-md.md)]i flusso di lavoro di macchina a stati in .NET 4.0.1 \- 4.0.3 e .NET Framework 4.5, vedere [Update 4.0.1 for Microsoft .NET Framework 4 Features](http://msdn.microsoft.com/it-it/de3297bd-c3e1-4126-95be-2ed7fe2a98fc) e [Flussi di lavoro macchina a stati](../../../docs/framework/windows-workflow-foundation//state-machine-workflows.md).  
  
 [WF Migration Cookbook: Custom Activities](http://go.microsoft.com/fwlink/?LinkId=153856)  
 Vengono forniti esempi e istruzioni per riprogettare le attività personalizzate di WF3 in WF4.  
  
 [Guida di riferimento dettagliata sulla migrazione di WF: attività personalizzate avanzate](http://go.microsoft.com/fwlink/?LinkId=275560)  
 Vengono fornite indicazioni per la riprogettazione delle attività personalizzate avanzate WF3 che utilizzano le code WF3 e pianificano attività figlio come attività personalizzate WF4.  
  
 [WF Migration Cookbook: Workflows](http://go.microsoft.com/fwlink/?LinkId=153858)  
 Vengono forniti esempi e istruzioni per riprogettare i flussi di lavoro di WF3 in WF4.  
  
 [Guida di riferimento dettagliata sulla migrazione di WF: hosting dei flussi di lavoro](http://go.microsoft.com/fwlink/?LinkId=275561)  
 Vengono fornite indicazioni per la riprogettazione del codice di hosting WF3 come codice di hosting WF4.Vengono analizzate le differenze principali dell'hosting di flusso di lavoro tra WF3 e WF4.  
  
 [Guida di riferimento dettagliata sulla migrazione di WF: rilevamento dei flussi di lavoro](http://go.microsoft.com/fwlink/?LinkId=275562)  
 Vengono fornite indicazioni per la riprogettazione della configurazione e del codice di rilevamento WF3 utilizzando una configurazione e un codice di rilevamento WF4 equivalenti.  
  
 [Guida di riferimento dettagliata su WF: servizi di flussi di lavoro](http://go.microsoft.com/fwlink/?LinkId=275564)  
 Vengono fornite istruzioni dettagliate orientate all'esempio per la riprogettazione di flussi di lavoro che implementano i servizi Web Windows Communication Foundation \(WCF\) \(comunemente definiti come servizi di flussi di lavoro\) creati in WF3 per utilizzare WF4, in scenari comuni di attività predefinite.  
  
## Vedere anche  
 <xref:System.Activities.Statements.Interop>