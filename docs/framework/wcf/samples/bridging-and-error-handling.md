---
title: "Bridging e gestione degli errori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ae87d1a-b615-4014-a494-a53f63ff0137
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Bridging e gestione degli errori
In questo esempio viene descritto come il servizio di routing di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene utilizzato per il collegamento delle comunicazioni tra un client e un servizio che impiegano associazioni diverse.L'esempio mostra inoltre come utilizzare un servizio di backup per scenari di failover.Il servizio di routing è un componente di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che semplifica l'aggiunta nell'applicazione di un router basato sul contenuto.In questo esempio viene adattato l'esempio relativo alla calcolatrice [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] standard per comunicare tramite il servizio di routing.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\RoutingServices\ErrorHandlingAndBridging`  
  
## Dettagli dell'esempio  
 In questo esempio, il client calcolatrice è configurato per inviare messaggi a un endpoint esposto dal router.Il servizio di routing è configurato per accettare tutti i messaggi ad esso inviati e per inoltrarli a un endpoint che corrisponde al servizio di calcolatrice.Nei punti seguenti viene descritta la configurazione del servizio di calcolatrice primario, del servizio di calcolatrice di backup e del client calcolatrice. Vengono inoltre fornite informazioni sulla modalità di comunicazione tra client e servizio mediante il servizio di routing:  
  
-   Il client calcolatrice è configurato per utilizzare BasicHttpBinding, mentre il servizio di calcolatrice è configurato per utilizzare NetTcpBinding.Il servizio di routing converte automaticamente i messaggi in modo appropriato prima di inviarli al servizio di calcolatrice e converte anche le risposte in modo che il client calcolatrice sia in grado di accedervi.  
  
-   Il servizio di routing è in grado di riconoscere la presenza di due servizi di calcolatrice: il servizio di calcolatrice primario e il servizio di calcolatrice di backup.Il servizio di routing tenta in primo luogo di comunicare con l'endpoint del servizio di calcolatrice primario.Se il tentativo non riesce a causa dell'inattività dell'endpoint, il servizio di routing tenta di comunicare con l'endpoint del servizio di calcolatrice di backup.  
  
 I messaggi inviati dal client vengono pertanto ricevuti dal router e reindirizzati al servizio di calcolatrice effettivo.Se l'endpoint del servizio di calcolatrice è inattivo, il servizio di routing instrada il messaggio all'endpoint del servizio di calcolatrice di backup.I messaggi provenienti dal servizio di calcolatrice di backup vengono inviati nuovamente al router del servizio, che a sua volta li inoltra al client calcolatrice.  
  
> [!NOTE]
>  In un elenco di backup possono essere definiti più endpoint.In questo caso, se l'endpoint del servizio di backup è inattivo, il servizio di routing tenta di connettersi all'endpoint di backup successivo nell'elenco fino a quando il tentativo di connessione non riesce.  
  
#### Per utilizzare questo esempio  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire RouterBridgingAndErrorHandling.sln.  
  
2.  Premere F5 o CTRL\+MAIUSC\+B in Visual Studio  
  
    1.  Se si desidera avviare automaticamente i progetti necessari quando si preme F5, fare clic con il pulsante destro del mouse sulla soluzione, selezionare **Proprietà**, quindi nel nodo **Progetto di avvio**, in **Proprietà comuni**, selezionare **Progetti di avvio multipli** e impostare tutti i progetti su **Avvia**.  
  
    2.  Se si compila il progetto con CTRL\+MAIUSC\+B, avviare le applicazioni seguenti:  
  
        1.  Client calcolatrice \(.\/CalculatorClient\/bin\/client.exe\)  
  
        2.  Servizio di calcolatrice \(.\/CalculatorService\/bin\/service.exe\)  
  
        3.  Servizio di routing \(.\/RoutingService\/bin\/RoutingService.exe\)  
  
3.  Nel client calcolatrice, premere INVIO per avviare il client.  
  
     È necessario visualizzare il seguente output:  
  
    ```Output  
    Add(100,15.99) = 115.99  
    Subtract(145,76.54) = 68.46  
    Multiply(9,81.25) = 731.25  
    Divide(22,7) = 3.14285714285714  
  
    ```  
  
## Configurabile tramite codice o App.config  
 L'esempio proposto è configurato per l'utilizzo di un file App.config per definire il comportamento del router.È inoltre possibile modificare il nome del file App.config affinché non venga riconosciuto e rimuovere i commenti dalla chiamata al metodo in `ConfigureRouterViaCode()`.Entrambi i metodi restituiscono lo stesso comportamento da parte del router.  
  
### Scenario  
 L'esempio dimostra il funzionamento del router del servizio come bridge del protocollo e gestore errori.In questo scenario, non si verifica alcun routing basato sul contenuto; il servizio di routing viene utilizzato come nodo proxy trasparente configurato per inoltrare direttamente messaggi a un set preconfigurato di endpoint di destinazione.Il servizio di routing esegue inoltre i passaggi aggiuntivi di gestione trasparente degli errori che si verificano in caso di invio agli endpoint con i quali è prevista la comunicazione in base alla configurazione.Utilizzato come bridge del protocollo, il servizio di routing consente all'utente di definire un protocollo per le comunicazioni esterne e un altro per le comunicazioni interne.  
  
### Scenario reale  
 Contoso desidera fornire un endpoint del servizio interoperativo a livello mondiale, ottimizzando al contempo le prestazioni interne.Propone pertanto i propri servizi a livello internazionale tramite un endpoint utilizzando BasicHttpBinding e ricorrendo internamente al servizio di routing che funge da bridge alla connessione all'endpoint utilizzando NetTcpBinding, impiegato dai propri servizi.Inoltre, poiché Contoso desidera che il servizio offerto tenga conto di possibili periodi di interruzione temporanei in uno dei servizi di produzione, virtualizza più endpoint associati al servizio del router utilizzando le funzionalità di gestione degli errori per il failover automatico nel caso in cui si renda necessario effettuare il backup degli endpoint.  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)