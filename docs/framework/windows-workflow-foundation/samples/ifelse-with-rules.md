---
title: "IfElse con regole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4ad9bb2-9037-413a-8b14-59ed7b927a9e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# IfElse con regole
In questo esempio viene mostrato l'utilizzo di una condizione della regola con un'attività <xref:System.Workflow.Activities.IfElseActivity>.  
  
 L'esempio passa un parametro `OrderValue` dall'host.Il valore del parametro viene utilizzato in una condizione della regola sul primo ramo dell'attività <xref:System.Workflow.Activities.IfElseActivity>.Se il valore è minore di 10.000, viene eseguito il primo branch e l'attività <xref:System.Workflow.Activities.CodeActivity> nel primo branch stampa **Get Manager Approval** nella console.Se il valore è maggiore di 10.000, viene eseguita l'attività <xref:System.Workflow.Activities.CodeActivity> nel secondo branch e viene stampato **Get VP Approval**.  
  
### Per compilare l'esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,  
  
3.  Eseguire la soluzione senza debug premendo CTRL\+F5.  
  
### Per eseguire l’esempio  
  
-   Nella finestra del prompt dei comandi di SDK eseguire il file con estensione exe nella cartella IfElseWithRules\\bin\\debug \(oppure nella cartella IfElseWithRules\\bin per la versione Visual Basic dell'esempio\), collocata sotto la cartella principale dell'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Rules\IfElseWithRules`  
  
## Vedere anche  
 <xref:System.Workflow.Activities.Rules>   
 <xref:System.Workflow.Activities.IfElseActivity>   
 <xref:System.Workflow.Activities.CodeActivity>   
 <xref:System.Workflow.Activities.Rules.RuleDefinitions>