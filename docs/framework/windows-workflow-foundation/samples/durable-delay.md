---
title: "Ritardo durevole | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 220ec240-b958-430c-81ff-b734a6aa97ae
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Ritardo durevole
In questo esempio viene illustrato come utilizzare un ritardo durevole, ovvero un ritardo che rende persistente il flusso di lavoro in un dispositivo durevole durante il ritardo.Il flusso di lavoro di esempio contiene due messaggi alla console separati da un ritardo.Quando viene attivato il ritardo, il flusso di lavoro viene scaricato e attende 5 secondi nell'archivio di istanze del flusso di lavoro prima di essere ricaricato in memoria.  
  
## Dettagli del flusso di lavoro  
 Oltre a ospitare il flusso di lavoro, l'host del servizio flusso di lavoro gestisce le istanze del flusso di lavoro caricandole e scaricandole.Per avviare un'istanza della definizione di flusso di lavoro, nell'esempio viene impostato un proxy che invia un messaggio all'attività <xref:System.ServiceModel.Activities.Receive> nel flusso di lavoro.La proprietà <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> è impostata su `true`, consentendo la creazione di una nuova istanza del flusso di lavoro dopo la ricezione di un messaggio.  
  
 Nell'elenco seguente viene fornita una descrizione dettagliata della configurazione del servizio flusso di lavoro durante l'inizializzazione.  
  
1.  Crea un host del servizio con un indirizzo \(http:\/\/localhost:8080\/Client\).  
  
2.  Crea un endpoint nell'host del servizio per abilitare la comunicazione con l'attività <xref:System.ServiceModel.Activities.Receive> nel flusso di lavoro.  
  
3.  Configura un archivio di istanze SQL.  
  
4.  Aggiunge un comportamento di scaricamento di istanze che specifica le condizioni in base alle quali l'host del servizio flusso di lavoro deve scaricare un'istanza del flusso di lavoro nell'archivio di persistenza SQL.Per questo esempio scarica immediatamente l'istanza dopo che il flusso di lavoro diventa inattivo \(quando viene attivato il ritardo\).  
  
5.  Crea il proxy che invia un messaggio all'attività <xref:System.ServiceModel.Activities.Receive> nel flusso di lavoro.  
  
#### Per utilizzare questo esempio  
  
1.  Impostare il database di persistenza.  
  
    1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
    2.  Passare alla directory [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] \(C:\\Windows\\Microsoft.NET\\Framework\\v4.X\\\).  
  
    3.  Modificare il file WorkflowManagementService.exe.config e aggiungere la stringa di connessione seguente nell'elemento \<`database`\>.  
  
        ```  
        <database connectionString="Data Source=localhost\SQLEXPRESS;Initial Catalog=DefaultSampleStore;Integrated Security=True;Asynchronous Processing=True" />  
  
        ```  
  
    4.  Passare alla directory DurableDelay\\CS.  
  
    5.  Eseguire Setup.cmd.  
  
2.  Eseguire [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] con autorizzazioni elevate facendo clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e scegliendo **Esegui come amministratore**.  
  
3.  Aprire il file della soluzione Delay.sln.  
  
4.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
5.  Premere CTRL\+F5 per eseguire la soluzione.  
  
#### Per disinstallare l'esempio  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Passare alla directory DurableDelay\\CS.  
  
3.  Eseguire Cleanup.cmd.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\DurableDelay`  
  
## Vedere anche