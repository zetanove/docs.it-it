---
title: "Token di supporto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 65a8905d-92cc-4ab0-b6ed-1f710e40784e
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 29
---
# Token di supporto
L'esempio dei token di supporto illustra come aggiungere token aggiuntivi a un messaggio che utilizza WS\-Security.  L'esempio aggiunge un token di sicurezza binario X.509 e un token di sicurezza nome utente.  Il token viene passato in un'intestazione di un messaggio WS\-Security dal client al servizio e parte del messaggio viene firmata con la chiave privata associata al token di sicurezza X.509 per provare il possesso del certificato X.509 al destinatario.  Ciò è utile nel caso in cui vi sia un requisito di più richieste per autenticare o autorizzare il mittente associate a un messaggio.  Il servizio implementa un contratto che definisce un modello di comunicazione richiesta\/risposta.  
  
## Dimostrazione  
 L'esempio illustra quanto segue:  
  
-   Come un client può passare token di sicurezza aggiuntivi a un servizio.  
  
-   Come il server può accedere a richieste associate ai token di sicurezza aggiuntivi.  
  
-   Come viene usato il certificato X.509 del server per proteggere la chiave simmetrica usata per crittografare il messaggio e la firma.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
## Il client autentica con token nome utente e token di sicurezza X.509 di supporto  
 Il servizio espone un solo endpoint per comunicare con il servizio che viene creato a livello di codice utilizzando le classi `BindingHelper` e `EchoServiceHost`.  L'endpoint è costituito da un indirizzo, un'associazione e un contratto.  L'associazione è configurata con un'associazione personalizzata usando `SymmetricSecurityBindingElement` e `HttpTransportBindingElement`.  Questo esempio imposta `SymmetricSecurityBindingElement` per utilizzare un certificato X.509 del servizio per proteggere la chiave simmetrica durante la trasmissione e passare un `UserNameToken` insieme a un  `X509SecurityToken` di supporto in un'intestazione del messaggio WS\-Security.  La chiave simmetrica viene utilizzata per crittografare il corpo del messaggio e il token di sicurezza del nome utente.  Il token di supporto viene passato come un token di sicurezza binario aggiuntivo nell'intestazione del messaggio WS\-Security.  L'autenticità del token di supporto viene provata firmando parte del messaggio con la chiave privata associata con il token di sicurezza X.509 di supporto.  
  
```  
public static Binding CreateMultiFactorAuthenticationBinding()  
{  
    HttpTransportBindingElement httpTransport = new HttpTransportBindingElement();  
  
    // the message security binding element will be configured to require 2 tokens:  
    // 1) A username-password encrypted with the service token  
    // 2) A client certificate used to sign the message  
  
    // Instantiate a binding element that will require the username/password token in the message (encrypted with the server cert)  
    SymmetricSecurityBindingElement messageSecurity = SecurityBindingElement.CreateUserNameForCertificateBindingElement();  
  
    // Create supporting token parameters for the client X509 certificate.  
    X509SecurityTokenParameters clientX509SupportingTokenParameters = new X509SecurityTokenParameters();  
    // Specify that the supporting token is passed in message send by the client to the service  
    clientX509SupportingTokenParameters.InclusionMode = SecurityTokenInclusionMode.AlwaysToRecipient;  
    // Turn off derived keys  
    clientX509SupportingTokenParameters.RequireDerivedKeys = false;  
    // Augment the binding element to require the client's X509 certificate as an endorsing token in the message  
    messageSecurity.EndpointSupportingTokenParameters.Endorsing.Add(clientX509SupportingTokenParameters);  
  
    // Create a CustomBinding based on the constructed security binding element.  
    return new CustomBinding(messageSecurity, httpTransport);  
}  
  
```  
  
 Il comportamento specifica le credenziali del servizio che devono essere usate per l'autenticazione del client e anche informazioni sul certificato X.509 del servizio.  L'esempio utilizza `CN=localhost` come nome del soggetto nel certificato X.509 del servizio.  
  
```  
override protected void InitializeRuntime()  
{  
    // Extract the ServiceCredentials behavior or create one.  
    ServiceCredentials serviceCredentials =   
        this.Description.Behaviors.Find<ServiceCredentials>();  
    if (serviceCredentials == null)  
    {  
        serviceCredentials = new ServiceCredentials();  
        this.Description.Behaviors.Add(serviceCredentials);  
    }  
  
    // Set the service certificate  
    serviceCredentials.ServiceCertificate.SetCertificate(  
                                       "CN=localhost");  
  
/*  
Setting the CertificateValidationMode to PeerOrChainTrust means that if the certificate is in the Trusted People store, then it will be trusted without performing a validation of the certificate's issuer chain. This setting is used here for convenience so that the sample can be run without having to have certificates issued by a certification authority (CA).  
This setting is less secure than the default, ChainTrust. The security implications of this setting should be carefully considered before using PeerOrChainTrust in production code.  
*/  
    serviceCredentials.ClientCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
  
    // Create the custom binding and add an endpoint to the service.  
    Binding multipleTokensBinding =  
         BindingHelper.CreateMultiFactorAuthenticationBinding();  
    this.AddServiceEndpoint(typeof(IEchoService),   
                          multipleTokensBinding, string.Empty);  
    base.InitializeRuntime();  
}  
```  
  
 Codice del servizio  
  
```  
[ServiceBehavior(IncludeExceptionDetailInFaults = true)]  
public class EchoService : IEchoService  
{  
    public string Echo()  
    {  
        string userName;  
        string certificateSubjectName;  
        GetCallerIdentities(  
            OperationContext.Current.ServiceSecurityContext,   
            out userName,   
            out certificateSubjectName);  
            return String.Format("Hello {0}, {1}",   
                    userName, certificateSubjectName);  
    }  
  
    public void Dispose()  
    {  
    }  
  
    bool TryGetClaimValue<TClaimResource>(ClaimSet claimSet,   
            string claimType, out TClaimResource resourceValue)  
            where TClaimResource : class  
    {  
        resourceValue = default(TClaimResource);  
        IEnumerable<Claim> matchingClaims =   
            claimSet.FindClaims(claimType, Rights.PossessProperty);  
        if(matchingClaims == null)  
            return false;  
        IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();  
        if (enumerator.MoveNext())  
        {  
            resourceValue =   
              (enumerator.Current.Resource == null) ? null :   
              (enumerator.Current.Resource as TClaimResource);  
            return true;  
        }  
        else  
        {  
            return false;  
        }  
    }  
  
    // Returns the username and certificate subject name provided by   
    //the client  
    void GetCallerIdentities(ServiceSecurityContext   
        callerSecurityContext,   
        out string userName, out string certificateSubjectName)  
    {  
        userName = null;  
        certificateSubjectName = null;  
  
       // Look in all the claimsets in the authorization context  
       foreach (ClaimSet claimSet in   
               callerSecurityContext.AuthorizationContext.ClaimSets)  
       {  
            if (claimSet is WindowsClaimSet)  
            {  
                // Try to find a Name claim. This will have been   
                // generated from the windows username.  
                string tmpName;  
                if (TryGetClaimValue<string>(claimSet, ClaimTypes.Name,   
                                                      out tmpName))  
                {  
                    userName = tmpName;  
                }  
            }  
            else if (claimSet is X509CertificateClaimSet)  
            {  
                // Try to find an X500DisinguishedName claim. This will   
                // have been generated from the client certificate.  
                X500DistinguishedName tmpDistinguishedName;  
                if (TryGetClaimValue<X500DistinguishedName>(claimSet,   
                               ClaimTypes.X500DistinguishedName,   
                               out tmpDistinguishedName))  
                {  
                    certificateSubjectName = tmpDistinguishedName.Name;  
                }  
            }  
        }  
    }  
}   
```  
  
 L'endpoint del client viene configurato in modo simile all'endpoint del servizio.  Il client usa la stessa classe `BindingHelper` per creare un'associazione.  Il resto dell'installazione è situato nella classe `Client`.  Il client imposta informazioni sul token di sicurezza del nome utente, il token di sicurezza X.509 di supporto e informazioni sul certificato X.509 del servizio nel codice dell'installazione sulla raccolta dei comportamenti dell'endpoint del client.  
  
```  
 static void Main()  
 {  
     // Create the custom binding and an endpoint address for   
     // the service.  
     Binding multipleTokensBinding =   
         BindingHelper.CreateMultiFactorAuthenticationBinding();  
         EndpointAddress serviceAddress = new EndpointAddress(  
         "http://localhost/servicemodelsamples/service.svc");  
       ChannelFactory<IEchoService> channelFactory = null;  
       IEchoService client = null;  
  
       Console.WriteLine("Username authentication required.");  
       Console.WriteLine(  
         "Provide a valid machine or domain account. [domain\\user]");  
       Console.WriteLine("   Enter username:");  
       string username = Console.ReadLine();  
       Console.WriteLine("   Enter password:");  
       string password = "";  
       ConsoleKeyInfo info = Console.ReadKey(true);  
       while (info.Key != ConsoleKey.Enter)  
       {  
           if (info.Key != ConsoleKey.Backspace)  
           {  
               if (info.KeyChar != '\0')  
               {  
                   password += info.KeyChar;  
                }  
                info = Console.ReadKey(true);  
            }  
            else if (info.Key == ConsoleKey.Backspace)  
            {  
                if (password != "")  
                {  
                    password =   
                       password.Substring(0, password.Length - 1);  
                }  
                info = Console.ReadKey(true);  
            }  
         }  
         for (int i = 0; i < password.Length; i++)  
            Console.Write("*");  
         Console.WriteLine();  
         try  
         {  
           // Create a proxy with the previously create binding and   
           // endpoint address  
              channelFactory =   
                 new ChannelFactory<IEchoService>(  
                     multipleTokensBinding, serviceAddress);  
           // configure the username credentials, the client   
           // certificate and the server certificate on the channel   
           // factory   
           channelFactory.Credentials.UserName.UserName = username;  
           channelFactory.Credentials.UserName.Password = password;  
           channelFactory.Credentials.ClientCertificate.SetCertificate(  
           "CN=client.com", StoreLocation.CurrentUser, StoreName.My);  
              channelFactory.Credentials.ServiceCertificate.SetDefaultCertificate(  
           "CN=localhost", StoreLocation.LocalMachine, StoreName.My);  
           client = channelFactory.CreateChannel();  
           Console.WriteLine("Echo service returned: {0}",   
                                           client.Echo());  
  
           ((IChannel)client).Close();  
           channelFactory.Close();  
        }  
        catch (CommunicationException e)  
        {  
         Abort((IChannel)client, channelFactory);  
         // if there is a fault then print it out  
         FaultException fe = null;  
         Exception tmp = e;  
         while (tmp != null)  
         {  
            fe = tmp as FaultException;  
            if (fe != null)  
            {  
                break;  
            }  
            tmp = tmp.InnerException;  
        }  
        if (fe != null)  
        {  
           Console.WriteLine("The server sent back a fault: {0}",   
         fe.CreateMessageFault().Reason.GetMatchingTranslation().Text);  
        }  
        else  
        {  
         Console.WriteLine("The request failed with exception: {0}",e);  
        }  
    }  
    catch (TimeoutException)  
    {  
        Abort((IChannel)client, channelFactory);  
        Console.WriteLine("The request timed out");  
    }  
    catch (Exception e)  
    {  
         Abort((IChannel)client, channelFactory);  
          Console.WriteLine(  
          "The request failed with unexpected exception: {0}", e);  
    }  
    Console.WriteLine();  
    Console.WriteLine("Press <ENTER> to terminate client.");  
    Console.ReadLine();  
}  
```  
  
## Visualizzazione delle informazioni sul chiamante  
 Per visualizzare le informazioni sul chiamante è possibile utilizzare `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` come mostra il codice seguente.  `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` contiene attestazioni di autorizzazione associate al chiamante corrente.  Tali richieste vengono fornite automaticamente da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per ogni token ricevuto nel messaggio.  
  
```  
bool TryGetClaimValue<TClaimResource>(ClaimSet claimSet, string   
                         claimType, out TClaimResource resourceValue)  
    where TClaimResource : class  
{  
    resourceValue = default(TClaimResource);  
    IEnumerable<Claim> matchingClaims =   
    claimSet.FindClaims(claimType, Rights.PossessProperty);  
    if (matchingClaims == null)  
          return false;  
    IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();  
    if (enumerator.MoveNext())  
    {  
        resourceValue = (enumerator.Current.Resource == null) ? null : (enumerator.Current.Resource as TClaimResource);  
        return true;  
    }  
    else  
    {  
         return false;  
    }  
}  
  
// Returns the username and certificate subject name provided by the client  
void GetCallerIdentities(ServiceSecurityContext callerSecurityContext, out string userName, out string certificateSubjectName)  
{  
    userName = null;  
    certificateSubjectName = null;  
  
    // Look in all the claimsets in the authorization context  
    foreach (ClaimSet claimSet in   
      callerSecurityContext.AuthorizationContext.ClaimSets)  
    {  
        if (claimSet is WindowsClaimSet)  
        {  
            // Try to find a Name claim. This will have been generated   
            //from the windows username.  
            string tmpName;  
            if (TryGetClaimValue<string>(claimSet, ClaimTypes.Name,   
                                                     out tmpName))  
            {  
                userName = tmpName;  
            }  
        }  
        else if (claimSet is X509CertificateClaimSet)  
         {  
            //Try to find an X500DisinguishedName claim.   
            //This will have been generated from the client   
            //certificate.  
            X500DistinguishedName tmpDistinguishedName;  
            if (TryGetClaimValue<X500DistinguishedName>(claimSet,   
               ClaimTypes.X500DistinguishedName,   
               out tmpDistinguishedName))  
            {  
                    certificateSubjectName = tmpDistinguishedName.Name;  
            }  
        }  
    }  
}  
```  
  
## Esecuzione dell'esempio  
 Quando si esegue l'esempio, il client innanzitutto richiede nome utente e password per il token del nome utente.  Assicurarsi di fornire valori corretti per l'account del sistema, perché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nel servizio esegue il mapping dei valori forniti nel token del nome utente nell'identità fornita dal sistema.  Successivamente, il client visualizza la risposta del servizio.  Premere INVIO nella finestra del client per arrestare il client.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso in questo esempio consente di configurare il server con i certificati attinenti per eseguire un'applicazione ospitata su Internet Information Services \(IIS\) che richiede sicurezza server basata su certificato.  Questo file batch deve essere modificato per funzionare tra più computer o in caso di applicazioni indipendenti.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
### Creazione del certificato del client  
 Le righe seguenti del file batch Setup.bat creano il certificato client da utilizzare.  La variabile `%CLIENT_NAME%` specifica l'oggetto del certificato client.  Questo esempio utilizza "client.com" come nome del soggetto.  
  
 Il certificato viene memorizzato nell'archivio personale nel percorso di archivio `CurrentUser`.  
  
```  
echo ************  
echo making client cert  
echo ************  
makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
```  
  
### Installazione del certificato client nell'archivio certificati attendibili del server:  
 La riga seguente nel file batch Setup.bat copia il certificato client nell'archivio delle persone attendibili del server.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema server.  Se è già disponibile un certificato con radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio del popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
```  
echo ************  
echo copying client cert to server's CurrentUserstore  
echo ************  
certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople  
```  
  
### Creazione del certificato del server:  
 Le righe seguenti del file batch Setup.bat creano il certificato server da usare.  La variabile `%SERVER_NAME%`  specifica il nome del server.  Modificare questa variabile per specificare nome del server.  Il valore predefinito in questo file batch è localhost.  
  
 Il certificato viene memorizzato nell'archivio personale nel percorso di archivio LocalMachine.  Il certificato viene archiviato nell'archivio LocalMachine per i servizi ospitati su IIS.  Per i servizi indipendenti, è necessario modificare il file batch per archiviare il certificato server nel percorso dell'archivio CurrentUser sostituendo la stringa LocalMachine con CurrentUser.  
  
```  
echo ************  
echo Server cert setup starting  
echo %SERVER_NAME%  
echo ************  
echo making server cert  
echo ************  
makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
```  
  
### Installazione del certificato server nell'archivio certificati attendibili del client:  
 Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.  Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.  Se è già disponibile un certificato con radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio del popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
```  
echo ************  
echo copying server cert to client's TrustedPeople store  
echo ************certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
```  
  
### Abilitare l'accesso alla chiave privata del certificato  
 Per abilitare l'accesso alla chiave privata del certificato dal servizio ospitato su IIS, è necessario concedere le autorizzazioni alla chiave privata appropriate all'account utente con cui viene eseguito il processo ospitato da IIS.  Questa operazione viene eseguita negli ultimi passaggi dello script Setup.bat.  
  
```  
echo ************  
echo setting privileges on server certificates  
echo ************  
for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
(ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
iisreset  
```  
  
##### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni seguenti.  
  
##### Per eseguire l'esempio sullo stesso computer  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.  In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.  Assicurarsi di rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio.  Negli altri esempi relativi alla sicurezza vengono usati gli stessi certificati.  
  
2.  Avviare Client.exe da \\client\\bin.  L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
3.  Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
##### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio.  Crea un'applicazione virtuale denominata servicemodelsamples per questa directory utilizzando lo strumento di gestione di Internet Information Services \(IIS\).  
  
2.  Copiare i file del programma del servizio da \\inetpub\\wwwroot\\servicemodelsamples alla directory virtuale sul computer del servizio.  Assicurarsi di copiare i file nella sottodirectory \\bin  Copiare anche i file Setup.bat, Cleanup.bat e ImportClientCert.bat nel computer del servizio.  
  
3.  Creare una directory sul client del servizio per i file binari del client.  
  
4.  Copiare i file di programma del client nella directory del client sul computer del client  e i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel client.  
  
5.  Sul server aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire `setup.bat service`.  Quando si esegue `setup.bat` ``  con l'argomento `service` viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service.cer.  
  
6.  Modificare Web.config per riflettere il nuovo nome del certificato \(nell'attributo `findValue` dell'[\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) che corrisponde al nome di dominio completo del computer.  
  
7.  Copiare il file Service.cer dalla directory del servizio alla directory del client sul computer client.  
  
8.  Sul client aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire `setup.bat client`.  L'esecuzione di `setup.bat` con l'argomento `client` crea un certificato client denominato client.com ed esporta il certificato client in un file denominato Client.cer.  
  
9. Nel file Client.exe.config nel computer client, modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.  
  
10. Copiare il file Client.cer dalla directory del client nella directory del servizio sul server.  
  
11. Nel client, eseguire ImportServiceCert.bat.  In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser \- TrustedPeople.  
  
12. Eseguire sul server ImportClientCert.bat. In questo modo il certificato client viene importato dal file Client.cer nell'archivio LocalMachine \- TrustedPeople.  
  
13. Sul computer client, avviare Client.exe da una finestra del prompt dei comandi.  Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
##### Per eseguire la pulizia dopo l'esempio  
  
-   Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
> [!NOTE]
>  Questo script non rimuove i certificati del servizio su un client quando si esegue questo esempio tra più computer.  Se sono stati eseguiti esempi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che utilizzano certificati in più computer, verificare di cancellare i certificati del servizio installati nell'archivio CurrentUser \- TrustedPeople.  Per eseguire questa operazione, usare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
## Vedere anche