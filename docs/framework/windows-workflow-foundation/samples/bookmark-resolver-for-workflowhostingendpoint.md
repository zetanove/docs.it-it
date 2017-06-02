---
title: "Risolver di segnalibri per WorkflowHostingEndpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97fd5816-935e-4625-ad04-e6f6befa07de
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Risolver di segnalibri per WorkflowHostingEndpoint
In questo esempio viene illustrato come utilizzare l'oggetto <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> con l'oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost> per creare istanze del flusso di lavoro.  
  
## Dimostrazione  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
## Discussione  
 In questo esempio viene utilizzato <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> per creare istanze del flusso di lavoro ospitate utilizzando <xref:System.ServiceModel.Activities.WorkflowServiceHost>.<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> è un punto di estensibilità per <xref:System.ServiceModel.Activities.WorkflowServiceHost> che può essere utilizzato negli scenari seguenti:  
  
-   Creazione di nuove istanze del flusso di lavoro.  
  
-   Ripresa di segnalibri nell'istanza del flusso di lavoro ospitata in un oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
 L'endpoint di esempio incluso espone un contratto che fornisce operazioni per creare un flusso di lavoro e restituisce l'ID istanza o crea un'istanza con un ID specifico.L'applicazione console di esempio crea un'istanza <xref:System.ServiceModel.Activities.WorkflowServiceHost> con una definizione di flusso di lavoro e aggiunge un oggetto `CreationEndpoint` all'host.Successivamente chiama l'operazione `Create` nell'endpoint per creare una nuova istanza del flusso di lavoro.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Compilare la soluzione.  
  
2.  Eseguire l'applicazione.Nella console `CreationEndpoint` viene visualizzato un messaggio che include l'ID istanza quando viene creata l'istanza del flusso di lavoro.Il messaggio "Hello World\!" viene stampato dall'istanza del flusso di lavoro.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Execution\CreationEndpoint`