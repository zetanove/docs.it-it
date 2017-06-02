---
title: "Generazione degli esempi Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2899e7a5-9cb2-4e8d-b8d2-f31391549198
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Generazione degli esempi Windows Communication Foundation
Gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono essere compilati utilizzando Visual Studio 2010 oppure utilizzando il comando **msbuild** dalla riga di comando.Entrambe le procedure sono descritte in questo argomento.  
  
> [!NOTE]
>  Prima di compilare o eseguire qualsiasi esempio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], verificare di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
### Per compilare l'esempio utilizzando il prompt dei comandi  
  
1.  Aprire il prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore, quindi spostarsi nella sottodirectory specifica del linguaggio nel percorso della directory in cui è installato l'esempio.  
  
2.  Digitare `msbuild` dalla riga di comando.I file di programma client vengono compilati in client\\bin, mentre i file del programma del servizio vengono compilati in service\\bin.Se il servizio viene ospitato in Internet Information Services \(IIS\), i file del programma del servizio vengono inoltre copiati nella directory servicemodelsamples e nella sottodirectory \\bin.  
  
> [!NOTE]
>  È necessario impostare ACLs su %systemdrive%\\inetpub\\wwwroot per concedere autorizzazioni di modifica per l'account in esecuzione.In caso contrario vi saranno errori relativi a eventi post\-compilazione.In alternativa, è possibile lasciare le ACL come sono ed eseguire il prompt dei comandi SDK come amministratore.  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Se si utilizza [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../../includes/lserver-md.md)], Windows 7 o Windows Server 2008 R2 e si esegue [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], è necessario eseguire [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] con privilegi elevati.A tale scopo, fare clic con il pulsante destro del mouse sul menu Start e quindi scegliere **Esegui come amministratore**.  
  
2.  Scegliere **Apri** dal menu **File** di [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] e fare clic su **Progetto\/Soluzione**.Passare alla sottodirectory specifica del linguaggio della directory in cui si è installato l'esempio e fare doppio clic sull'icona del file con estensione sln per aprire la soluzione in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
3.  Scegliere **Ricompila soluzione** dal menu **Compila**.I file di programma client vengono compilati su client\\bin e i file del programma del servizio vengono compilati su service\\bin.Se il servizio viene ospitato su IIS, i file del programma del servizio vengono inoltre copiati nella directory servicemodelsamples e nella sottodirectory \\bin.  
  
> [!NOTE]
>  È necessario impostare ACLs su %systemdrive%\\inetpub\\wwwroot per concedere autorizzazioni di modifica per l'account in esecuzione.In caso contrario vi saranno errori relativi a eventi post\-compilazione.In alternativa, è possibile lasciare le ACL come sono ed eseguire il prompt dei comandi SDK o Visual Studio come amministratore.Anche alcune azioni di Visual Studio \(ad esempio allegare un debugger al processo di lavoro ASP.NET\) richiedono privilegi amministrativi.  
  
## Impostare file batch e script  
 I file batch Setup.exe e Cleanup.exe e gli script devono essere eseguiti da un prompt dei comandi di Visual Studio.Diversi file di installazione e pulizia eseguono attività che richiedono privilegi amministrativi e devono essere avviati con privilegi di questo tipo.  
  
## Importanti informazioni di sicurezza sugli endpoint dei metadati  
 Per impedire la rivelazione non intenzionale di metadati del servizio potenzialmente riservati la configurazione predefinita per i servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] disabilita la pubblicazione dei metadati.Questo comportamento è protetto per impostazione predefinita, ma significa inoltre che non è possibile utilizzare uno strumento di importazione di metadati \(ad esempio Svcutil.exe\) per generare il codice client necessario per chiamare il servizio a meno che il comportamento del servizio di pubblicazione dei metadati non venga attivato in modo esplicito in fase di configurazione.Per rendere più semplice la sperimentazione con gli esempi, quasi tutti gli esempi espongono un endpoint di pubblicazione dei metadati non protetto.Tali endpoint sono potenzialmente disponibili per utenti anonimi non autenticati anonimi e bisogna fare attenzione prima di distribuirli per garantire che la pubblicazione dei metadati di un servizio sia appropriata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] pubblicazione dei metadati del servizio, vedere l'esempio [Comportamento di pubblicazione dei metadati](../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md).Vedere l'esempio [Endpoint di metadati protetto personalizzato](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md) per un esempio di protezione di un endpoint di metadati.  
  
## Gestione delle eccezioni  
 In genere questi esempi non includono la gestione delle eccezioni per fare in modo che il codice sia focalizzato sull'argomento dell'esempio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] gestione delle eccezioni, vedere l'esempio [Eccezioni previste](../../../../docs/framework/wcf/samples/expected-exceptions.md).  
  
## Rigenerazione client e configurazione con Svcutil  
 È possibile utilizzare [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per rigenerare codice client e configurare la maggior parte degli esempi.Alcuni esempi richiedono una configurazione manuale.Ad esempio, se si utilizza Svcutil.exe per rigenerare la configurazione per un esempio che utilizza credenziali del certificato client, si devono specificare manualmente le credenziali precedentemente configurate.Alcuni esempi utilizzano opzioni Svcutil.exe specifiche per influire sul codice generato, queste opzioni sono specificate in argomenti di esempio appositi.  
  
#### Per rigenerare client e file di configurazione  
  
1.  Aprire il prompt dei comandi SDK, quindi spostarsi nella sottodirectory specifica del linguaggio del percorso della directory in cui si è installato l'esempio.  
  
2.  Se il servizio è di tipo ospitato sul Web, utilizzare il comando seguente.  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
    ```  
  
     Se il servizio è di tipo indipendente, digitare il comando seguente.  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
    ```  
  
     Sostituire http:\/\/localhost:8000\/ServiceModelSamples\/service .svc\/mex con l'indirizzo dell'endpoint mex del servizio indipendente.  
  
     Per generare il client in un tipo Visual Basic, utilizzare il comando seguente.  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb  
  
    ```  
  
     Se il servizio è di tipo indipendente, utilizzare il comando seguente.  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb  
    ```  
  
    > [!NOTE]
    >  Per ignorare la generazione della configurazione client, aggiungere l'opzione **\/noConfig**.  
  
## Vedere anche  
 [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)