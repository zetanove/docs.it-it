---
title: "Invio e gestione di errori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98e8e04d-2ac9-4a33-ae08-462f757a7a14
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Invio e gestione di errori
In questo esempio viene illustrato come utilizzare le attività di messaggistica <xref:System.ServiceModel.Activities.SendReply> e <xref:System.ServiceModel.Activities.ReceiveReply> per inviare e ricevere errori previsti e imprevisti.In questo scenario, la prima richiesta del client comporta un errore previsto incluso nella raccolta <xref:System.ServiceModel.Activities.Send.KnownTypes%2A>.Le successive richieste del client comportano la ricezione di errori imprevisti, prima del completamento della richiesta finale.  
  
## Per utilizzare questo esempio  
  
1.  Aprire [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] con autorizzazioni elevate facendo clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e scegliendo **Esegui come amministratore**.  
  
2.  Aprire il file della soluzione Faults.sln.  
  
3.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
4.  Eseguire il progetto del servizio.  
  
    1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto `FaultService` e selezionare **Imposta come progetto di avvio**.  
  
    2.  Premere CTRL\+F5.  
  
5.  Aprire un'altra copia di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] con autorizzazioni elevate facendo clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e scegliendo **Esegui come amministratore**.  
  
6.  Aprire il file della soluzione Faults.sln.  
  
7.  Eseguire il progetto del client.  
  
    1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto `FaultClient` e scegliere **Imposta come progetto di avvio**.  
  
    2.  Premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\Faults`  
  
## Vedere anche