---
title: "Servizio facciata attendibile | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c34d1a8f-e45e-440b-a201-d143abdbac38
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Servizio facciata attendibile
In questo scenario viene illustrato come propagare le informazioni di identità del chiamante da un servizio a un'altro usando un'infrastruttura di sicurezza di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
 Si tratta di un modello di progettazione comune per esporre la funzionalità fornita da un servizio alla rete pubblica usando un servizio di facciata. Il servizio di facciata risiede in genere nella rete perimetrale e comunica con un servizio back\-end che implementa la regola business e ha accesso ai dati interni. Il canale di comunicazione tra il servizio di facciata e il servizio back\-end passa attraverso un firewall e in genere è limitato a un solo obiettivo.  
  
 L'esempio è costituito dai componenti seguenti:  
  
-   Client calcolatrice  
  
-   Servizio di facciata calcolatrice  
  
-   Servizio back\-end calcolatrice  
  
 Il servizio di facciata ha la responsabilità di convalidare la richiesta e autenticare il chiamante. Una volta completate correttamente l'autenticazione e la convalida, inoltra la richiesta al servizio back\-end usando il canale di comunicazione controllato dalla rete perimetrale alla rete interna. I servizio di facciata include come parte della richiesta inoltrata informazioni sull'identità del chiamante, in modo che il servizio back\-end possa usare queste informazioni nell'elaborazione. L'identità del chiamante viene trasmessa usando un token di sicurezza `Username` all'interno dell'intestazione di `Security` del messaggio. L'esempio usa l'infrastruttura di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per trasmettere ed estrarre queste informazioni dall'intestazione di `Security`.  
  
> [!IMPORTANT]
>  Il servizio back\-end considera attendibile il servizio di facciata per autenticare il chiamante. Di conseguenza il servizio back\-end non autentica nuovamente il chiamante, ma usa le informazioni di identità fornite dal servizio di facciata nella richiesta inoltrata. A causa di questa relazione di trust, il servizio back\-end deve autenticare il servizio di facciata in modo da assicurare che il messaggio inoltrato provenga da una fonte attendibile, in questo caso, dal servizio di facciata.  
  
## Implementazione  
 In questo esempio vengono riportati due percorsi di comunicazione. Il primo è tra il client e il servizio di facciata, il secondo è tra il servizio di facciata e il servizio back\-end.  
  
### Percorso di comunicazione tra il client e il servizio di facciata  
 Il percorso di comunicazione dal client al servizio di facciata usa `wsHttpBinding` con un tipo di credenziale `UserName`. Questo significa che il client usa il nome utente e la password per autenticare al servizio di facciata e il servizio di facciata usa il certificato X.509 per autenticare il client. L'aspetto della configurazione dell'associazione è analogo al seguente:  
  
```  
<bindings>  
  <wsHttpBinding>  
    <binding name="Binding1">  
      <security mode="Message">  
        <message clientCredentialType="UserName"/>  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 Il servizio di facciata autentica il chiamante usando l'implementazione `UserNamePasswordValidator` personalizzata. A scopo dimostrativo, l'autenticazione assicura solo che il nome utente del chiamante corrisponda alla password presentata. Nella situazione del mondo reale l'utente viene probabilmente autenticato usando Active Directory o un provider di appartenenze ASP.NET personalizzato. L'implementazione del validator si trova nel file `FacadeService.cs`.  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // check that username matches password  
        if (null == userName || userName != password)  
        {  
            Console.WriteLine("Invalid username or password");  
            throw new SecurityTokenValidationException(  
                       "Invalid username or password");  
        }  
    }  
}  
```  
  
 Il validator personalizzato viene configurato per essere usato nel comportamento `serviceCredentials` nel file di configurazione del servizio di facciata. Questo comportamento viene inoltre usato per configurare il certificato X.509 del servizio.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="FacadeServiceBehavior">  
      <!--The serviceCredentials behavior allows you to define -->  
      <!--a service certificate. -->  
      <!--A service certificate is used by the service to  -->  
      <!--authenticate itself to its clients and to provide  -->  
      <!--message protection. -->  
      <!--This configuration references the "localhost"  -->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate   
               findValue="localhost"   
               storeLocation="LocalMachine"   
               storeName="My"   
               x509FindType="FindBySubjectName" />  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
            customUserNamePasswordValidatorType=  
           "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,  
            FacadeService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
### Percorso di comunicazione tra il servizio di facciata e il servizio back\-end  
 Il percorso di comunicazione dal servizio di facciata al servizio back\-end usa un `customBinding` costituito da molti elementi di associazione. Questa associazione consente di raggiungere due obiettivi. Autentica il servizio di facciata e il servizio back\-end per assicurare che la comunicazione sia protetta e che provenga da una fonte attendibile. Trasmette inoltre l'identità del chiamante iniziale all'interno del token di sicurezza `Username`. In questo caso, solo il nome utente del chiamante iniziale viene trasmesso al servizio back\-end, la password non viene inclusa nel messaggio. Questo è dovuto al fatto che il servizio back\-end considera attendibile il servizio di facciata per autenticare il chiamante prima di inoltrargli la richiesta. Poiché il servizio di facciata si autentica con il servizio back\-end, il servizio back\-end può considerare le informazioni contenute nella richiesta inoltrata attendibili.  
  
 Di seguito è riportata la configurazione di associazione per questo percorso di comunicazione.  
  
```  
<bindings>  
  <customBinding>  
    <binding name="ClientBinding">  
      <security authenticationMode="UserNameOverTransport"/>  
      <windowsStreamSecurity/>  
      <tcpTransport/>  
    </binding>  
  </customBinding>  
</bindings>  
```  
  
 L'elemento di associazione [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) si occupa di trasmettere ed estrarre il nome utente del chiamante iniziale.[\<sicurezzaFlussoWindows\>](../../../../docs/framework/configure-apps/file-schema/wcf/windowsstreamsecurity.md) e [\<trasportoTcp\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) si occupano di autenticare il servizio di facciata e il servizio back\-end e della protezione dei messaggi.  
  
 Per inoltrare la richiesta l'implementazione del servizio di facciata deve fornire il nome utente del chiamante iniziale, in modo che l'infrastruttura di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possa posizionarlo nel messaggio inoltrato. Il nome utente del chiamante iniziale viene fornito nell'implementazione del servizio di facciata impostandolo nella proprietà `ClientCredentials` sull'istanza del proxy client che il servizio di facciata usa per comunicare con il servizio back\-end.  
  
 Nel codice seguente viene illustrata l'implementazione del metodo `GetCallerIdentity` nel servizio di facciata. Gli altri metodi usano lo stesso modello.  
  
```  
public string GetCallerIdentity()  
{  
    CalculatorClient client = new CalculatorClient();  
    client.ClientCredentials.UserName.UserName = ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    string result = client.GetCallerIdentity();  
    client.Close();  
    return result;  
}  
```  
  
 Come illustrato nel codice precedente, la password non viene impostata nella proprietà `ClientCredentials`. Viene impostato solo il nome utente. In questo caso l'infrastruttura di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea un token di sicurezza del nome utente senza una password, esattamente quello che richiede questo scenario.  
  
 Nel servizio back\-end, le informazioni contenute nel token di sicurezza del nome utente devono essere autenticate. Per impostazione predefinita, la sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tenta di eseguire il mapping dell'utente a un account di Windows usando la password fornita. In questo caso non è stata fornita una password e non è necessario che il servizio back\-end autentichi il nome utente, visto che l'autenticazione è già stata eseguita dal servizio di facciata. Per implementare questa funzionalità in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], viene fornito un `UserNamePasswordValidator` personalizzato che impone solo che venga specificato un nome utente nel token e non esegue altre autenticazioni.  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // Ignore the password because it is empty,   
        // we trust the facade service to authenticate the client.  
        // Accept the username information here so that the   
        // application gets access to it.  
        if (null == userName)  
        {  
            Console.WriteLine("Invalid username");  
            throw new   
             SecurityTokenValidationException("Invalid username");  
        }  
    }  
}  
```  
  
 Il validator personalizzato viene configurato per essere usato nel comportamento `serviceCredentials` nel file di configurazione del servizio di facciata.  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="BackendServiceBehavior">  
      <serviceCredentials>  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
           customUserNamePasswordValidatorType=  
          "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,   
           BackendService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Per estrarre le informazioni relative al nome utente e all'account del servizio di facciata attendibile, l'implementazione del servizio back\-end usa la classe `ServiceSecurityContext`. Nel codice seguente viene illustrato come implementare il metodo `GetCallerIdentity`.  
  
```  
public string GetCallerIdentity()  
{  
    // Facade service is authenticated using Windows authentication.  
    //Its identity is accessible.  
    // On ServiceSecurityContext.Current.WindowsIdentity.  
    string facadeServiceIdentityName =   
          ServiceSecurityContext.Current.WindowsIdentity.Name;  
  
    // The client name is transmitted using Username authentication on   
    //the message level without the password  
    // using a supporting encrypted UserNameToken.  
    // Claims extracted from this supporting token are available in   
    // ServiceSecurityContext.Current.AuthorizationContext.ClaimSets   
    // collection.  
    string clientName = null;  
    foreach (ClaimSet claimSet in   
        ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
    {  
        foreach (Claim claim in claimSet)  
        {  
            if (claim.ClaimType == ClaimTypes.Name &&   
                                   claim.Right == Rights.Identity)  
            {  
                clientName = (string)claim.Resource;  
                break;  
            }  
        }  
    }  
    if (clientName == null)  
    {  
        // In case there was no UserNameToken attached to the request.  
        // In the real world implementation the service should reject   
        // this request.  
        return "Anonymous caller via " + facadeServiceIdentityName;  
    }  
  
    return clientName + " via " + facadeServiceIdentityName;  
}  
```  
  
 Le informazioni relative all'account del servizio di facciata vengono estratte usando la proprietà `ServiceSecurityContext.Current.WindowsIdentity`. Per accedere alle informazioni relative al chiamante iniziale, il servizio back\-end usa la proprietà `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets`. Cerca un'attestazione di `Identity` di tipo `Name`. Questa attestazione viene generata automaticamente dall'infrastruttura di sicurezza di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dalle informazioni contenute nel token di protezione `Username`.  
  
## Esecuzione dell'esempio  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client. Premere INVIO nella finestra del client per arrestare il client. È possibile premere INVIO nelle finestre della console del servizio di facciata e del servizio back\-end per arrestare i servizi.  
  
```  
Username authentication required.  
Provide a valid machine or domain ac  
   Enter username:  
user  
   Enter password:  
****  
user via MyMachine\testaccount  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
 Il file batch Setup.bat incluso nell'esempio relativo allo scenario della Facciata attendibile consente di configurare il server con un certificato attinente per eseguire il servizio di facciata che richiede sicurezza server basata su certificato per autenticarsi sul client. Per altre informazioni, vedere la procedura di configurazione alla fine di questo argomento.  
  
 Di seguito viene presentata una breve panoramica delle diverse sezioni dei file batch.  
  
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
  
     La variabile `%SERVER_NAME%` specifica il nome del server. Il valore predefinito è localhost. Il certificato viene archiviato nell'archivio LocalMachine.  
  
-   Installazione del servizio di facciata nell'archivio certificati attendibili del client.  
  
     La riga seguente copia il servizio di facciata nell'archivio Persone attendibili del client. Questo passaggio è necessario perché certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client. Se è già disponibile un certificato impostato come radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il popolamento dell'archivio certificati client con il certificato server non è necessario.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
#### Per eseguire l'esempio sullo stesso computer  
  
1.  Assicurarsi che il percorso includa la cartella in cui è situato Makecert.exe.  
  
2.  Eseguire Setup.bat dalla cartella di installazione dell'esempio. In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.  
  
3.  Avviare BackendService.exe dalla directory \\BackendService\\bin in una finestra della console separata  
  
4.  Avviare FacadeService.exe dalla directory \\FacadeService\\bin in una finestra della console separata  
  
5.  Avviare Client.exe da \\client\\bin. L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
6.  Se il client e il servizio non possono comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire la pulizia dopo l'esempio  
  
1.  Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)]. Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\TrustedFacade`  
  
## Vedere anche