---
title: "Comunicazione asincrona | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 128dc092-9eb2-4e33-9470-9a7f62b60df6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Comunicazione asincrona
In questo esempio viene illustrata la modalità di esecuzione della comunicazione, eseguita in modo asincrono per impostazione predefinita, tra due diversi servizi [!INCLUDE[wf](../../../../includes/wf-md.md)].  
  
## Dimostrazione  
 Comunicazione asincronica tra servizi [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  
  
## Discussione  
 In questo esempio viene illustrata la modalità di esecuzione della comunicazione asincrona tra applicazioni [!INCLUDE[wf1](../../../../includes/wf1-md.md)] tramite le attività di messaggistica fornite da .NET Framework.  
  
 L'esempio è costituito dai tre progetti seguenti.  
  
 CreditCheckService  
 Questo servizio riceve il punteggio del credito di una particolare persona o il valore dell'elemento da acquisire, quindi stabilisce se viene concesso alla persona il credito.  
  
 RentalApprovalService  
 Questo servizio riceve un'applicazione da una persona che richiede credito.Il servizio comunica in modo asincrono con `CreditCheckService` per determinare se la richiesta di credito è valida.  
  
 Client  
 Il client comunica in modo sincrono con `RentalApprovalService` per sapere se il credito è approvato.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Fare clic con il pulsante destro del mouse sulla soluzione **AsynchronousCommunication** e scegliere **Proprietà**.  
  
2.  In **Proprietà comuni** selezionare **Progetto di avvio**, quindi **Progetti di avvio multipli**.  
  
3.  Spostare **RentalApprovalService** nella prima posizione nell'elenco, seguito da **CreditCheckService**, quindi da **Client**.Impostare l'azione **Avvia** per tutti e tre i progetti.  
  
4.  Fare clic su **OK** e premere F5 per eseguire l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\Services\AsynchronousCommunication`