---
title: "Ritardo durevole in XAMLX | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efc38df4-2d34-453c-8e59-2c21d1307354
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Ritardo durevole in XAMLX
In questo esempio viene illustrato come utilizzare un ritardo durevole, ovvero un ritardo che rende persistente il flusso di lavoro in un dispositivo durevole durante il ritardo.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\DurableDelayXamlx`  
  
## Discussione  
 Il flusso di lavoro di esempio contiene due messaggi in un file locale separati da un ritardo.Quando viene attivato il ritardo, il flusso di lavoro viene scaricato e attende 5 secondi nell'archivio di istanze del flusso di lavoro prima di essere ricaricato in memoria.  
  
 Il file .xamlx è un servizio di flusso di lavoro ospitato in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].In [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] viene utilizzato Cassini che utilizza un host del servizio del flusso di lavoro per ospitare il flusso di lavoro.  
  
 Oltre a ospitare il flusso di lavoro, l'host del servizio flusso di lavoro gestisce le istanze del flusso di lavoro caricandole e scaricandole.Per avviare un'istanza della definizione di [!INCLUDE[wf](../../../../includes/wf-md.md)] \(nell'host del servizio flusso di lavoro\), impostare un client che invia un messaggio all'attività <xref:System.ServiceModel.Activities.Receive> nel flusso di lavoro.Questo oggetto <xref:System.ServiceModel.Activities.Receive> dispone della proprietà <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> impostata su `true` in modo che possa creare una nuova istanza del flusso di lavoro dopo aver ricevuto un messaggio.  
  
 Durante l'inizializzazione, viene aggiunto un comportamento di scaricamento di istanze al file di configurazione che specifica all'host del servizio flusso di lavoro il punto in cui scaricare un'istanza nell'archivio di persistenza \(database\).Per questo esempio, scarica immediatamente l'istanza dopo che il flusso di lavoro diventa inattivo \(quando viene attivato il ritardo\).  
  
#### Per utilizzare questo esempio  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Passare alla cartella DurableDelayXamlx\\CS.  
  
3.  Eseguire Setup.cmd.  
  
4.  Eseguire [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] come Amministratore.  
  
5.  Aprire il file della soluzione DurableDelayXamlx.sln.  
  
6.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Proprietà**.  
  
7.  Selezionare **Progetti di avvio multipli** e impostare entrambi i progetti su **Avvia**.  
  
8.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
9. Per eseguire la soluzione, premere CTRL\+F5.  
  
#### Per disinstallare l'esempio  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Passare alla cartella DurableDelayXamlx\\CS.  
  
3.  Eseguire Cleanup.cmd.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\DurableDelayXamlX`