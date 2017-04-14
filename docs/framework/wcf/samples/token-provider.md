---
title: "Provider di token | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 947986cf-9946-4987-84e5-a14678d96edb
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# Provider di token
Questo esempio dimostra come implementare un provider di token personalizzato.In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] un provider di token viene utilizzato per fornire credenziali all'infrastruttura di sicurezza.In generale, il provider di token esamina la destinazione ed emette credenziali adatte in modo che l'infrastruttura di sicurezza possa salvaguardare il messaggio.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene fornito con il provider di token di Gestione credenziali predefinito.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene anche fornito con un provider di token [!INCLUDE[infocard](../../../../includes/infocard-md.md)].I provider di token personalizzati sono utili nei casi seguenti:  
  
-   Se è disponibile un archivio di credenziali con cui questi provider di token non sono in grado di operare.  
  
-   Se si vuole fornire un meccanismo personalizzato per la trasformazione delle credenziali dal punto in cui l'utente fornisce i dettagli a quello in cui il framework client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le credenziali.  
  
-   Se si sta compilando un token personalizzato.  
  
 Questo esempio illustra come compilare un provider di token personalizzato che trasforma l'input dell'utente in un formato diverso.  
  
 Per riassumere, questo esempio illustra quanto segue.  
  
-   Come un client può eseguire l'autenticazione utilizzando un nome utente e una password.  
  
-   Come è possibile configurare un client con un provider personalizzato.  
  
-   Come il server può convalidare le credenziali client utilizzando una password con una classe personalizzato <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> personalizzata che convalida la corrispondenza tra nome utente e password.  
  
-   Come viene autenticato il servizio dal client mediante il certificato X.509 del server.  
  
 Questo esempio mostra anche come l'identità del chiamante sia accessibile dopo il processo di autenticazione del token personalizzato.  
  
 Il servizio espone un solo endpoint per comunicare con il servizio che viene definito mediante il file di configurazione App.config.L'endpoint è costituito da un indirizzo, un'associazione e un contratto.L'associazione viene configurata con una classe `wsHttpBinding` standard, per la quale è impostata l'autenticazione dei messaggi come predefinita.In questo esempio viene impostata la classe `wsHttpBinding` standard per utilizzare l'autenticazione del nome utente del client.Il servizio configura anche il certificato del servizio utilizzando il comportamento serviceCredentials.Il comportamento serviceCredentials consente di configurare il certificato del servizio.Un certificato di servizio viene utilizzato da un client per autenticare il servizio e fornire protezione al messaggio.La configurazione seguente fa riferimento al certificato localhost installato durante l'installazione dell'esempio come descritto nelle istruzioni seguenti.  
  
```  
<system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <host>  
          <baseAddresses>  
            <!-- configure base address provided by host -->  
            <add baseAddress ="http://localhost:8000/servicemodelsamples/service"/>  
          </baseAddresses>  
        </host>  
        <!-- use base address provided by host -->  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  bindingConfiguration="Binding1"   
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      </service>  
    </services>  
  
    <bindings>  
      <wsHttpBinding>  
        <binding name="Binding1">  
          <security mode="Message">  
            <message clientCredentialType="UserName" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by a client to authenticate the service and provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
  
```  
  
 La configurazione dell'endpoint client è costituita da un nome di configurazione, un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto.L'associazione client viene configurata con la `Mode` e il `clientCredentialType` del messaggio appropriati.  
  
```  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
              address="http://localhost:8000/servicemodelsamples/service"   
              binding="wsHttpBinding"   
              bindingConfiguration="Binding1"   
              contract="Microsoft.ServiceModel.Samples.ICalculator">  
    </endpoint>  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <binding name="Binding1">  
        <security mode="Message">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
</system.serviceModel>  
```  
  
 I passaggi seguenti illustrano come sviluppare un provider di token personalizzato e integrarlo nel framework di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
1.  Scrivere un provider di token personalizzati.  
  
     L'esempio implementa un provider di token personalizzato che ottiene nome utente e password.La password deve corrispondere al nome utente.Questo provider di token personalizzato è a mero scopo esemplificativo e non si consiglia di distribuirlo.  
  
     Per eseguire questa attività il provider di token personalizzato deriva dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenProvider> ed esegue l'override del metodo <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29>.Questo metodo creare e restituisce un nuovo `UserNameSecurityToken`.  
  
    ```  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
        // obtain username and password from the user using console window  
        string username = GetUserName();  
        string password = GetPassword();  
        Console.WriteLine("username: {0}", username);  
  
        // return new UserNameSecurityToken containing information obtained from user  
        return new UserNameSecurityToken(username, password);  
    }  
  
    ```  
  
2.  Scrivere il gestore di token di sicurezza personalizzato.  
  
     La classe <xref:System.IdentityModel.Selectors.SecurityTokenManager> viene utilizzata per creare <xref:System.IdentityModel.Selectors.SecurityTokenProvider> per il <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> specifico che viene passato nel metodo `CreateSecurityTokenProvider`.Viene inoltre utilizzato un gestore del token di sicurezza per creare autenticatori del token e serializzatori del token, che però non sono trattati in questo esempio.In questo esempio, il gestore del token di sicurezza personalizzato eredita dalla classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> ed esegue l'override del metodo `CreateSecurityTokenProvider` per restituire il provider di token nome utente personalizzato quando i requisiti del token passati indicano che il provider nome utente è richiesto.  
  
    ```  
    public class MyUserNameSecurityTokenManager : ClientCredentialsSecurityTokenManager  
    {  
        MyUserNameClientCredentials myUserNameClientCredentials;  
  
        public MyUserNameSecurityTokenManager(MyUserNameClientCredentials myUserNameClientCredentials)  
            : base(myUserNameClientCredentials)  
        {  
            this.myUserNameClientCredentials = myUserNameClientCredentials;  
        }  
  
        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)  
        {  
            // if token requirement matches username token return custom username token provider  
            // otherwise use base implementation  
            if (tokenRequirement.TokenType == SecurityTokenTypes.UserName)  
            {  
                return new MyUserNameTokenProvider();  
            }  
            else  
            {  
                return base.CreateSecurityTokenProvider(tokenRequirement);  
            }  
        }  
    }  
    ```  
  
3.  Scrivere una credenziale client personalizzata.  
  
     La classe delle credenziali client viene utilizzata per rappresentare le credenziali configurate per il proxy client e crea un gestore del token di sicurezza utilizzato per ottenere gli autenticatori del token, i provider di token e il serializzatore di token.  
  
    ```  
    public class MyUserNameClientCredentials : ClientCredentials  
    {  
        public MyUserNameClientCredentials()  
            : base()  
        {  
        }  
  
        protected override ClientCredentials CloneCore()  
        {  
            return new MyUserNameClientCredentials();  
        }  
  
        public override SecurityTokenManager CreateSecurityTokenManager()  
        {  
            // return custom security token manager  
            return new MyUserNameSecurityTokenManager(this);  
        }  
    }  
    ```  
  
4.  Configurare il client per l'utilizzo della credenziale client personalizzata.  
  
     L'esempio elimina la classe della credenziale client predefinita e fornisce la nuova classe della credenziale client affinché il client possa utilizzare la credenziale client personalizzata.  
  
    ```  
    static void Main()  
    {  
        // ...  
           // Create a client with given client endpoint configuration  
          CalculatorClient client = new CalculatorClient();  
  
          // set new credentials  
           client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));  
         client.ChannelFactory.Endpoint.Behaviors.Add(new MyUserNameClientCredentials());  
       // ...  
    }  
  
    ```  
  
 Nel servizio, per visualizzare le informazioni sul chiamante è possibile utilizzare <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> come mostra il codice di esempio seguente.La classe <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> contiene informazioni sulle attestazioni circa il chiamante corrente.  
  
```  
static void DisplayIdentityInformation()  
{  
    Console.WriteLine("\t\tSecurity context identity  :  {0}",   
        ServiceSecurityContext.Current.PrimaryIdentity.Name);  
}  
  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
## File batch di installazione  
 Il file batch Setup.bat incluso con questo esempio consente di configurare il server con il certificato attinente per eseguire un'applicazione indipendente che richiede sicurezza server basata su certificato.Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.  
  
 Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.  
  
-   Creazione del certificato server.  
  
     Le righe seguenti del file batch Setup.bat creano il certificato server da utilizzare.La variabile `%SERVER_NAME%` specifica il nome del server.Modificare questa variabile per specificare il nome del server.Il valore predefinito in questo file batch è localhost.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
-   Installazione del certificato server nell'archivio certificati attendibile del client:  
  
     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio delle persone attendibile del client.Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio della popolazione dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
  
    ```  
  
> [!NOTE]
>  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di SDK di Windowse richiede che la variabile di ambiente MSSDK punti alla directory in cui è installato SDK.Questa variabile di ambiente viene impostata automaticamente in un prompt dei comandi di SDK di Windows.  
  
#### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di aver eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
#### Per eseguire l'esempio nello stesso computer  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] con privilegi di amministratore ed eseguire Setup.bat dalla cartella di installazione dell'esempio.In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
    > [!NOTE]
    >  Il file batch Setup.bat è progettato per essere eseguito da un prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].La variabile di ambiente PATH impostata nel prompt dei comandi di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] punta alla directory che contiene file eseguibili richiesti dallo script Setup.bat.  
  
2.  Avviare service.exe da service\\bin.  
  
3.  Avviare Client.exe da \\client\\bin.L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
4.  Al prompt del nome utente, digitare un nome utente.  
  
5.  Al prompt della password, utilizzare la stessa stringa digitata per il prompt del nome utente.  
  
6.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Creare una directory sul computer del servizio per i file binari del servizio.  
  
2.  Copiare i file di programma del servizio nella directory del servizio sul computer relativo.Copiare i file Setup.bat e Cleanup.bat nel computer del servizio.  
  
3.  È necessario disporre di un certificato server con il nome del soggetto che contiene il nome di dominio completo del computer.Il file Service.exe.config deve essere aggiornato per riflettere il nome del nuovo certificato.È possibile creare il certificato server modificando il file batch Setup.bat.Si noti che è necessario eseguire il file setup.bat in un prompt dei comandi di Visual Studio aperto con privilegi di amministratore.È necessario impostare la variabile `%SERVER_NAME%` sul nome host completo del computer utilizzato per ospitare il servizio.  
  
4.  Copiare il certificato server nell'archivio CurrentUser\-TrustedPeople del client.Questo passaggio non è necessario quando il certificato server è emesso da un'autorità emittente client attendibile.  
  
5.  Nel file Service.exe.config sul computer del servizio modificare il valore dell'indirizzo di base per specificare un nome del computer completo anziché localhost.  
  
6.  Sul computer del servizio eseguire service.exe da un prompt dei comandi.  
  
7.  Copiare i file del programma client dalla cartella \\client\\bin\\, presente nella cartella specifica del linguaggio, nel computer client.  
  
8.  Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.  
  
9. Sul computer client avviare `Client.exe` da una finestra del prompt dei comandi.  
  
10. Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.bat nella cartella degli esempi dopo che è terminata l'esecuzione dell'esempio.  
  
## Vedere anche