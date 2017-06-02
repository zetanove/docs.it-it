---
title: "Criteri semplici | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6a94c834-2e32-4bed-9f47-ae5845eef6ff
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Criteri semplici
In questo esempio viene mostrato come utilizzare un'attività <xref:System.Workflow.Activities.PolicyActivity> in un flusso di lavoro.  
  
 Il flusso di lavoro sequenziale in questo esempio viene creato utilizzando un'attività <xref:System.Workflow.Activities.PolicyActivity>.Il flusso di lavoro definisce campi `orderValue`, `customerType` e `discount` utilizzati per definire un flusso di lavoro di sconto del prodotto.Le regole definite nel file delle regole impostano un valore di sconto basato su `orderValue` e `customerType`.`orderValue` e `customerType` sono impostati nella definizione della classe `SimplePolicyWorkflow` e possono essere modificati per modificarne il comportamento.Lo sconto risultante viene scritto nella console nel gestore eventi <xref:System.Workflow.Runtime.WorkflowRuntime.WorkflowCompleted> definito nella classe `SimplePolicyWorkflow`.  
  
### Per compilare l'esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,  
  
3.  Eseguire la soluzione senza debug premendo CTRL\+F5.  
  
### Per eseguire l’esempio  
  
-   Nella finestra del prompt dei comandi di SDK eseguire il file con estensione exe nella cartella SimplePolicy\\bin\\debug \(oppure nella cartella SimplePolicy\\bin per la versione Visual Basic dell'esempio\), collocata sotto la cartella principale dell'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Rules\Policy\SimplePolicy`  
  
## Vedere anche  
 <xref:System.Workflow.Activities.Rules.RuleSet>   
 <xref:System.Workflow.Activities.PolicyActivity>   
 [Criteri avanzati](../../../../docs/framework/windows-workflow-foundation/samples/advanced-policy.md)