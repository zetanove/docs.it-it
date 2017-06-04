---
title: "Hosting in un&#39;applicazione di servizio Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4199998-27f3-4dd9-aee4-0a4addfa9f24
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Hosting in un&#39;applicazione di servizio Windows
I servizi Windows, precedentemente noti come servizi Windows NT, offrono un modello di processo particolarmente adatto ad applicazioni che devono risiedere in un eseguibile a esecuzione prolungata e che non visualizzano alcuna forma di interfaccia utente.  La durata del processo di un'applicazione di servizio Windows viene gestita da Gestione controllo servizi \(SCM\), che consente di avviare, interrompere e sospendere le applicazioni di servizio Windows.  È possibile configurare un processo di servizio Windows perché venga automaticamente avviato all'avvio del computer, rendendolo un ambiente host adatto ad applicazioni sempre attive.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle applicazioni del servizio Windows, vedere [Applicazioni di servizio Windows](http://go.microsoft.com/fwlink/?LinkId=89450).  
  
 Le applicazioni che ospitano servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] a esecuzione prolungata condividono molte caratteristiche dei servizi Windows.  In particolare, i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono eseguibili server a esecuzione prolungata che non interagiscono direttamente con l'utente e non implementano quindi alcuna forma di interfaccia utente.  Pertanto, l'hosting di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] all'interno di un'applicazione di servizio Windows è una delle opzioni per la creazione di efficaci applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] a esecuzione prolungata.  
  
 Gli sviluppatori [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] devono spesso decidere se ospitare le proprie applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in un'applicazione di servizio Windows o nell'ambiente host IIS \(Internet Information Services\) o del servizio di attivazione dei processi di Windows \(WAS\).  È consigliabile considerare l'uso di applicazioni di servizio Windows alle condizioni seguenti:  
  
-   L'applicazione richiede l'attivazione esplicita.  È, ad esempio, consigliabile usare servizi Windows quando l'applicazione deve essere avviata automaticamente all'avvio del server, invece di essere avviata dinamicamente in risposta al primo messaggio in ingresso.  
  
-   Il processo che ospita l'applicazione deve restare in esecuzione una volta avviato.  Una volta avviato, un processo di servizio Windows resta in esecuzione, a meno che non venga esplicitamente interrotto da un amministratore del server tramite Gestione controllo servizi.  Le applicazioni ospitate in IIS o WAS possono essere avviate e interrotte dinamicamente, per usare le risorse di sistema in modo ottimale.  Le applicazioni che richiedono il controllo esplicito sulla durata del processo host dovrebbero usare servizi Windows invece di IIS o WAS.  
  
-   È necessario eseguire il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] su Windows Server 2003 e usare trasporti diversi da HTTP.  Su Windows Server 2003, l'ambiente host [!INCLUDE[iis601](../../../../includes/iis601-md.md)] è limitato alla sola comunicazione HTTP.  Le applicazioni di servizio Windows non sono soggette a questa restrizione e possono usare qualsiasi trasporto supportato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], inclusi net.tcp, net.pipe e net.msmq.  
  
### Per ospitare WCF in un'applicazione di servizio Windows  
  
1.  Creare un'applicazione di servizio Windows.  È possibile scrivere applicazioni di servizio Windows in codice gestito usando le classi nello spazio dei nomi <xref:System.ServiceProcess>.  Questa applicazione deve includere una classe che eredita da <xref:System.ServiceProcess.ServiceBase>.  
  
2.  Collegare la durata dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] alla durata dell'applicazione di servizio Windows.  In genere, si desidera che i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in un'applicazione di servizio Windows divengano attivi quando viene avviato il servizio di hosting, interrompano l'ascolto dei messaggi quando viene arrestato il servizio di hosting e interrompano il processo di hosting quando il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] rileva un errore.  Per ottenere questo risultato, è possibile procedere come segue:  
  
    -   Eseguire l'override di [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> per aprire una o più istanze di <xref:System.ServiceModel.ServiceHost>.  Una sola applicazione di servizio Windows può ospitare più servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], che vengono avviati e interrotti come gruppo.  
  
    -   Eseguire l'override di <xref:System.ServiceProcess.ServiceBase.OnStop%2A> per chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Closed> su <xref:System.ServiceModel.ServiceHost> per tutti i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in esecuzione avviati durante [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>.  
  
    -   Eseguire la sottoscrizione all'evento <xref:System.ServiceModel.Channels.CommunicationObject.Faulted> di <xref:System.ServiceModel.ServiceHost> e usare la classe <xref:System.ServiceProcess.ServiceController> per arrestare l'applicazione di servizio Windows in caso di errore.  
  
     Le applicazioni di servizio Windows che ospitano servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono distribuite e gestite nello stesso modo delle applicazioni di servizio Windows che non usano [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Vedere anche  
 <xref:System.ServiceProcess>   
 [Procedura dettagliata: creazione di un'applicazione di servizio per Windows nella finestra Progettazione componenti](http://go.microsoft.com/fwlink/?LinkId=94875)   
 [Procedura: ospitare un servizio WCF in un servizio Windows gestito](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [Host del servizio Windows](../../../../docs/framework/wcf/samples/windows-service-host.md)   
 [Architettura di programmazione delle applicazioni di servizio](http://go.microsoft.com/fwlink/?LinkId=94876)   
 [Funzionalità di hosting di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)