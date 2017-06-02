---
title: "Utilizzo di base delle attivit&#224; SendParameters e ReceiveParameters | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b6b1681-3d41-403f-bfe2-3f600f24aa8c
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Utilizzo di base delle attivit&#224; SendParameters e ReceiveParameters
Nell'esempio seguente viene illustrato l'utilizzo delle attività <xref:System.ServiceModel.Activities.SendParametersContent> e <xref:System.ServiceModel.Activities.ReceiveParametersContent>.Il servizio espone un'operazione che accetta un argomento di tipo stringa e restituisce l'input al client.Nell'esempio viene illustrato come configurare i parametri per queste attività di messaggistica.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\SendReceiveParameters`  
  
#### Utilizzo dell'esempio  
  
1.  Caricare la soluzione del progetto in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e compilare il progetto.  
  
2.  Eseguire innanzitutto l'applicazione EchoWorkflowService, generata in \[directory soluzione di base\]\\EchoWorkflowService\\bin\\debug.  
  
3.  In secondo luogo eseguire l'applicazione EchoWorkflowClient generata in \[directory soluzione di base\]\\EchoWorkflowClient\\bin\\debug.  
  
4.  Il client chiama l'operazione Echo nel servizio e stampa i risultati.Al termine premere INVIO per uscire dal client e quindi dal servizio.  
  
## Vedere anche