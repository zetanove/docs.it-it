---
title: "OperationScope | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56206a21-1e63-422d-b92a-e5d8b713e707
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# OperationScope
In questo esempio viene illustrato come è possibile utilizzare le attività di messaggistica, <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> per esporre un'attività personalizzata esistente come operazione in un servizio flusso di lavoro.Questo esempio include una nuova attività personalizzata chiamata `OperationScope`.È destinata a facilitare lo sviluppo di un servizio flusso di lavoro consentendo agli utenti di creare separatamente il corpo delle operazioni come attività personalizzate ed esponendole quindi facilmente come operazioni del servizio tramite l'attività `OperationScope`.Ad esempio, un'attività `Add` personalizzata che accetta due argomenti `in` e restituisce un argomento `out` potrebbe essere esposta come un'operazione `Add` nel servizio flusso di lavoro rilasciandolo in `OperationScope`.  
  
 Il funzionamento dell'ambito si basa sul controllo dell'attività fornita come corpo.Gli eventuali argomenti `in` non associati vengono considerati come input dal messaggio in arrivo.Tutti gli argomenti `out`, indipendentemente che siano  associati, sono considerati come output nel messaggio di risposta successivo.Il nome dell'operazione esposto viene rilevato dal nome visualizzato dell'attività `OperationScope`.Come risultato finale viene eseguito il wrapping dell'attività del corpo in un oggetto <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> con i parametri dei messaggi associati agli argomenti dell'attività.  
  
 In questo esempio viene esposto un servizio flusso di lavoro tramite endpoint HTTP.Per l'esecuzione, è necessario aggiungere ACL di URL appropriati.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Configurazione di HTTP e HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353).L'esecuzione del comando seguente a un prompt con privilegi elevati consente di aggiungere ACL appropriati \(assicurarsi di sostituire % DOMAIN%\\%UserName% con dominio e nome utente\).  
  
 **netsh http add urlacl url\=http:\/\/\+:8000\/ user\=%DOMAIN%\\%UserName%**  
  
### Per eseguire l’esempio  
  
1.  Aprire la soluzione OperationScope.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Impostare più progetti di avvio facendo clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e scegliendo **Imposta progetti di avvio**.Aggiungere Scenario e Scenario\_Client \(in tale ordine\) come più progetti di avvio.  
  
3.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
    > [!WARNING]
    >  Questo passaggio è necessario per visualizzare il flusso di lavoro BankService.xaml a causa dell'attività personalizzata `OperationScope`.  
  
4.  Premere CTRL\+F5 per eseguire l'applicazione.La console Scenario\_Client richiede l'input e l'output corrispondente viene visualizzato nella console di Scenario.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Services\OperationScope`  
  
## Vedere anche