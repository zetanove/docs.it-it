---
title: "Esempio sulla sicurezza dei messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82444166-6288-493a-85d4-85f43f134d19
caps.latest.revision: 33
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 33
---
# Esempio sulla sicurezza dei messaggi
In questo esempio viene illustrato come implementare un'applicazione che utilizza `basicHttpBinding` e la sicurezza del messaggio.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 La modalità di sicurezza di `basicHttpBinding` può essere impostata sui valori seguenti: `Message`, `Transport`, `TransportWithMessageCredential`, `TransportCredentialOnly` e `None`.Nell'esempio seguente il file App.config, la definizione dell'endpoint specifica l'`basicHttpBinding` e fa riferimento a una configurazione di associazione denominata `Binding1`, come mostra la configurazione di esempio seguente:  
  
```  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- This endpoint is exposed at the base address provided by -->  
     <!-- host: http://localhost:8000/ServiceModelSamples/service.-->  
     <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>   …  
</system.serviceModel>  
```  
  
 La configurazione dell'associazione imposta l'attributo `mode` di [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md) su `Message` e imposta l'attributo `clientCredentialType` di [\<messaggio\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-basichttpbinding.md) su `Certificate` come mostrato nel seguente esempio di configurazione:  
  
```  
<bindings>  
  <basicHttpBinding>  
    <!--   
        This configuration defines the SecurityMode as Message and   
        the clientCredentialType as Certificate.  
        -->  
    <binding name="Binding1" >  
      <security mode = "Message">  
        <message clientCredentialType="Certificate"/>  
      </security>  
    </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 Il certificato utilizzato dal servizio per l'autenticazione con il client è impostato nella sezione comportamenti del file di configurazione sotto l'elemento `serviceCredentials`.Anche la modalità di convalida applicata al certificato utilizzato dal servizio per l'autenticazione con il client è impostata nella sezione comportamenti del file di configurazione sotto l'elemento `clientCertificate`.  
  
```  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
      <!--The serviceCredentials behavior allows one to define a -->  
      <!--service certificate. A service certificate is used by a -->  
      <!--client to authenticate the service and provide message -->  
      <!-- protection. This configuration references the "localhost"-->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost"  
               storeLocation="LocalMachine"   
               storeName="My" x509FindType="FindBySubjectName" />  
        <clientCertificate>  
          <!-- Setting the certificateValidationMode to -->  
          <!-- PeerOrChainTrust means that if the certificate -->  
          <!--is in the user's Trusted People store, then it is -->  
          <!-- trusted without performing a validation of the -->  
          <!-- certificate's issuer chain. This setting is used -->  
          <!-- here for convenience so that the sample can be run -->  
          <!-- without having to have certificates issued by a -->  
          <!-- certification authority (CA). -->  
          <!-- This setting is less secure than the default, -->  
          <!-- ChainTrust. The security implications of this -->  
          <!-- setting should be carefully considered before using -->  
          <!-- PeerOrChainTrust in production code. -->  
          <authentication   
                       certificateValidationMode="PeerOrChainTrust" />  
        </clientCertificate>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Gli stessi dettagli sull'associazione e la sicurezza sono specificati nel file di configurazione del client.  
  
 L'identità del chiamante viene visualizzata nella finestra della console del servizio utilizzando il codice seguente:  
  
```  
Console.WriteLine("Called by {0}", ServiceSecurityContext.Current.PrimaryIdentity.Name);  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
### Per eseguire l'esempio nello stesso computer  
  
1.  Eseguire Setup.bat dalla cartella di installazione dell'esempio.In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di Windows SDK.e richiede che la variabile di ambiente MSSDK punti alla directory in cui è installato SDK.Questa variabile di ambiente viene impostata automaticamente all'interno di un prompt dei comandi di SDK di Windows.  
  
2.  Eseguire l'applicazione di servizio da \\service\\bin.  
  
3.  Eseguire l'applicazione client da \\client\\bin.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
5.  Rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.Gli altri esempi relativi alla sicurezza utilizzano gli stessi certificati.  
  
### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio per i file binari del servizio.  
  
2.  Copiare i file di programma del servizio nella directory del server.Copiare anche i file Setup.bat, Cleanup.bat e ImportClientCert.bat nel server.  
  
3.  Creare una directory sul client del servizio per i file binari del client.  
  
4.  Copiare i file di programma del client nella directory del client sul computer del clientCopiare anche i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel computer del client.  
  
5.  Nel server eseguire `setup.bat service`.L'esecuzione di `setup.bat`  con l'argomento `service` crea un certificato del servizio con il nome di dominio completo del computer ed esporta il certificato del servizio in un file denominato Service.cer.  
  
6.  Modificare Service.exe.config per riflettere il nuovo nome del certificato \(nell'attributo `findValue` dell'elemento [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) che corrisponde al nome di dominio completo del computer.Modificare anche il valore dell'indirizzo di base e specificare un nome di computer completo anziché localhost`.`  
  
7.  Copiare il file Service.cer dalla directory del servizio alla directory del client sul computer client.  
  
8.  Eseguire `setup.bat client` sul client.L'esecuzione di `setup.bat`  con l'argomento `client` crea un certificato client denominato Client.com ed esporta il certificato client in un file denominato Client.cer.  
  
9. Nel file Client.exe.config nel computer client, modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.Modificare anche l'attributo `findValue` di [\<certificatoPredefinito\>](../../../../docs/framework/configure-apps/file-schema/wcf/defaultcertificate-element.md) nel nuovo nome del certificato del servizio che corrisponde al nome di dominio completo del computer sul server.  
  
10. Copiare il file Client.cer dalla directory del client alla directory del servizio sul server.  
  
11. Nel client, eseguire ImportServiceCert.bat.In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
12. Eseguire ImportClientCert.bat sul server. In questo modo il certificato client viene importato dal file Client.cer nell'archivio LocalMachine \- TrustedPeople.  
  
13. Sul computer del servizio, eseguire Service.exe da un prompt dei comandi.  
  
14. Sul computer client, avviare Client.exe da una finestra del prompt dei comandi.  
  
    1.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
    > [!NOTE]
    >  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.Se sono stati eseguiti esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che utilizzano certificati tra più computer, assicurarsi di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.Per eseguire questa operazione, utilizzare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Binding\Basic\MessageSecurity`  
  
## Vedere anche