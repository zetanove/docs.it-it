---
title: "Elaborazione di messaggi nell&#39;ordine non corretto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33fc62a5-5d59-461c-a37a-0e1b51ac763d
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Elaborazione di messaggi nell&#39;ordine non corretto
I servizi flusso di lavoro possono dipendere da messaggi inviati in un ordine specifico.Un servizio flusso di lavoro contiene una o più attività <xref:System.ServiceModel.Activities.Receive> e ogni attività <xref:System.ServiceModel.Activities.Receive> attende un messaggio specifico.Senza particolari garanzie di recapito di trasporto, i messaggi inviati dai client possono essere differiti e pertanto recapitati in un ordine inatteso dal servizio flusso di lavoro.L'implementazione di un servizio flusso di lavoro che non richiede l'invio di messaggi in un ordine specifico viene in genere effettuata mediante un'attività Parallel.Per un protocollo dell'applicazione più complicato, il flusso di lavoro diverrebbe rapidamente molto complesso.La funzionalità di elaborazione di messaggi nell'ordine non corretto in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di creare un flusso di lavoro simile senza la complessità derivante dalle attività Parallel annidate.L'elaborazione di messaggi nell'ordine non corretto è supportata solo in canali che supportano <xref:System.ServiceModel.Channele.ReceiveContext>, ad esempio le associazioni MSMQ di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Abilitazione dell'elaborazione di messaggi nell'ordine non corretto  
 L'elaborazione dei messaggi nell'ordine non corretto viene abilitata impostando la proprietà <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> su `true` in WorkflowService.Nell'esempio riportato di seguito viene illustrato come impostare la proprietà <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> nel codice.  
  
```csharp  
// Code: Opt-in to Buffered Receive processing...  
WorkflowService service = new WorkflowService  
{  
    Name="MyService",  
    Body = workflow,  
    AllowBufferedReceive = true  
};  
  
```  
  
 È inoltre possibile applicare l'attributo `AllowBufferedReceive` a un servizio flusso di lavoro in XAML, come indicato nell'esempio seguente.  
  
```xaml  
// Xaml: Opt-in to Buffered Receive processing...  
<WorkflowService AllowBufferedReceive="True">  
   <!—the actual children activities -->  
</Sequence>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.ReceiveContext>   
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Code e sessioni affidabili](../../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md)