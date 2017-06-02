---
title: "Correlazione request/reply | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf4379bf-2d08-43f3-9584-dfa30ffcb1f6
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Correlazione request/reply
La correlazione request\/reply viene usata con una coppia <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> per implementare un'operazione bidirezionale in un servizio flusso di lavoro e con una coppia <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> che richiama un'operazione bidirezionale in un altro servizio Web.  Se si richiama un'operazione bidirezionale in un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], quest'ultimo può essere un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] imperativo tradizionale basato sul codice o un servizio flusso di lavoro.  Per usare la correlazione request\/reply è necessario usare un'associazione bidirezionale, ad esempio <xref:System.ServiceModel.BasicHttpBinding>.  Se si richiama o implementa un'operazione bidirezionale, i passaggi dell'inizializzazione della correlazione sono simili e vengono trattati in questa sezione.  
  
## Utilizzo della correlazione in un'operazione bidirezionale con Receive\/SendReply  
 Una coppia <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> viene usata per implementare un'operazione bidirezionale in un servizio flusso di lavoro.  Il runtime usa la correlazione request\/reply per garantire che la risposta venga inviata al chiamante corretto.  Se un flusso di lavoro viene ospitato mediante <xref:System.ServiceModel.Activities.WorkflowServiceHost>, come nel caso dei servizi flusso di lavoro, è sufficiente l'inizializzazione della correlazione predefinita.  In questo scenario, una coppia <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> viene usata da un flusso di lavoro e non è richiesta alcuna configurazione di correlazione specifica.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
  
```  
  
### Inizializzazione esplicita della correlazione Request\/Reply  
 Se altre operazioni bidirezionali vengono eseguite in parallelo, è necessario configurare la correlazione in modo esplicito.  A tale scopo è possibile specificare un elemento <xref:System.ServiceModel.Activities.CorrelationHandle> e un elemento <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer>o posizionare l'elemento <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> all'interno di un elemento <xref:System.ServiceModel.Activities.CorrelationScope>.  In questo esempio, la correlazione request\-reply viene configurata su una coppia <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply>.  
  
```csharp  
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder",  
    CorrelationInitializers =  
    {  
        new RequestReplyCorrelationInitializer  
        {  
            CorrelationHandle = RRHandle  
        }  
    }  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
 Anziché configurare la correlazione in modo esplicito, è possibile usare un'attività <xref:System.ServiceModel.Activities.CorrelationScope>.  <xref:System.ServiceModel.Activities.CorrelationScope> fornisce un oggetto <xref:System.ServiceModel.Activities.CorrelationHandle> implicito per le attività della messaggistica in esso contenute.  In questo esempio, una coppia <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> è contenuta in un elemento <xref:System.ServiceModel.Activities.CorrelationScope>.  Non è richiesta alcuna configurazione di correlazione esplicita.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
CorrelationScope s = new CorrelationScope  
{  
    Body = new Sequence  
    {  
        Activities =   
        {  
            StartOrder,  
            // Activities that create the reply.  
            ReplyToStartOrder  
        }  
    }  
};  
  
// Construct a workflow using the CorrelationScope.  
```  
  
 Se sono necessarie ulteriori correlazioni, è possibile configurarle usando la proprietà <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> delle rispettive attività di messaggistica mediante i tipi `CorrelationInitializer` desiderati.  
  
## Utilizzo della correlazione in un'operazione bidirezionale con Send\/ReceiveReply  
 Mentre l'attività <xref:System.ServiceModel.Activities.Receive> può essere usata solo in un servizio flusso di lavoro ospitato da <xref:System.ServiceModel.Activities.WorkflowServiceHost>, <xref:System.ServiceModel.Activities.Send>, la coppia <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> può essere usata in qualsiasi flusso di lavoro che deve richiamare un metodo su un servizio Web.  Se il flusso di lavoro è ospitato usando <xref:System.ServiceModel.Activities.WorkflowServiceHost>, viene applicata la correlazione predefinita descritta nella sezione precedente. In caso contrario, è necessario configurare la correlazione in modo esplicito mediante gli elementi <xref:System.ServiceModel.Activities.CorrelationInitializer> e <xref:System.ServiceModel.Activities.CorrelationHandle>oppure tramite la gestione esplicita dell'handle dell'elemento <xref:System.ServiceModel.Activities.CorrelationScope>.  
  
 Se si usa **Aggiungi riferimento al servizio** in un servizio con operazioni bidirezionali, vengono generate attività che eseguono il wrapping di un'attività della coppia <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> a livello interno con la correlazione Request\/Reply specificata in modo esplicito.