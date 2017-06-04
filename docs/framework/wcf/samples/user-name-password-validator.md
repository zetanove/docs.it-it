---
title: "Validator del nome utente e password | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f03841-286b-42d8-ba58-18c75422bc8e
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Validator del nome utente e password
In questo esempio viene illustrato come implementare un validator di UserNamePassword personalizzato.Questo processo è utile nei casi in cui nessuna delle modalità di convalida UserNamePassword incorporate è appropriata per i requisiti dell'applicazione; ad esempio, quando le coppie di nome utente\/password sono archiviate in un archivio esterno, ad esempio un database.In questo esempio viene illustrato un servizio con un validator personalizzato che verifica due particolari coppie di nome utente\/password.Il cliente utilizza tale coppia di nome utente\/password per l'autenticazione nel servizio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Security\UserNamePasswordValidator`  
  
> [!NOTE]
>  Poiché chiunque può costruire una credenziale Username che utilizza le coppie di nome utente\/password accettate dal validator personalizzato, il servizio è meno affidabile rispetto al comportamento predefinito fornito dal validator UserNamePassword standard.Il validator UserNamePassword standard tenta di eseguire il mapping della coppia di nome utente\/password fornita a un account di Windows e se questo mapping non riesce, l'autenticazione ha esito negativo.Il validator UserNamePassword personalizzato in questo esempio non deve essere utilizzato nel codice di produzione, poiché è concepito per solo scopo illustrativo.  
  
 In sintesi, nell'esempio viene illustrato in che modo eseguire le operazioni seguenti:  
  
-   Il client può essere autenticato utilizzando un token Username.  
  
-   Il server convalida le credenziali client in relazione a un UserNamePasswordValidator personalizzato e il modo in cui vengono propagati gli errori personalizzati dipende dalla logica di convalida del nome utente e della password nel client.  
  
-   Il server viene autenticato tramite il certificato X.509 del server.  
  
 Il servizio espone un solo endpoint per comunicare con il servizio che viene definito mediante il file di configurazione App.config.L'endpoint è costituito da un indirizzo, un'associazione e un contratto.L'associazione viene configurata con una classe `wsHttpBinding` standard per la quale è previsto l'utilizzo predefinito dell'autenticazione WS\-Securitye del nome utente.Il comportamento del servizio specifica la modalità `Custom` per la convalida delle coppie nome utente\/password client insieme al tipo di classe del validator.Il comportamento specifica inoltre il certificato server mediante l'elemento `serviceCertificate`.Il certificato server deve contenere per la proprietà `SubjectName` lo stesso valore dell'attributo `findValue` in [\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).  
  
```  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
      <!-- use host/baseAddresses to configure base address provided by host -->  
      <host>  
        <baseAddresses>  
          <add baseAddress ="http://localhost:8001/servicemodelsamples/service" />  
        </baseAddresses>  
      </host>  
      <!-- use base address specified above, provide one endpoint -->  
      <endpoint address="username"  
                binding="wsHttpBinding"  
                bindingConfiguration="Binding"   
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- username binding -->  
      <binding name="Binding">  
        <security mode="Message">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <serviceDebug includeExceptionDetailInFaults ="true"/>  
        <serviceCredentials>  
          <!--   
          The serviceCredentials behavior allows one to   
          specify a custom validator for username/password  
          combinations.  
          -->  
          <userNameAuthentication userNamePasswordValidationMode="Custom"  
                                  customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService+MyCustomUserNameValidator, service" />  
          <!--   
          The serviceCredentials behavior allows one to define a service certificate. A service certificate is used by a client to authenticate the service and provide message protection. You must specify a server certificate when passing username/passwords to encrypt the information as it is sent on the wire. Otherwise the username and password information would be sent as clear text. This configuration references the "localhost" certificate installed during the setup instructions.  
          -->  
          <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
        </serviceCredentials>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
```  
  
 La configurazione dell'endpoint client è costituita da un nome di configurazione, un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto.L'associazione client viene configurata con la modalità e il `clientCredentialType` del messaggio appropriati.  
  
```  
<system.serviceModel>  
  
    <client>  
      <!-- Username based endpoint -->  
      <endpoint name="Username"  
address="http://localhost:8001/servicemodelsamples/service/username"   
                binding="wsHttpBinding"   
                bindingConfiguration="Binding"   
                behaviorConfiguration="ClientCertificateBehavior"  
                contract="Microsoft.ServiceModel.Samples.ICalculator">  
      </endpoint>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!-- Username binding -->  
        <binding name="Binding">  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="ClientCertificateBehavior">  
          <clientCredentials>  
            <serviceCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </serviceCertificate>  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
```  
  
 L'implementazione client richiede all'utente di immettere un nome utente e una password.  
  
```  
// Get the username and password  
Console.WriteLine("Username authentication required.");  
Console.WriteLine("Provide a username.");  
Console.WriteLine("   Enter username: (test1)");  
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
            password = password.Substring(0, password.Length - 1);  
        }  
        info = Console.ReadKey(true);  
    }  
}  
for (int i = 0; i < password.Length; i++)  
{  
    Console.Write("*");  
}  
Console.WriteLine();  
// Create a proxy with Certificate endpoint configuration  
CalculatorProxy proxy = new CalculatorProxy("Username")  
try  
{  
  proxy.ClientCredentials.Username.Username = username;  
  proxy.ClientCredentials.Username.Password = password;  
    // Call the Add service operation.  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
    double result = proxy.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  }  
  catch (Exception e)  
  {  
      Console.WriteLine("Call failed:");  
      while (e != null)  
      {  
          Console.WriteLine("\t{0}", e.Message);  
          e = e.InnerException;  
      }  
      proxy.Abort();  
  }  
}  
  
```  
  
 In questo esempio viene utilizzato un UserNamePasswordValidator personalizzato per convalidare le coppie di nome utente\/password.Nell'esempio viene implementato `CustomUserNamePasswordValidator`, derivato da <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>.Per ulteriori informazioni, vedere la documentazione di <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>.In questo particolare esempio del validator personalizzato viene implementato il metodo `Validate` per accettare due specifiche coppie di nome utente\/password, come illustrato nel codice seguente.  
  
```  
public class CustomUserNameValidator : UserNamePasswordValidator  
{  
 // This method validates users. It allows in two users,   
 // test1 and test2 with passwords 1tset and 2tset respectively.  
 // This code is for illustration purposes only and   
 // MUST NOT be used in a production environment because it   
 // is NOT secure.  
 public override void Validate(string userName, string password)  
 {  
  if (null == userName || null == password)  
  {  
   throw new ArgumentNullException();  
  }  
  
  if (!(userName == "test1" && password == "1tset") && !(userName == "test2" && password == "2tset"))  
  {  
   throw new FaultException("Unknown Username or Incorrect Password");  
   }  
  }  
 }  
```  
  
 Quando il validator è stato implementato nel codice del servizio, l'host del servizio deve essere informato dell'istanza del validator da utilizzare.Questa operazione viene eseguita tramite il codice seguente.  
  
```  
serviceHost.Credentials.UserNameAuthentication.UserNamePasswordValidationMode = UserNamePasswordValidationMode.Custom;  
serviceHost.Credentials. UserNameAuthentication.CustomUserNamePasswordValidator = new CustomUserNamePasswordValidator();  
```  
  
 In alternativa, è possibile eseguire la stessa operazione nella configurazione come segue.  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="CalculatorServiceBehavior">  
  ...  
   <serviceCredentials>  
    <!--   
    The serviceCredentials behavior allows one to specify authentication constraints on username / password combinations.  
    -->  
    <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService+CustomUserNameValidator, service" />  
   ...  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Il client deve chiamare correttamente tutti i metodi.Premere INVIO nella finestra del client per arrestare il client.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso con questo esempio consente di configurare il server con i certificati attinenti per eseguire un'applicazione indipendente che richiede la sicurezza server basata su certificato.Questo file batch deve essere modificato per funzionare su computer diversi o per operare in un contesto non indipendente.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
-   Creazione del certificato del server:  
  
     Le righe seguenti del file batch Setup.bat creano il certificato server da utilizzare.La variabile %SERVER\_NAME% specifica il nome del server.Modificare questa variabile per specificare il nome del server.Il valore predefinito è localhost.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
  
    ```  
  
-   Installazione del certificato server nell'archivio certificati attendibili del client:  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio delle persone attendibili del client.Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio della popolazione dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### Per impostare e compilare l'esempio  
  
1.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni seguenti.  
  
#### Per eseguire l'esempio sullo stesso computer  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] ed eseguire Setup.bat dalla cartella di installazione di esempio.In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.  
  
2.  Avviare Service.exe da service\\bin.  
  
3.  Avviare Client.exe da \\client\\bin.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio per i file binari del servizio.  
  
2.  Copiare i file di programma del servizio nella directory del servizio all'interno del computer del servizio.Copiare anche i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
3.  È necessario disporre di un certificato server con il nome del soggetto che contiene il nome di dominio completo del computer.Il file di configurazione per il server deve essere aggiornato per riflettere il nome del nuovo certificato.  
  
4.  Copiare il certificato server nell'archivio CurrentUser\-TrustedPeople del client.Questo passaggio è necessario solo se il certificato server non è emesso da un'autorità emittente attendibile.  
  
5.  Nel file App.config sul computer del servizio, modificare il valore dell'indirizzo di base per specificare un nome del computer completo anziché localhost.  
  
6.  Nel computer del servizio, avviare Service.exe da una finestra del prompt dei comandi.  
  
7.  Copiare i file del programma client dalla cartella \\client\\bin\\, nella cartella specifica del linguaggio, al computer client.  
  
8.  Nel file Client.exe.config nel computer client, modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  
  
9. Sul computer client, avviare Client.exe da una finestra del prompt dei comandi.  
  
10. Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.In questo modo il certificato del server viene rimosso dall'archivio certificati.  
  
## Vedere anche