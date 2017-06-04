---
title: "Utilizzo di variabili con un set di regole di .NET Framework 3.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27b56249-22fe-4252-840f-74c0d6c7a6b3
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Utilizzo di variabili con un set di regole di .NET Framework 3.5
In questo esempio viene illustrato come creare un flusso di lavoro che utilizza l'attività <xref:System.Activities.Statements.Interop> per integrare un'attività personalizzata scritta in [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] che utilizza criteri e regole.I dati vengono passati dal flusso di lavoro all'attività personalizzata associando variabili alle proprietà di dipendenza esposte dall'attività personalizzata.  
  
## Scenario di esempio  
  
#### Per esaminare TravelRuleLibrary  
  
1.  Tramite [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] aprire il file della soluzione InteropWith35RuleSet.sln.  
  
2.  Aprire TravelRuleSet.cs nella finestra di progettazione del flusso di lavoro.  
  
     Viene visualizzata un'attività sequenziale personalizzata che contiene <xref:System.Workflow.Activities.PolicyActivity>.  
  
3.  Fare doppio clic sull'attività dei criteri DiscountPolicy per esaminare le regole  
  
     che possono essere visualizzate nel relativo editor.  
  
4.  Fare clic con il pulsante destro del mouse su `DiscountPolicy` e selezionare l'opzione **Visualizza codice** per esaminare il codice C\# di tipo code\-beside incluso per l'attività.  
  
     Osservare l'impostazione della proprietà di dipendenza per l'oggetto `DiscountLevel`.È equivalente agli argomenti in [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)].[!INCLUDE[crabout](../../../../includes/crabout-md.md)]gli argomenti, vedere [Variabili e argomenti](../../../../docs/framework/windows-workflow-foundation//variables-and-arguments.md).  
  
## InteropWith35RuleSet  
 Si tratta di un progetto di flusso di lavoro sequenziale che utilizza l'attività <xref:System.Activities.Statements.Interop> per eseguire l'integrazione con il set di regole personalizzato creato nel progetto `TravelRuleLibrary`.Le variabili vengono create nell'attività <xref:System.Activities.Statements.Sequence> di primo livello.L'attività <xref:System.Activities.Statements.Interop> viene utilizzata per eseguire l'integrazione con l'attività `TravelRuleSet`.Le variabili dichiarate nell'oggetto <xref:System.Activities.Statements.Sequence> vengono utilizzate per eseguire l'associazione alle proprietà di dipendenza.  
  
## Per utilizzare questo esempio  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione InteropWith35RuleSet.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\InteropWith35RuleSet`  
  
## Vedere anche