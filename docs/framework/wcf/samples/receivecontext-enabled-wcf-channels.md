---
title: "Canali WCF abilitati per ReceiveContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d990d119-7321-4b8c-852b-10256f59f9b0
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Canali WCF abilitati per ReceiveContext
In questo esempio viene illustrata l'utilità dei canali WCF abilitati per <xref:System.ServiceModel.Channels.ReceiveContext>.  In questo esempio viene implementato un servizio per trovare il prodotto di due numeri usando un canale NetMSMQ.  
  
 La classe <xref:System.ServiceModel.Channels.ReceiveContext> consente a un'applicazione di scegliere se accedere al messaggio o lasciarlo nella coda per l'ulteriore elaborazione, anche dopo il controllo del contenuto del messaggio.  In questo esempio un client invia integer casuali a una coda transazionale.  Il servizio `ProductCalculator` riceve i messaggi e controlla il contenuto dei messaggi, costituito da integer, per determinare se è possibile calcolare il prodotto.  Se l'operazione del servizio non determina il calcolo del prodotto, il messaggio viene inserito di nuovo nella coda e può essere ricevuto nuovamente dal servizio in ascolto sulla coda.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\ReceiveContextProductGenerator`  
  
#### Per usare questo esempio  
  
1.  Verificare che Accodamento messaggi Microsoft \(MSMQ\) sia installato.  
  
    1.  Per installare MSMQ in [!INCLUDE[lserver](../../../../includes/lserver-md.md)]:  
  
        1.  In **Server Manager** fare clic su **Funzionalità**.  
  
        2.  Nel riquadro destro in **Riepilogo funzionalità** fare clic su **Aggiungi funzionalità**.  
  
        3.  Nella finestra che viene visualizzata espandere **Accodamento messaggi**.  
  
        4.  Espandere **Servizi Accodamento messaggio**.  
  
        5.  Fare clic su **Integrazione servizi directory** \(per i computer associati ad un dominio\), quindi fare clic su **Supporto HTTP**.  
  
        6.  Fare clic su **Avanti**, quindi su **Installa**.  
  
    2.  Per installare MSMQ in [!INCLUDE[wv](../../../../includes/wv-md.md)]  
  
        1.  Aprire il **Pannello di controllo**.  
  
        2.  Fare clic su **Programmi**, quindi in **Programmi e funzionalità** fare clic su **Attivazione e disattivazione delle funzionalità Windows**.  
  
        3.  Espandere **Microsoft Message Queue \(MSMQ\) Server**, espandere **Componenti di base di Microsoft Message Queue \(MSMQ\) Server**, quindi selezionare le caselle di controllo per l'installazione delle funzionalità di Accodamento messaggi seguenti:  
  
            -   Message Queuing Server  
  
            -   Integrazione dei Servizi di dominio Active Directory MSMQ \(per i computer aggiunti a un dominio\).  
  
            -   Supporto HTTP MSMQ  
  
        4.  Fare clic su **OK**.  
  
        5.  Se viene richiesto di riavviare il computer, fare clic su **OK** per completare l'installazione.  
  
2.  Verificare che [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] sia installato nel computer.  
  
3.  Usare [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] per aprire il file della soluzione ReceiveContextProductGenerator.sln.  
  
4.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
5.  Per eseguire la soluzione, premere CTRL\+F5.