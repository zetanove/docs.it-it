---
title: "Sicurezza dei messaggi anonima | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "WS-Security"
ms.assetid: c321cbf9-8c05-4cce-b5a5-4bf7b230ee03
caps.latest.revision: 52
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 52
---
# Sicurezza dei messaggi anonima
Nell'esempio relativo alla sicurezza dei messaggi anonima viene illustrato come implementare un'applicazione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che usa la sicurezza a livello di messaggi senza autenticazione del client, ma che richiede l'autenticazione del server usando il certificato X.509 del server.  Tutti i messaggi dell'applicazione tra il client e il server vengono firmati e crittografati.  Questo esempio è basato sull'esempio [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md).  Questo esempio è costituito da un programma di console client \(.exe\) e da una libreria di servizi \(.dll\) ospitati da Internet Information Services \(IIS\).  Il servizio implementa un contratto che definisce un modello di comunicazione richiesta\/risposta.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Questo esempio aggiunge una nuova operazione all'interfaccia della calcolatrice che restituisce `True` se il client non viene autenticato.  
  
```  
public class CalculatorService : ICalculator  
{  
    public bool IsCallerAnonymous()  
    {  
        // ServiceSecurityContext.IsAnonymous returns true if the caller is not authenticated.  
        return ServiceSecurityContext.Current.IsAnonymous;  
    }  
    ...  
}  
  
```  
  
 Il servizio espone un solo endpoint per comunicare con il servizio che viene definito mediante un file di configurazione \(Web.config\).  L'endpoint è costituito da un indirizzo, un'associazione e un contratto.  L'associazione viene configurata con un'associazione `wsHttpBinding`.  La modalità di sicurezza predefinita per l'associazione `wsHttpBinding` è `Message`.  L'attributo `clientCredentialType` è impostato su `None`.  
  
```  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
     <!--   
     <!--This configuration defines the security mode as Message and-->  
     <!--the clientCredentialType as None. This mode provides -- >  
     <!--server authentication only using the service certificate.-->  
  
     <binding>  
       <security mode="Message">  
         <message clientCredentialType="None" />  
       </security>  
     </binding>  
    </wsHttpBinding>  
  </bindings>  
  ...  
</system.serviceModel>  
```  
  
 Le credenziali da usare per l'autenticazione del servizio vengono specificate nell'[\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md).  Il `SubjectName` del certificato server deve contenere lo stesso valore di quello specificato per l'attributo `findValue`, come illustrato nell'esempio di codice seguente.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior>  
      <!--   
    The serviceCredentials behavior allows you to define a service certificate.  
    A service certificate is used by a client to authenticate the service and provide message protection.  
    This configuration references the "localhost" certificate installed during the setup instructions.  
    -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
      </serviceCredentials>  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
 La configurazione dell'endpoint client è costituita da un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto.  La modalità di sicurezza del client per l'associazione `wsHttpBinding` è `Message`.  L'attributo `clientCredentialType` è impostato su `None`.  
  
```  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
             address="http://localhost/servicemodelsamples/service.svc"   
             binding="wsHttpBinding"   
             behaviorConfiguration="ClientCredentialsBehavior"  
             bindingConfiguration="Binding1"   
             contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <!--This configuration defines the security mode as -->  
      <!--Message and the clientCredentialType as None. -->  
      <binding name="Binding1">  
        <security mode = "Message">  
          <message clientCredentialType="None"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>   
  ...  
</system.serviceModel>  
```  
  
 L'esempio imposta <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> su <xref:System.ServiceModel.Security.X509CertificateValidationMode> per l'autenticazione del certificato del servizio.  Questa operazione viene eseguita nel file App.config del client, nella sezione `behaviors`.  Questo significa che se il certificato si trova nell'archivio Persone attendibili, viene considerato attendibili senza eseguire la convalida della catena di emittenti del certificato.  Questa impostazione viene usata nell'esempio per comodità, in modo che possa essere eseguito senza richiedere certificati emessi da un'autorità di certificazione \(CA\).  Questa impostazione è meno protetta dell'impostazione predefinita, ChainTrust.  Le implicazioni di sicurezza di questa impostazione devono essere considerate attentamente prima di usare `PeerOrChainTrust` nel codice di produzione.  
  
 L'implementazione del client aggiunge una chiamata al metodo `IsCallerAnonymous` e solo per questo si differenzia dall'esempio [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md).  
  
```  
// Create a client with a client endpoint configuration.  
CalculatorClient client = new CalculatorClient();  
  
// Call the GetCallerIdentity operation.  
Console.WriteLine("IsCallerAnonymous returned: {0}", client.IsCallerAnonymous());  
  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
...  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
Console.WriteLine();  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Premere INVIO nella finestra del client per arrestare il client.  
  
```  
IsCallerAnonymous returned: True  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
  
```  
  
 Il file batch Setup.bat incluso nell'esempio relativo alla sicurezza dei messaggi anonima consente di configurare il server con un certificato attinente per eseguire un'applicazione ospitata che richiede sicurezza server basata su certificato.  Il file batch può essere eseguito in due modalità.  Per eseguire il file batch in un solo computer, digitare `setup.bat` nella riga di comando.  Per eseguirlo in modalità di servizio, digitare `setup.bat service`.  Usare questa modalità quando si esegue l'esempio tra più computer.  Per altre informazioni, vedere la procedura di configurazione alla fine di questo argomento.  
  
 Gli elementi seguenti forniscono una breve panoramica delle diverse sezioni dei file batch:  
  
-   Creazione del certificato server.  
  
     Le righe seguenti del file batch Setup.bat creano il certificato server da usare.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     La variabile %SERVER\_NAME% specifica il nome del server.  Il certificato viene archiviato nell'archivio LocalMachine.  Se il file batch di installazione viene eseguito con un argomento di servizio, ad esempio `setup.bat service`, la variabile %SERVER\_NAME% conterrà il nome di dominio completo del computer.  In caso contrario, viene usata l'impostazione predefinita localhost.  
  
-   Installazione del certificato server nell'archivio certificati attendibili del client.  
  
     La riga seguente copia il certificato server nell'archivio Persone attendibili del client.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.  Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
  
    ```  
  
-   Concessione delle autorizzazioni sulla chiave privata del certificato.  
  
     Le righe seguenti de file batch Setup.bat rendono il certificato server archiviato nell'archivio LocalMachine accessibile all'account del processo di lavoro [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
    ```  
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%MSSDK%\bin\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr "5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
  
    ```  
  
> [!NOTE]
>  Se si usa una versione in lingua diversa dall'inglese \(Stati Uniti\)  di Windows, è necessario modificare il file Setup.bat e sostituire il nome dell'account `NT AUTHORITY\NETWORK SERVICE` con l'equivalente locale.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
### Per eseguire l'esempio nello stesso computer  
  
1.  Assicurarsi che il percorso includa la cartella in cui sono situati Makecert.exe e FindPrivateKey.exe.  
  
2.  Aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.  In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch di installazione è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  e richiede che la variabile di ambiente PATH punti alla directory in cui è installato SDK.  Questa variabile di ambiente viene impostata automaticamente in un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
3.  Verificare l'accesso al servizio immettendo l'indirizzo http:\/\/localhost\/servicemodelsamples\/service.svc in un browser.  
  
4.  Avviare Client.exe da \\client\\bin.  L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
5.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio.  Creare un'applicazione virtuale denominata servicemodelsamples per questa directory usando lo strumento di gestione di Internet Information Services \(IIS\).  
  
2.  Copiare i file del programma del servizio da \\inetpub\\wwwroot\\servicemodelsamples nella directory virtuale sul computer del servizio.  Assicurarsi di copiare i file nella sottodirectory \\bin  Copiare i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
3.  Creare una directory sul client del servizio per i file binari del client.  
  
4.  Copiare i file di programma del client nella directory del client sul computer relativo  e i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel client.  
  
5.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire `setup.bat service`.  Quando si esegue `setup.bat` con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
6.  Modificare Web.config per riflettere il nuovo nome del certificato \(nell'attributo `findValue` in [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) che corrisponde al nome di dominio completo del computer.  
  
7.  Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.  
  
8.  Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  
  
9. Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire ImportServiceCert.bat.  In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
10. Sul computer client avviare Client.exe da un prompt dei comandi.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi dopo che l'esempio è stato completato.  
  
> [!NOTE]
>  Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.  Se sono stati eseguiti esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che usano certificati tra più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.  Per eseguire questa operazione, usare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`  
  
## Vedere anche