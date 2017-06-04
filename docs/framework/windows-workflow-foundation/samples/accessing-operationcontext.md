---
title: "Accesso a OperationContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e92efe8-7e79-41f3-b50e-bdc38b9f41f8
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Accesso a OperationContext
In questo esempio viene illustrato come le attività di messaggistica \(<xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.Send>\) possono essere utilizzate con un'attività di ambiti personalizzata per accedere a <xref:System.ServiceModel.OperationContext.Current%2A> e allegare o recuperare un'intestazione di messaggio personalizzata all'interno di un messaggio in uscita o in ingresso.  
  
## Dimostrazione  
 Attività di messaggistica, <xref:System.ServiceModel.Activities.ISendMessageCallback>, <xref:System.ServiceModel.Activities.IReceiveMessageCallback>.  
  
## Discussione  
 In questo esempio viene illustrato come utilizzare punti di estensibilità \(<xref:System.ServiceModel.Activities.ISendMessageCallback>\) <xref:System.ServiceModel.Activities.IReceiveMessageCallback>\) nelle attività di messaggistica per accedere a <xref:System.ServiceModel.OperationContext.Current%2A>.I callback vengono registrati all'interno dell'esecuzione del flusso di lavoro come un'implementazione di <xref:System.Activities.IExecutionProperty> raccolta dalle attività della messaggistica durante l'esecuzione.Qualsiasi attività di messaggistica nello stesso ambito di tale implementazione <xref:System.Activities.IExecutionProperty> risulta interessata.In particolare, questo esempio utilizza un'attività di ambiti personalizzata per applicare il comportamento di callback.<xref:System.ServiceModel.Activities.ISendMessageCallback> viene utilizzato nel flusso di lavoro client per includere l'oggetto <xref:System.Activities.WorkflowApplication.Id%2A> del flusso di lavoro come <xref:System.ServiceModel.Channels.MessageHeader> in uscita.Questa intestazione viene quindi scelta nel servizio utilizzando <xref:System.ServiceModel.Activities.IReceiveMessageCallback> e il valore dell'intestazione viene stampato nella console.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  In questo esempio viene esposto un servizio flusso di lavoro tramite endpoint HTTP.Per eseguire questo esempio, è necessario aggiungere \(per informazioni dettagliate, vedere [Configurazione di HTTP e HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)\) elenchi ACL URL appropriati eseguendo Visual Studio come amministratore oppure eseguendo il comando seguente a un prompt con privilegi elevati per aggiungere gli ACL appropriati.Assicurarsi che vengono sostituiti il dominio e il nome utente.  
  
    ```  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2.  Una volta aggiunti gli elenchi ACL URL, utilizzare i passaggi seguenti.  
  
    1.  Compilare la soluzione.  
  
    2.  Impostare più progetti di avvio facendo clic con il pulsante destro del mouse sulla soluzione e selezionando **Imposta progetti di avvio**.  
  
    3.  Aggiungere **Servizio** e **Client** \(in tale ordine\) come più progetti di avvio.  
  
    4.  Eseguire l'applicazione.Nella console client viene visualizzato un flusso di lavoro che viene eseguito due volte e nella finestra Servizio è visualizzato l'ID istanza di tali flussi di lavoro.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Services\Accessing Operation Context`