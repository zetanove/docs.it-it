---
title: "Endpoint di metadati protetto personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e369e99-ea4a-49ff-aed2-9fdf61091a48
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# Endpoint di metadati protetto personalizzato
In questo esempio viene illustrato come implementare un servizio con un endpoint di metadati protetto che utilizza una delle associazioni di scambio non di metadati e come configurare lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) o i client per il recupero di metadati da tale endpoint di metadati.Per l'esposizione di endpoint di metadati sono disponibili due associazioni fornite dal sistema, cioè mexHttpBinding e mexHttpsBinding.L'associazione mexHttpBinding viene utilizzata per esporre un endpoint di metadati tramite HTTP in modo non protetto.L'associazione mexHttpsBinding viene utilizzata per esporre un endpoint di metadati tramite HTTPS in modo non protetto.In questo esempio viene illustrato come esporre un endpoint di metadati protetto tramite <xref:System.ServiceModel.WSHttpBinding>.Procedere in questo modo quando si desidera modificare le impostazioni di sicurezza sull'associazione senza utilizzare HTTPS.Se si utilizza mexHttpsBinding, l'endpoint di metadati sarà protetto, ma non sarà in alcun modo possibile modificare le impostazioni dell'associazione.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
## Servizio  
 Il servizio di questo esempio è dotato di due endpoint.L'endpoint dell'applicazione invia al contratto `ICalculator` un `WSHttpBinding` con la `ReliableSession` attivata e la sicurezza dei `Message` che utilizza certificati.L'endpoint di metadati utilizza inoltre `WSHttpBinding`, con le stesse impostazioni di sicurezza ma senza `ReliableSession`.La configurazione pertinente è la seguente:  
  
```  
<services>  
    …  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
            behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- use base address provided by host -->  
     <endpoint address=""  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding2"  
       contract="Microsoft.ServiceModel.Samples.ICalculator" />  
     <endpoint address="mex"  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding1"  
       contract="IMetadataExchange" />  
     </service>  
 </services>  
 <bindings>  
   <wsHttpBinding>  
     <binding name="Binding1">  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
     <binding name="Binding2">  
       <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
   </wsHttpBinding>  
 </bindings>  
```  
  
 In molti degli altri esempi, l'endpoint di metadati utilizza il `mexHttpBinding` predefinito, che non è protetto.Qui i metadati sono protetti utilizzando `WSHttpBinding` con sicurezza dei `Message`.Affinché i client di metadati possano recuperare questi metadati, è necessario che siano configurati con un'associazione corrispondente.Nell'esempio viene illustrato l'utilizzo di due di questi client.  
  
 Il primo client utilizza Svcutil.exe per recuperare i metadati e generare il codice del client e la configurazione in fase di progettazione.Il servizio utilizza un'associazione non predefinita per i metadati, quindi lo strumento Svcutil.exe deve essere specificamente configurato in modo da ottenere i metadati dal servizio che utilizza quell'associazione.  
  
 Il secondo client utilizza il `MetadataResolver` per recuperare dinamicamente i metadati per un contratto noto e richiamare quindi le operazioni sul client generato dinamicamente.  
  
## Client Svcutil  
 Quando si utilizza l'associazione predefinita per ospitare l'endpoint `IMetadataExchange`, è possibile eseguire Svcutil.exe con l'indirizzo di quell'endpoint:  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 e funziona.Ma in questo esempio, il server utilizza un endpoint non predefinito per ospitare i metadati.È quindi necessario richiedere a Svcutil.exe di utilizzare l'associazione corretta.Questa operazione può essere eseguita utilizzando un file Svcutil.exe.config.  
  
 Il file Svcutil.exe.config sembra un file di configurazione client normale.Le uniche differenze sono il nome e il contratto dell'endpoint:  
  
```  
<endpoint name="http"  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"  
          behaviorConfiguration="ClientCertificateBehavior"  
          contract="IMetadataExchange" />  
```  
  
 Il nome dell'endpoint deve essere il nome dello schema dell'indirizzo in cui vengono ospitati i metadati e il contratto dell'endpoint deve essere `IMetadataExchange`.In questo modo, quando viene eseguito Svcutil.exe con una riga di comando simile alla seguente:  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 viene cercato l'endpoint denominato "http" e il contratto `IMetadataExchange` per configurare l'associazione e il comportamento dello scambio di comunicazione con l'endpoint di metadati.Il resto del file Svcutil.exe.config nell'esempio specifica la configurazione di associazione e le credenziali del comportamento per fare corrispondere la configurazione del server all'endpoint di metadati.  
  
 Perché Svcutil.exe selezioni la configurazione in Svcutil.exe.config, Svcutil.exe deve trovarsi nella stessa directory del file di configurazione.Di conseguenza, è necessario copiare Svcutil.exe dal percorso di installazione alla directory che contiene il file Svcutil.exe.config.Da tale directory, eseguire il comando seguente:  
  
```  
.\svcutil.exe http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 Il ". \\" inizialeassicura che la copia di Svcutil.exe in questa directory \(quello dotato di un Svcutil.exe.config corrispondente\) venga eseguita.  
  
## Client di MetadataResolver  
 Se il client conosce il contratto e come comunicare con i metadati in fase di progettazione, può scoprire dinamicamente l'associazione e indirizzo degli endpoint dell'applicazione utilizzando `MetadataResolver`.In questo esempio di client viene illustrata questa operazione, oltre a come configurare l'associazione e le credenziali utilizzate dal `MetadataResolver` creando e configurando un `MetadataExchangeClient`.  
  
 Le stesse informazioni sull'associazione e sul certificato visualizzate in Svcutil.exe.config possono essere specificate in modo imperativo nel `MetadataExchangeClient`:  
  
```  
// Specify the Metadata Exchange binding and its security mode  
WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a MetadataExchangeClient for retrieving metadata, and set the // certificate details  
MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
mexClient.SoapCredentials.ClientCertificate.SetCertificate(    StoreLocation.CurrentUser, StoreName.My,  
    X509FindType.FindBySubjectName, "client.com");  
mexClient.SoapCredentials.ServiceCertificate.Authentication.    CertificateValidationMode =    X509CertificateValidationMode.PeerOrChainTrust;  
mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(    StoreLocation.CurrentUser, StoreName.TrustedPeople,  
    X509FindType.FindBySubjectName, "localhost");  
```  
  
 Una volta configurato il `mexClient`, è possibile enumerare i contratti desiderati e utilizzare `MetadataResolver` per recuperare un elenco di endpoint con quei contratti:  
  
```  
// The contract we want to fetch metadata for  
Collection<ContractDescription> contracts =    new Collection<ContractDescription>();  
ContractDescription contract =    ContractDescription.GetContract(typeof(ICalculator));  
contracts.Add(contract);  
// Find endpoints for that contract  
EndpointAddress mexAddress = new    EndpointAddress(ConfigurationManager.AppSettings["mexAddress"]);  
ServiceEndpointCollection endpoints =    MetadataResolver.Resolve(contracts, mexAddress, mexClient);  
```  
  
 Infine, è possibile utilizzare le informazioni da quegli endpoint per inizializzare l'associazione e l'indirizzo di una `ChannelFactory` utilizzata per creare canali per comunicare con gli endpoint dell'applicazione.  
  
```  
ChannelFactory<ICalculator> cf = new    ChannelFactory<ICalculator>(endpoint.Binding, endpoint.Address);  
```  
  
 Il punto importante di questo esempio di client è di dimostrare che, se si utilizza `MetadataResolver` ed è necessario specificare associazioni o comportamenti personalizzati per la comunicazione di scambio di metadati, è possibile utilizzare un `MetadataExchangeClient` per specificare quelle impostazioni personalizzate.  
  
#### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
#### Per eseguire l'esempio sullo stesso computer  
  
1.  Eseguire Setup.bat dalla cartella di installazione dell'esempio.In tal modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.Si noti che Setup.bat utilizza lo strumento FindPrivateKey.exe, installato eseguendo setupCertTool.bat da [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Eseguire l'applicazione client da \\MetadataResolverClient\\bin o \\SvcutilClient\\bin.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
3.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
4.  Rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.Gli altri esempi relativi alla sicurezza utilizzano gli stessi certificati.  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Eseguire `setup.bat service` sul server.Quando si esegue `setup.bat` con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
2.  Modificare Web.config sul server per riflettere il nome del nuovo certificato,ovvero modificare l'attributo `findValue` nell'elemento [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) con il nome di dominio completo del computer.  
  
3.  Copiare il file Service.cer dalla directory del servizio alla directory del client sul computer client.  
  
4.  Eseguire `setup.bat client` sul client.Quando si esegue `setup.bat` con l'argomento `client` viene creato un certificato client denominato Client.com e il certificato client viene esportato in un file denominato Client.cer.  
  
5.  Nel file App.config del `MetadataResolverClient` sul computer client, modificare il valore dell'indirizzo dell'endpoint mex in modo che corrisponda al nuovo indirizzo del servizio.Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.Modificare inoltre l'occorrenza di "localhost" nel file metadataResolverClient.cs al nuovo nome del certificato del servizio \(il nome di dominio completo del server\).Eseguire la stessa operazione per il file App.config del progetto SvcutilClient.  
  
6.  Copiare il file Client.cer dalla directory del client alla directory del servizio sul server.  
  
7.  Eseguire `ImportServiceCert.bat` sul client.In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
8.  Eseguire `ImportClientCert.bat` sul server. In questo modo il certificato client viene importato dal file Client.cer nell'archivio LocalMachine \- TrustedPeople.  
  
9. Compilare il progetto di servizio in Visual Studio sul computer server e selezionare la pagina della Guida in un browser Web per verificare che sia in esecuzione.  
  
10. Eseguire MetadataResolverClient o SvcutilClient da VS sul computer client.  
  
    1.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
    > [!NOTE]
    >  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.Se sono stati eseguiti esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che utilizzano certificati in più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.A tale scopo, utilizzare il comando seguente: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`.Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Metadata\CustomMexEndpoint`  
  
## Vedere anche