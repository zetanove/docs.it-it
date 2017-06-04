---
title: "Esempio di federazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e9da0ca-e925-4644-aa96-8bfaf649d4bb
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Esempio di federazione
In questo esempio viene descritta la sicurezza federativa.  
  
## Dettagli dell'esempio  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce supporto per la distribuzione di architetture di sicurezza federate tramite `wsFederationHttpBinding`.L'elemento `wsFederationHttpBinding` offre un'associazione sicura, affidabile e interoperativa che comporta l'utilizzo di HTTP come meccanismo di trasporto sottostante per la comunicazione request\/reply e Text\/XML come formato di trasmissione per la codifica.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] federazione in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], vedere [Federazione](../../../../docs/framework/wcf/feature-details/federation.md).  
  
 Lo scenario è costituito da 4 elementi:  
  
-   Servizio della libreria  
  
-   Servizio token di protezione della libreria  
  
-   Servizio token di protezione HomeRealm  
  
-   Client della libreria  
  
 Il servizio della libreria supporta due operazioni, `BrowseBooks` e `BuyBook`.Consente accesso anonimo all'operazione `BrowseBooks`, ma richiede accesso autenticato per l'operazione `BuyBooks`.L'autenticazione prende il form di un token pubblicato dal Servizio token di protezione della libreria.Il file di configurazione per Servizio della Libreria punta i client al Servizio token di protezione della libreria utilizzando l'`wsFederationHttpBinding`.  
  
```  
<wsFederationHttpBinding>  
<!-- This is the Service binding for the BuyBooks endpoint. It redirects clients to the BookStore STS -->  
    <binding name='BuyBookBinding'>  
        <security mode="Message">  
            <message>  
                <issuerMetadata  
  address='http://localhost/FederationSample/BookStoreSTS/STS.svc/mex' >  
                    <identity>  
                        <dns value ='BookStoreSTS.com'/>  
                    </identity>  
                </issuerMetadata>  
            </message>  
        </security>  
    </binding>  
</wsFederationHttpBinding>  
```  
  
 Il servizio token di protezione della libreria richiede quindi che i client si autentichino utilizzando un token pubblicato dal servizio token di protezione HomeRealm.Anche in questo caso, il file di configurazione per il servizio token di protezione della libreria punta i client al servizio token di protezione HomeRealm utilizzando `wsFederationHttpBinding`.  
  
```  
<wsFederationHttpBinding>  
 <!-- This is the binding for the clients requesting tokens from this STS. It redirects clients to the HomeRealm STS -->  
    <binding name='BookStoreSTSBinding'>  
        <security mode='Message'>  
            <message>  
                <issuerMetadata  
 address='http://localhost/FederationSample/HomeRealmSTS/STS.svc/mex' >  
                    <identity>  
                        <dns value ='HomeRealmSTS.com' />  
                    </identity>  
                </issuerMetadata>  
            </message>  
        </security>  
    </binding>  
</wsFederationHttpBinding>  
```  
  
 La sequenza di eventi quando si accede all'operazione `BuyBook` è la seguente:  
  
1.  Il client effettua l'accesso al servizio token di protezione HomeRealm utilizzando le credenziali di Windows.  
  
2.  Il servizio token di protezione HomeRealm pubblica un token che può essere utilizzato per accedere al servizio token di protezione della libreria.  
  
3.  Il client accede al servizio token di protezione della libreria utilizzando il token pubblicato dal servizio token di protezione HomeRealm.  
  
4.  Il servizio token di protezione della libreria pubblica un token che può essere utilizzato per accedere al servizio della libreria.  
  
5.  Il client accede al servizio della libreria utilizzando il token pubblicato dal servizio token di protezione della libreria.  
  
6.  Il client accede all'operazione `BuyBook`.  
  
 Vedere le istruzioni seguenti su come impostare ed eseguire l'esempio.  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario disporre di autorizzazioni di scrittura per la directory **wwwroot**.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la finestra del prompt dei comandi SDK.Nel percorso di esempio, eseguire Setup.bat.Ciò crea le directory virtuali richieste per l'esempio e installa i certificati obbligatori con le autorizzazioni adeguate.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di Windows SDK.e richiede che la variabile di ambiente MSSDK punti alla directory in cui è installato SDK.Questa variabile di ambiente viene impostata automaticamente all'interno di un prompt dei comandi di SDK di Windows.In [!INCLUDE[wv](../../../../includes/wv-md.md)], è necessario assicurarsi che Compatibilità di gestione con IIS 6.0 sia installato perché la configurazione utilizza script amministrativi di IIS.L'esecuzione dello script di installazione in [!INCLUDE[wv](../../../../includes/wv-md.md)] richiede privilegi di amministratore.  
  
2.  Aprire FederationSample.sln in Visual Studio e selezionare **Compila soluzione** nel menu **Compila**.Compila i file di progetto comuni, il servizio della libreria, gli STS della libreria, gli STS di HomeRealm e li distribuisce in IIS.Compila anche l'applicazione client della libreria e posiziona il file eseguibile BookStoreClient.exe nella cartella FederationSample\\BookStoreClient\\bin\\Debug.  
  
3.  Fare doppio clic su BookStoreClient.exe.Verrà visualizzata la finestra BookStoreClient.  
  
4.  È possibile esplorare i libri disponibili nella libreria facendo clic su **Sfoglia libri**.  
  
5.  Per acquistare un particolare libro, selezionarlo dall'elenco e fare clic su **Acquista libro**.L'applicazione si avvia e effettua l'autenticazione utilizzando l'autenticazione di Windows con il servizio token di protezione HomeRealm.  
  
     L'esempio è configurato per consentire agli utenti di acquistare libri che costano 15$ o meno.Il tentativo di acquistare volumi che costano più di 15$ comporta il ricevimento da parte del client di un messaggio Accesso negato dal servizio della libreria.  
  
    > [!NOTE]
    >  L'esempio non aggiorna il limite di credito dell'utente dopo un acquisto.È possibile acquistare ripetutamente libri entro i limiti di credito \(fissi\) dell'utente.  
  
#### Per eseguire la pulizia  
  
1.  Eseguire Cleanup.bat.Ciò consente di eliminare le directory virtuali create durante l'installazione e di rimuovere inoltre i certificati installati durante l'installazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\Federation`  
  
## Vedere anche