---
title: "Memorizzazione nella cache dei canali con l&#39;attivit&#224; Send | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e69a2502-25cb-43bf-b8d2-95fbdecb41cb
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Memorizzazione nella cache dei canali con l&#39;attivit&#224; Send
L'oggetto <xref:System.ServiceModel.Activities.SendMessageChannelCache> consente agli utenti di disporre di livelli diversi di memorizzazione nella cache di canali con le attività <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.SendParametersContent>.La memorizzazione nella cache a livello di istanza è abilitata per impostazione predefinita e in questo esempio vengono illustrate le seguenti funzionalità:  
  
1.  Condividere un oggetto <xref:System.ServiceModel.Activities.SendMessageChannelCache> in un dominio applicazione.  
  
2.  Disabilitare la memorizzazione nella cache di canali.  
  
3.  Condividere un oggetto <xref:System.ServiceModel.Activities.SendMessageChannelCache> tra istanze del flusso di lavoro in un oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
## Dimostrazione  
 Estensione <xref:System.ServiceModel.Activities.SendMessageChannelCache>, attività <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.ReceiveContent> e <xref:System.ServiceModel.Activities.SendReply>.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Caricare la soluzione del progetto in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e compilare il progetto.  
  
2.  Eseguire l'applicazione EchoWorkflowService generata in \\EchoWorkflowService\\bin\\debug.  
  
3.  Eseguire l'applicazione EchoWorkflowClient generata in\\EchoWorkflowClient\\bin\\debug.  
  
4.  Il client chiama l'operazione Echo nel servizio e stampa i risultati.Una volta stampati i risultati, premere INVIO per uscire dal client e dal servizio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\ChannelCache`