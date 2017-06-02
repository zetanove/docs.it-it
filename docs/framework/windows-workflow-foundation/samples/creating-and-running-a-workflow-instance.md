---
title: "Creazione ed esecuzione di un&#39;istanza del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19d27f47-0491-4569-8f53-51bc1d940e80
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Creazione ed esecuzione di un&#39;istanza del flusso di lavoro
In questo esempio viene illustrato come eseguire un'istanza del flusso di lavoro,sia in modo sincrono che asincrono.  
  
## Dimostrazione  
 <xref:System.Activities.WorkflowInvoker>, <xref:System.Activities.WorkflowApplication>.  
  
## Discussione  
 Nella prima parte dell'esempio viene utilizzato <xref:System.Activities.WorkflowInvoker.Invoke%2A>.Si tratta della modalità di base per eseguire un flusso di lavoro.I flussi di lavoro eseguiti con <xref:System.Activities.WorkflowInvoker.Invoke%2A> possono esserlo solo in modo sincrono.  
  
 Nella seconda parte dell'esempio viene utilizzata la classe <xref:System.Activities.WorkflowApplication>.<xref:System.Activities.WorkflowApplication> consente un maggiore controllo su ogni istanza, inclusa la possibilità di interagire con il flusso di lavoro in esecuzione ed eseguirlo in modo asincrono.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Execution\CreatingWorkflowInstances`  
  
## Vedere anche  
 [Utilizzo di WorkflowInvoker e WorkflowApplication](../../../../docs/framework/windows-workflow-foundation//using-workflowinvoker-and-workflowapplication.md)