---
title: "Gestione avanzata degli errori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed54b687-78af-4eda-8507-9fd081bdea1a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Gestione avanzata degli errori
Nell'esempio viene descritto il servizio di routing [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  Il servizio di routing è un componente di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che semplifica l'aggiunta nell'applicazione di un router basato sul contenuto.  Nell'esempio viene illustrata la modalità di ripristino intelligente del servizio di routing in caso di errore mediante l'uso di transazioni e altri concetti di messaggistica più complessi, ad esempio il multicasting.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\RoutingServices\AdvancedErrorHandling`  
  
## Dettagli dell'esempio  
 In questo esempio il servizio di routing è configurato per leggere un messaggio da una coda MSMQ ed eseguirne il multicasting a due elenchi di code.  Un elenco viene usato per le code dei servizi e un altro per le code di registrazione.  
  
 Poiché per impostazione predefinita l'associazione MSMQ per il cui uso è configurato il servizio di routing supporta l'uso di transazioni, il servizio di routing verifica che il messaggio sia transazionale e che sia stato ricevuto da almeno una coda in ogni elenco prima della segnalazione alla coda in ingresso \(`InQ`\) a cui il messaggio è stato indirizzato correttamente.  Pertanto, nel caso in cui non siano disponibili entrambe le code dei servizi o entrambe le code di registrazione, il servizio di routing segnalerà l'impossibilità di indirizzare il messaggio e la coda in ingresso dovrà intraprendere un'azione.  Questa azione consiste nello spostamento del messaggio alla coda di messaggi non recapitabili di sistema.  
  
#### Per usare questo esempio  
  
1.  > [!IMPORTANT]
    >  Installare MSMQ prima di eseguire questo esempio.  Se MSMQ non è installato, nel momento in cui l'esempio viene eseguito verrà restituito un messaggio di eccezione.  Le istruzioni per l'installazione di Accodamento messaggi sono disponibili in [Installazione di Accodamento messaggi](http://go.microsoft.com/fwlink/?LinkId=166437).  
  
     Aprire AdvancedErrorHandling.sln usando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Premere **F5** o **CTRL\+MAIUSC\+B** in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
    1.  Se l'applicazione viene compilata con CTRL\+MAIUSC\+B, sarà necessario avviare l'applicazione in .\/RoutingService\/bin\/debug\/RoutingService.exe.  
  
3.  Nella finestra della console premere INVIO per avviare il client.  
  
4.  Il client restituirà statistiche diverse relativamente alle code per ogni caso.  
  
    1.  Di seguito è riportato l'output restituito per il caso 1 \(nessun errore\).  
  
        ```Output  
  
                            La coda in ingresso contiene 0 messaggi.  
  
        La coda dei servizi primaria contiene 1 messaggio.  
  
        La coda dei servizi di backup contiene 0 messaggio.  
  
        La coda di registrazione primaria contiene 1 messaggio.  
  
        La coda di registrazione di backup contiene 0 messaggi.  
  
        Premere <INVIO> per continuare.  
  
        ```  
  
    2.  Di seguito è riportato l'output restituito per il caso 3 \(coda dei servizi primaria e di registrazione con errori\).  
  
        ```Output  
  
        La coda in ingresso contiene 0 messaggi.  
  
        La coda dei servizi primaria non esiste.  
  
        La coda dei servizi di backup contiene 1 messaggio.  
  
        La coda di registrazione primaria non esiste.  
  
        La coda di registrazione di backup contiene 1 messaggi.  
  
        Premere <INVIO> per continuare.  
  
        ```  
  
    3.  Di seguito è riportato l'output restituito per il caso 4 \(coda dei servizi primaria e coda di registrazione primaria e di backup con errori\).  
  
        ```Output  
  
                            La coda in ingresso contiene 0 messaggi.  
  
        La coda dei servizi primaria non esiste.  
  
        La coda dei servizi di backup contiene 0 messaggio.  
  
        La coda di registrazione primaria non esiste.  
  
        La coda di registrazione di backup non esiste.  
  
        La coda di messaggi non recapitabili di sistema contiene 1 messaggio.  
  
        Premere <INVIO> per uscire.  
  
        ```  
  
    4.  Di seguito è riportato l'output restituito per il caso 2 \(coda dei servizi primaria con errori\).  
  
        ```Output  
  
                            La coda in ingresso contiene 0 messaggi.  
  
        La coda dei servizi primaria non esiste.  
  
        La coda dei servizi di backup contiene 1 messaggio.  
  
        La coda di registrazione primaria contiene 1 messaggio.  
  
        La coda di registrazione di backup contiene 0 messaggi.  
  
        Premere <INVIO> per continuare.  
  
        ```  
  
## Configurabile tramite codice o App.config  
 L'esempio proposto è configurato per l'uso di un file App.config per la definizione del comportamento del router.  È inoltre possibile modificare il nome del file RoutingService\\App.config affinché non venga riconosciuto e modificare il valore del campo `configDriven` in RoutingService\\Program.cs su `false` per usare la configurazione definita nel codice.  Entrambi i metodi restituiscono lo stesso comportamento da parte del router.  
  
### Scenario  
 In questo esempio viene illustrato come il servizio di routing sia in grado di gestire funzionalità di messaggistica avanzate, ad esempio transazioni e contesto di ricezione, e possa usare tali funzionalità come parte della gestione corretta di scenari di errore.  
  
### Scenario reale  
 Contoso desidera usare ricezioni transazionali tramite il servizio di routing per garantire che tutti i servizi necessari ricevano le informazioni anche durante le condizioni di errore.  Desidera inoltre che gli errori vengano gestiti correttamente e automaticamente e che i problemi vengano segnalati nel caso in cui un messaggio non sia recapitabile anche quando viene usata la logica di gestione degli errori.  Per questo scopo, il servizio di routing viene configurato per il failover di endpoint specifici come previsto. Tale servizio gestisce inoltre le situazioni di errore, inclusi la creazione, il completamento, il rollback o l'interruzione di transazioni\/contesti di ricezione in base alle necessità.  
  
## Vedere anche  
 [Esempi di hosting e salvataggio permanente di AppFabric](http://go.microsoft.com/fwlink/?LinkId=193961)